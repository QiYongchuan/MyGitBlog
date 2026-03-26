# [Tailscale + SSH 多设备并网完整教程](https://github.com/QiYongchuan/MyGitBlog/issues/147)

# Tailscale + SSH 多设备并网完整教程

**适用人群**：完全小白
**目标**：让多台设备（Windows、macOS、Linux）通过 Tailscale 组网，实现双向 SSH 免密访问
**工具**：Claude Code + 命令行

---

## 快速检查清单

开始前确保：
- [ ] 所有设备都已安装 Tailscale 并登录同一账号
- [ ] 了解如何使用 Claude Code 执行命令
- [ ] 有设备的管理员权限

---

## 第一步：确认 Tailscale 组网

### 1.1 在所有设备上查看 Tailscale 状态

**Windows / PowerShell:**
```powershell
tailscale status
```

**macOS / Linux:**
```bash
tailscale status
```

### 1.2 记录设备信息

创建一个设备清单（示例）：

| 设备名 | Tailscale IP | 系统 | 用户名 |
|--------|--------------|------|--------|
| laptop | 100.91.53.84 | Windows | user1 |
| macmini | 100.80.153.60 | macOS | user2 |
| server | 100.94.2.125 | Linux | root |

**获取用户名命令：**
```bash
# Windows
$env:USERNAME

# macOS/Linux
whoami
```

---

## 第二步：生成 SSH 密钥对

### 2.1 检查是否已有密钥

```bash
# Windows/macOS/Linux
ls ~/.ssh/id_ed25519*
```

**如果已存在**：跳过此步
**如果不存在**：继续执行

### 2.2 生成新密钥

```bash
ssh-keygen -t ed25519 -C "你的邮箱或标识"
```

**一路按回车**（使用默认路径，空密码）

---

## 第三步：配置免密登录

### 核心理解

| 系统 | 公钥存储位置 |
|------|--------------|
| macOS/Linux | `~/.ssh/authorized_keys` |
| **Windows** | `C:\ProgramData\ssh\administrators_authorized_keys` ⚠️ |

### 3.1 场景一：macOS/Linux → macOS/Linux

**假设**：设备 A (100.x.x.1) 要免密登录设备 B (100.x.x.2)

**在设备 A 上执行：**
```bash
# 复制公钥到目标设备
ssh-copy-id username@100.x.x.2
```

**输入一次密码后永久生效**

### 3.2 场景二：macOS/Linux → Windows

**假设**：Mac (100.80.153.60) 要免密登录 Windows (100.91.53.84)

**方法 1：使用 ssh-copy-id（推荐）**
```bash
# 在 Mac 上执行
ssh-copy-id user@100.91.53.84
```

**方法 2：手动复制（如果 ssh-copy-id 失败）**

在 Mac 上获取公钥：
```bash
cat ~/.ssh/id_ed25519.pub
```

在 Windows 上（管理员 PowerShell）：
```powershell
# 创建目录（如果不存在）
New-Item -ItemType Directory -Force -Path "C:\ProgramData\ssh"

# 追加公钥（替换 <公钥内容>）
Add-Content -Path "C:\ProgramData\ssh\administrators_authorized_keys" -Value "<公钥内容>" -Force

# 重启 SSH 服务
Restart-Service sshd
```

### 3.3 场景三：Windows → macOS/Linux

**在 Windows 上执行：**
```powershell
# 复制公钥到目标
type $env:USERPROFILE\.ssh\id_ed25519.pub | ssh user@100.x.x.x "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

**输入一次密码后永久生效**

### 3.4 场景四：Windows → Windows

**在源 Windows 上获取公钥：**
```powershell
cat $env:USERPROFILE\.ssh\id_ed25519.pub
```

**在目标 Windows 上（管理员 PowerShell）：**
```powershell
Add-Content -Path "C:\ProgramData\ssh\administrators_authorized_keys" -Value "<公钥内容>" -Force
Restart-Service sshd
```

---

## 第四步：验证免密登录

### 4.1 基础测试

```bash
# 测试免密连接
ssh -o BatchMode=yes user@目标IP "echo 免密成功"
```

**成功输出**：`免密成功`
**失败输出**：`Permission denied`

### 4.2 实际连接测试

```bash
# 实际连接
ssh user@目标IP
```

**如果不需要输入密码 → 配置成功 ✅**

---

## 第五步：（可选）自动化密码输入

如果 ssh-copy-id 需要密码且无法手动输入，使用 expect：

**在 macOS/Linux 上：**
```bash
# 安装 expect（如果未安装）
brew install expect  # macOS
# 或
sudo apt install expect  # Ubuntu/Debian

# 自动化脚本
cat << 'EOF' | expect
set timeout 30
spawn ssh-copy-id user@目标IP
expect "password:" { send "你的密码\r" }
expect eof
EOF
```

---

## 故障排查速查表

| 问题 | 可能原因 | 解决方法 |
|------|----------|----------|
| `Permission denied` | 公钥未正确添加 | 检查目标设备的 authorized_keys 文件 |
| Windows 免密失败 | 公钥位置错误 | 确认在 `C:\ProgramData\ssh\administrators_authorized_keys` |
| Windows 写入失败 | 权限不足 | 使用管理员 PowerShell |
| `No route to host` | Tailscale 未连接 | 检查 `tailscale status` |
| `Connection refused` | SSH 服务未启动 | Windows: `Start-Service sshd` <br> Mac: `sudo systemsetup -setremotelogin on` |

### Windows 常见问题

**检查 SSH 服务状态：**
```powershell
Get-Service sshd
```

**如果未运行：**
```powershell
Start-Service sshd
Set-Service sshd -StartupType Automatic
```

**检查公钥文件权限：**
```powershell
icacls "C:\ProgramData\ssh\administrators_authorized_keys"
# 应显示：Administrators:(F) 和 SYSTEM:(F)
```

**修复权限：**
```powershell
icacls "C:\ProgramData\ssh\administrators_authorized_keys" /inheritance:r
icacls "C:\ProgramData\ssh\administrators_authorized_keys" /grant "Administrators:F"
icacls "C:\ProgramData\ssh\administrators_authorized_keys" /grant "SYSTEM:F"
```

### macOS/Linux 常见问题

**检查 SSH 权限：**
```bash
ls -la ~/.ssh/authorized_keys
# 应该是：-rw------- (600)
```

**修复权限：**
```bash
chmod 600 ~/.ssh/authorized_keys
chmod 700 ~/.ssh
```

---

## 快速配置模板（复制粘贴用）

### 模板 A：两台 macOS/Linux 互连

```bash
# 设备 1 → 设备 2
ssh-copy-id user2@设备2的IP

# 设备 2 → 设备 1
ssh-copy-id user1@设备1的IP
```

### 模板 B：Mac → Windows

```bash
# 在 Mac 上
ssh-copy-id windows_user@Windows的IP
```

### 模板 C：Windows → Mac

```powershell
# 在 Windows 上
type $env:USERPROFILE\.ssh\id_ed25519.pub | ssh mac_user@Mac的IP "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

---

## 验证清单

完成后测试：

```bash
# 从设备 A 连接设备 B
ssh user@设备B的IP "hostname"

# 从设备 B 连接设备 A
ssh user@设备A的IP "hostname"

# 如果都返回主机名，配置成功！
```

---

## 进阶配置（可选）

### 配置 SSH 别名

编辑 `~/.ssh/config`（或 Windows 的 `C:\Users\你的用户名\.ssh\config`）：

```
Host macmini
    HostName 100.80.153.60
    User qyc

Host windows
    HostName 100.91.53.84
    User Qyc

Host server
    HostName 100.94.2.125
    User root
```

**之后只需：**
```bash
ssh macmini
ssh windows
ssh server
```

### 禁用密码登录（仅允许密钥）

**在目标设备上：**

```bash
# 编辑 sshd_config
sudo nano /etc/ssh/sshd_config  # macOS/Linux
# 或
notepad C:\ProgramData\ssh\sshd_config  # Windows
```

**修改：**
```
PasswordAuthentication no
```

**重启 SSH 服务：**
```bash
sudo systemctl restart sshd  # Linux
sudo launchctl stop com.openssh.sshd && sudo launchctl start com.openssh.sshd  # macOS
Restart-Service sshd  # Windows
```

---

## 总结

1. **安装 Tailscale** → 所有设备在同一虚拟网络
2. **生成 SSH 密钥** → 每台设备生成 id_ed25519
3. **交换公钥** → 复制到目标设备的 authorized_keys
4. **验证** → 测试免密连接

**核心要点：**
- macOS/Linux 公钥在 `~/.ssh/authorized_keys`
- **Windows 公钥在 `C:\ProgramData\ssh\administrators_authorized_keys`**
- 权限必须正确设置
- Windows 需要重启 sshd 服务

---

*教程版本：v1.0*
*最后更新：2026-03-26*
*问题反馈：查看故障排查速查表*
