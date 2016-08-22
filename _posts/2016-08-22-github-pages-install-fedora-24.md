---
layout: post
title:  "github-pages installation on Fedora 24"
date:   2016-08-22 07:32 +0700
categories:ruby jekyll fedora24 
---

Since I'm trying to setup jekyl on my new linux box, 
When trying to install `github-pages` on Fedora 24 page, I got following installation error message:


```
...

Provided configuration options:
--with-opt-dir
--without-opt-dir
--with-opt-include
--without-opt-include=${opt-dir}/include
--with-opt-lib
--without-opt-lib=${opt-dir}/lib64
--with-make-prog
--without-make-prog
--srcdir=.
--curdir
--ruby=/usr/bin/$(RUBY_BASE_NAME)
--with-rtlib
--without-rtlib
/usr/share/ruby/mkmf.rb:456:in `try_do': The compiler failed to generate an executable file. (RuntimeError)
You have to install development tools first.`

...

```

After searching on Internet[1] , most of them said to install dependencies below using `dnf`:


```
$ sudo dnf update
$ sudo dnf install rpm-build zlib-devel
```

`zlib-devel` needed because nokogiri package need a zlib header, so I add that one after `rpm-build`.


When done, try running gem install `github-pages` once again:

```
$ sudo gem install github-pages
```

and done, back to my coffee :D


[1] https://github.com/copiousfreetime/hitimes/issues/54#issuecomment-154829452

