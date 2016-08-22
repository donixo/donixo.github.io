
When trying to install `github-pages` on Fedora 24 page, I got installation error message:


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

After searching on Internet, most of them said to install following dependencies using `dnf`:


```
$ sudo dnf update
$ sudo dnf install rpm-build zlib-devel
```

When done, try running gem install `github-pages` once again:

```
$ sudo gem install github-pages
```

and done, back to my coffee :D
