---
layout: post
title: "使用github page建立自己的博客"
category: 
tags: []
---

## [github page](https://pages.github.com/)

　　首先你需要一个github账号

　　然后在github建立一个项目, 项目名为 USERNAME.github.io

　　可以git pull 一个index.html文件上去, 访问项目名的网址, 看到效果了吗?

　　github page支持[hexo](https://hexo.io/ )和[jekyll](https://jekyllrb.com/)

## [jekyll](https://jekyllrb.com/)
　　jekyll 是一个将Markdown(或文本)转化为静态网页和博客的框架.

# 安装:

　　jekyll是基于<font color="red">Ruby</font>的, 所以需要先安装Ruby.

　　windows用户进入[rubyinstaller.org](http://rubyinstaller.org/downloads/)下载安装即可

安装成功后

　　`gem install jekyll bundler`

# 使用:

```
jekyll new my-awesome-site

cd my-awesome-site

bundle exec jekyll serve
```

　　在浏览器中打开[localhost:4000](localhost:4000)即可浏览实际效果


# 新增文章:

　　新增文章需要在_posts文件夹下新建一个markdown文件

　　文件名: YEAR-MONTH-DAY-TITLE-TITLE.markdown

　　若想方便快捷, 可以借助rakefile的方法:

　　复制
```
require 'rake'
require 'yaml'

SOURCE = "."
CONFIG = {
  'posts' => File.join(SOURCE, "_posts"),
  'post_ext' => "md",
}

# Usage: rake post title="A Title"
desc "Begin a new post in #{CONFIG['posts']}"
task :post do
  abort("rake aborted: '#{CONFIG['posts']}' directory not found.") unless FileTest.directory?(CONFIG['posts'])
  title = ENV["title"] || "new-post"
  slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
  filename = File.join(CONFIG['posts'], "#{Time.now.strftime('%Y-%m-%d')}-#{slug}.#{CONFIG['post_ext']}")
  if File.exist?(filename)
    abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
  end

  puts "Creating new post: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: post"
    post.puts "title: \"#{title.gsub(/-/,' ')}\""
    post.puts "category: "
    post.puts "tags: []"
    post.puts "---"
  end
end # task :post
```
　　进一个文件,命名为Rakefile, 放到项目根目录即可

　　使用命令
`rake post title="hello world"`

　　看看_posts下是否多了一个md文件呢?

## [git](https://git-scm.com/)
　　使用git将文件上传至github

```
git remote set-url origin git@github.com:USERNAME/USERNAME.github.io.git

git add .

git push origin master
```

　　以上是最基本的在githubpage建立博客的说明了