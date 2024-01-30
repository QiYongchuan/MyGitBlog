# [实现无限滚动遇到的坑—document.body.offsetHeight 的值一直不变？](https://github.com/QiYongchuan/MyGitBlog/issues/76)

### 实现无限滚动遇到的坑 --css样式设置

遇到的最大的问题是，
```
      if (window.innerHeight + window.scrollY > document.body.offsetHeight && !isLoading) {
        isLoading = true; // 设置标志变量为true，表示加载操作开始
        load();
        console.log('开始加载');
        console.log(window.innerHeight, window.scrollY, document.body.offsetHeight);
```
  在第一次到达底部成功加载后，就会无限次的重复加载，而不是像判断条件写的那样，等window.innerHeight + window.scrollY > document.body.offsetHeight时，再进行请求加载。

  打印后发现数值有问题：

  document.body.offsetHeight  的值只有80？

  一度以为是属性用错了或者这个属性发生了变化，换用document.documentElement.scrollHeight 后，发现问题没有解决，是96px

  回头发现，这个80的数值，是一开始设置的div的数值

这里：
  <body>
  <div id="posts"></div>
  </body>


正好看到有一篇文章中，offsetHeight的数值不变的

[Javascript offsetHeight not updating from initial rendered height?](https://stackoverflow.com/questions/53566405/javascript-offsetheight-not-updating-from-initial-rendered-height)

他的原因是：
>FFS! Found it... I had the height set to 100% on the global html element :

> html {
  height: 100%; // Arrrrggghhhh!
  width: 100%;
}




已经写死了html，也就是document的值。

我于是检查这一块的东西，发现确实有问题：
```
  // Add a new post with given contents to DOM
      function add_post(contents) {
        // Create new post
        const post = document.createElement('div');
        post.className = 'post';
        post.innerHTML = contents;

        // Add post to DOM
        document.querySelector('#posts').append(post)
      }
```
这是我请求数据后插入的内容，每次插入一个  名为post类的元素

但是我页面中的是id = posts 的div，我一开始设置的也是这个的高度，正好是80px，而在我加载页面的过程中，document的高度也始终是80px；

我应该设置的是每次新加入进来的元素post的高度，而不是post外面的盒子posts的高度，这样高度就写死了，而不是随着内部内容的增加而增加了。

也就是：
```
  .post {
      height: 80px;
      background: green;
      width: 200px;
      margin-bottom: 5px;

    }
```
问题解决。


