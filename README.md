# CF Blog

<a href="https://blog.buildtest.club/">
  <img src="https://secure.gravatar.com/avatar/" width="100" alt="App Icon" />
</a>

## Cloudflare Workers Blog
![Crates.io](https://img.shields.io/crates/l/rustc-serialize)
[![Build Status](https://travis-ci.org/agalwood/Motrix.svg?branch=master)](https://travis-ci.org/agalwood/Motrix)
![Spiget Download Size](https://img.shields.io/spiget/download-size/6)
![Relative date](https://img.shields.io/date/1571760316)


[English](./README.md) | [简体中文](./README-CN.md)
# Usage
Paste workers.js into the Cloudflare worker panel
# How to write a blog

First create a Github project with a random name and then clone the project locally.

```
# Example
Git clone https://github.com/LittleRey/CloudFlare-Worker-Blog
Cd cloudflare-worker-blog/
```

Go to the project folder and create a new post folder

```
Mkdir posts/
```

Write an article inside, the content is generally suffixed with .md, for example helloworld.md

After writing, go back to the project root directory (that is, the parent directory), and then create a new list.json
# List format
```json
[
  {
    "title":"name1",
    "time":"2019-06-01",
    "file":"posts/1.md"
  },
  {
    "title":"name2",
    "time":"2019-06-03",
    "file":"posts/2.md"
  },
  {
    "title":"name3",
    "time":"2019-06-07",
    "file":"posts/3.md"
  } <-- # There is no comma here #
]
```

