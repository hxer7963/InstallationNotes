[TOC]

### 1. install jekyll on macOS Mojave 10.14.4[^1]

```sh
$ gem install jekyll bundler
Fetching: safe_yaml-1.0.5.gem (100%)
ERROR:  While executing gem ... (Gem::FilePermissionError)
    You don't have write permissions for the /Library/Ruby/Gems/2.3.0 directory.
$ sudo a+w /Library/Ruby/Gems/2.3.0
$ gem install jekyll bundler
Fetching: safe_yaml-1.0.5.gem (100%)
ERROR:  While executing gem ... (Errno::EACCES)
    Permission denied @ rb_sysopen - /Library/Ruby/Gems/2.3.0/cache/safe_yaml-1.0.5.gem
$ ruby -v
ruby 2.3.7p456
```

几乎每个命令均提示`permission denied`，虽然OS X自带Ruby环境，但只为系统使用；用户能用的只有system，`/Library`目录下需要`root`权限，`gem`没使用`sudo`(我也没使用一直使用`sudo gem`)。用户Ruby环境最好与系统环境隔离，同时jekyll 需要Ruby version 2.4.0 or above[^1]，所以安装`rvm`，来管理多版本ruby.

#### 1.1 RVM vs. RubyGems vs. Gem vs. Bundle

RVM：安装、管理Ruby环境(类似Conda之于Python?)，指定Ruby应用对应的Ruby环境；

RubyGems：Ruby package manager，将Ruby应用程序打包成到一个gem中，作为一个安装单元，安装的Ruby中自带RubyGems。

Gem：封装起来的Ruby应用程序或代码库；

> 终端使用的`gem`命令通过RubyGems管理Gem包；

Gemfile：应用程序依赖第三方库，

Bundle：自动下载安装Gemfile中依赖的包，相当于多次运行RubyGems?

参考：[整理Ruby相关的各种概念（rvm, gem, bundle, rake, rails等）](<https://henter.me/post/ruby-rvm-gem-rake-bundle-rails.html>) 

#### 1.2  install rvm on OS X

rvm(Ruby Version Manager)，包括`Ruby`版本管理和`Gem`库管理(gemset).

```sh
$ curl -L get.rvm.io | bash -s stable
...
Installing RVM to /Users/hxer/.rvm/
    Adding rvm PATH line to /Users/hxer/.profile /Users/hxer/.mkshrc /Users/hxer/.bashrc /Users/hxer/.zshrc.
    * To start using RVM you need to run `source /Users/hxer/.rvm/scripts/rvm`
    in all your open shell windows, in rare cases you need to reopen all shell windows.
$ rvm -v
rvm 1.29.7 (latest) by Michal Papis, Piotr Kuczynski, Wayne E. Seguin [https://rvm.io]
## 修改rvm安装源为淘宝源
$ sed -i -e 's/ftp\.ruby-lang\.org\/pub\/ruby/ruby\.taobao\.org\/mirrors\/ruby/g' ~/.rvm/config/db
$ rvm list
# No rvm rubies installed yet. Try 'rvm help install'.
$ rvm list known
...
# MRI Rubies
[ruby-]2.3[.8]
[ruby-]2.4[.5]
[ruby-]2.5[.3]
[ruby-]2.6[.0]
ruby-head
...
$ rvm install 2.5.3
...
Installing required packages: autoconf, automake, libtool, pkg-config, coreutils, libyaml, readline, libksba, openssl@1.1 - please wait

Requirements installation successful.
Installing Ruby from source to: /Users/hxer/.rvm/rubies/ruby-2.5.3, this may take a while depending on your cpu(s)...
ruby-2.5.3 - #downloading ruby-2.5.3, this may take a while depending on your connection...
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 13.5M  100 13.5M    0     0   622k      0  0:00:22  0:00:22 --:--:--  695k
ruby-2.5.3 - #extracting ruby-2.5.3 to /Users/hxer/.rvm/src/ruby-2.5.3 - please wait
ruby-2.5.3 - #configuring - please wait
ruby-2.5.3 - #post-configuration - please wait
ruby-2.5.3 - #compiling - please wait
ruby-2.5.3 - #installing - please wait
ruby-2.5.3 - #making binaries executable - please wait
ruby-2.5.3 - #downloading rubygems-2.7.9
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  842k  100  842k    0     0  1065k      0 --:--:-- --:--:-- --:--:-- 1065k
No checksum for downloaded archive, recording checksum in user configuration.
ruby-2.5.3 - #extracting rubygems-2.7.9 - please wait
ruby-2.5.3 - #removing old rubygems - please wait
$LANG was empty, setting up LANG=en_US.US-ASCII, if it fails again try setting LANG to something sane and try again.
ruby-2.5.3 - #installing rubygems-2.7.9 - please wait
ruby-2.5.3 - #gemset created /Users/hxer/.rvm/gems/ruby-2.5.3@global
ruby-2.5.3 - #importing gemset /Users/hxer/.rvm/gemsets/global.gems - please wait
ruby-2.5.3 - #generating global wrappers - please wait
ruby-2.5.3 - #gemset created /Users/hxer/.rvm/gems/ruby-2.5.3
ruby-2.5.3 - #importing gemsetfile /Users/hxer/.rvm/gemsets/default.gems evaluated to empty gem list
ruby-2.5.3 - #generating default wrappers - please wait
ruby-2.5.3 - #adjusting #shebangs for (gem irb erb ri rdoc testrb rake).
Install of ruby-2.5.3 - #complete
Ruby was built without documentation, to build it run: rvm docs generate-ri
$ ruby -v
ruby 2.5.3p105 (2018-10-18 revision 65156) [x86_64-darwin18]

λ hxer [~] → rvm list
=* ruby-2.5.3 [ x86_64 ]

# => - current
# =* - current && default
#  * - default
$ rvm use 2.5.3
Using /Users/hxer/.rvm/gems/ruby-2.5.3
$ which ruby
/Users/hxer/.rvm/rubies/ruby-2.5.3/bin/ruby
$ gem env
...
$ gem which # 查看安装了哪些gem;
...
$ gem --version
2.7.9
```

参考：[Mac安装Ruby版本管理器RVM](https://www.jianshu.com/p/c44ef74d99f9)、[How to Install Ruby on Mac OS X with RVM](<https://usabilityetc.com/articles/ruby-on-mac-os-x-with-rvm/>) 

#### 1.3 Using Jekyll with Bundler[^2]

```sh
$ bundle --version
Bundler version 1.16.6
$ gem install bundler
Fetching: bundler-2.0.1.gem (100%)
Successfully installed bundler-2.0.1
Parsing documentation for bundler-2.0.1
Installing ri documentation for bundler-2.0.1
Done installing documentation for bundler after 3 seconds
1 gem installed
$ bundler --version
Bundler version 2.0.1
$ cd ~/hxer/Blog
~/hxer/Blog $ bundle init
Writing new Gemfile to /Users/hxer/hxer/Blog/Gemfile
~/hxer/Blog $ cat Gemfile
# frozen_string_literal: true

source "https://rubygems.org"

git_source(:github) {|repo_name| "https://github.com/#{repo_name}" }

# gem "rails" 
~/hxer/Blog $ bundle install --path vendor/bundle
~/hxer/Blog $ ls
Gemfile      Gemfile.lock vendor
~/hxer/Blog $ cat .bundle/config
---
BUNDLE_PATH: "vendor/bundle"
## add jekyll gem to our Gemfile and install it to the ./vendor/bundle/ 
~/hxer/Blog $ bundle add jekyll
注：bundle在请求source: https://rubygems.org/而长时间无响应； 
```

##### 修改`gem`和`bundle`为国内源[^3] 

```sh
## Gem 
$ gem sources --add https://gems.ruby-china.com --remove https://rubygems.org/
## Bundle
$ bundle config 'mirror.https://rubygems.org' 'https://gems.ruby-china.com'
```

> 淘宝的源已经停止更新；且如果Gemfile中source已经为`rubygems.org`，可能还需手动修改`Gemfile.source`.

```sh
$ bundle add jekyll
bundle add jekyll
Fetching gem metadata from https://gems.ruby-china.com/............
Fetching gem metadata from https://gems.ruby-china.com/..
...
Fetching jekyll 3.8.5
Installing jekyll 3.8.5
$ bundle exec jekyll new --force --skip-bundle .
New jekyll site installed in /Users/hxer/hxer/Blog.
Bundle install skipped.
Blog/ $ ls
404.html     Gemfile.lock _posts       index.md
Gemfile      _config.yml  about.md     vendor
Blog/ $ bundle install
The dependency tzinfo-data (>= 0) will be unused by any of the platforms Bundler is installing for. Bundler is installing for ruby but the dependency is only for x86-mingw32, x86-mswin32, x64-mingw32, java. To add those platforms to the bundle, run `bundle lock --add-platform x86-mingw32 x86-mswin32 x64-mingw32 java`.
...
Installing jekyll-feed 0.12.1
Installing jekyll-seo-tag 2.6.0
Installing minima 2.5.0
Bundled gems are installed into `./vendor/bundle`
Blog/ $ bundle lock --add-platform x86-mingw32 x86-mswin32 x64-mingw32 java
Resolving dependencies...
Writing lockfile to /Users/hxer/hxer/Blog/Gemfile.lock
Blog/ $ bundle exec jekyll serve
		...
		 Incremental build: disabled. Enable with --incremental
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```

> 运行jekyll serve命令还在前面加了bundle exec是让bundle运行项目文件夹的Jekyll版本；如果没有使用Gemfile，可直接使用`jekyll serve` build your site.

按照输出提示，访问`http://127.0.0.1:4000`看到Jekyll 默认**minima主题**。

 参考：

* [Jekyll · Quickstart](<https://jekyllrb.com/docs/>) 、[Jekyll · Installation](<https://jekyllrb.com/docs/installation/>) 、[Using Jekyll with Bundler](<https://jekyllrb.com/tutorials/using-jekyll-with-bundler>) 、[Ruby 101](<https://jekyllrb.com/docs/ruby-101/#gems>) 

* [Bundler-Docs](<https://bundler.io/v2.0/gemfile.html>)

* [^1]: https://jekyllrb.com/docs/installation/

* [^2]: https://jekyllrb.com/tutorials/using-jekyll-with-bundler/

* [^3]: https://blog.imst.xyz/archives/210/

### 2. 修改默认主题minima为Minimal Mistake

默认主题`minima`:

```sh
$ bundle show minima
/Users/hxer/hxer/Blog/vendor/bundle/ruby/2.5.0/gems/minima-2.5.0
$ ls vendor/bundle/ruby/2.5.0/gems/minima-2.5.0
LICENSE.txt README.md   _includes   _layouts    _sass       assets
```

选择主题: [**awesome-jekyll-themes**](<https://github.com/planetjekyll/awesome-jekyll-themes>) ，这里选择star数最多的Minimal Mistake[^4].

```sh
$ bundle add "minimal-mistakes-jekyll"
...
Installing minimal-mistakes-jekyll 4.0.1
```

修改`_config.yml`中`theme`为: `theme: minimal-mistakes-jekyll`.使用`bundle update`更新主题。

```sh
$ bundle exec jekyll serve
...
Build Warning: Layout 'post' requested in _posts/2019-04-25-welcome-to-jekyll.markdown does not exist.
     Build Warning: Layout 'page' requested in about.md does not exist.
```



[^4]: <https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/>

#### 3. TO-DO List

- [ ] 将`jekyll-paginate`更换成[jekeyll-paginate-v](<https://github.com/sverrirs/jekyll-paginate-v2>)；

- [ ] 设置scrollspy TOC:

  方法有：将`gem "minimal-mistakes-jekyll", "~> 4.0"`更换成` gem 'minimal-mistakes-jekyll', :git => 'https://github.com/mmistakes/minimal-mistakes.git', :branch => 'smooth-scroll-gumshoe'`，不知道container为何不直接merge到master branch中；

  搜索：scrollspy apply to the TOC in minimal mistake theme。