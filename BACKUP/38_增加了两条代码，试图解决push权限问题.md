# [增加了两条代码，试图解决push权限问题](https://github.com/QiYongchuan/MyGitBlog/issues/38)

设置 Git 远程 URL 

`- name: Set Git Remote URL with Token
  run: git remote set-url origin https://x-access-token:${{ secrets.G_T }}@github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
`

---

仍然没有解决问题：

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/5b1312df-2fef-4863-a411-f0ad251d0b0d)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/064ed3a8-081b-4bd1-a369-3202f6b1f940)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/8172a38d-63bd-4538-a7ea-899f02bf4529)
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/366a8389-5242-4899-8a01-1983822623eb)
