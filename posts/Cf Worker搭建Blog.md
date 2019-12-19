# CF Blog

<a href="https://blog.buildtest.club/">
  <img src="https://secure.gravatar.com/avatar/" width="100" alt="App Icon" />
</a>
[项目地址](https://github.com/LittleRey/CloudFlare-Worker-Blog)


# 用法
将worker.js粘贴到Cloudflare worker面板中

# 如何撰写博客

首先使用随机名称创建一个Github项目，然后在本地克隆该项目。
```
# Example
Git clone https://github.com/LittleRey/CloudFlare-Worker-Blog
Cd cloudflare-worker-blog/
```
转到项目文件夹并创建一个新的帖子文件夹## 如何编写文章

首先创建一个 Github 项目，名字随意，然后将这个项目 clone 到本地。

```
# 示例
git clone https://github.com/LittleRey/CloudFlare-Worker-Blog
cd cloudflare-worker-blog/
```

进入项目文件夹，新建一个 posts 文件夹

```
mkdir posts/
```

在里面编写文章，内容一般用 .md 后缀即可，例如 helloworld.md

写完之后回到项目根目录（就是上级目录），然后新建一个 list.json

```
touch list.json
```

# List.json 格式

```json
[
  {
    "title":"文章1",
    "time":"2019-06-01",
    "file":"posts/1.md"
  },
  {
    "title":"文章2",
    "time":"2019-06-03",
    "file":"posts/2.md"
  },
  {
    "title":"文章3",
    "time":"2019-06-07",
    "file":"posts/3.md"
  } <--注意json格式，最后一篇文章的这里不需要逗号
]
```

一切就绪后，使用 `git push` 命令将代码推送到仓库上。

然后修改你的 workers，设置 github_base 为你的仓库名称

现在访问你的 Workers 即可看到文章。
