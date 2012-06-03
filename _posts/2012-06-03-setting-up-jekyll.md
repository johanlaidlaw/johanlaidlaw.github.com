---
layout: post
title: "Setting up Jekyll"
description: "Setting up Jekyll on Github.com pages"
category: 
tags: [jekyll,github.com]
---
{% include JB/setup %}


I have finally setup my new blog and I thought it would be a good idea to share my experience with setting up Pages and Jekyll on github.com


First thing I did was to follow the instructions on [jekyllbootstrap.com](http://jekyllbootstrap.com/).
I cloned the bootstrap jekyll into my own git repository and pushed it to github.


	$ git clone https://github.com/plusjade/jekyll-bootstrap.git johanlaidlaw.github.com
	$ cd johanlaidlaw.github.com
	$ git remote set-url origin git@github.com:johanlaidlaw/johanlaidlaw.github.com.git
	$ git push origin master


After a few minutes I got an email from github:

*Your page has been built. If this is the first time you've pushed, it may take a few minutes to appear, otherwise your changes should appear immediately.*


I could now see my page live on [johanlaidlaw.github.com](johanlaidlaw.github.com)

I then configured the site by changing the `_config.yml`.

Everytime I changed something, I pushed the changes to github and got a new email, saying that the page has been built succesfully. After a few times pushing I got quite annoyed with this and realized I would need to install Jekyll on my machine.

	$ sudo gem install jekyll

But it was throwing this error:

	Building native extensions.  This could take a while...
	ERROR:  Error installing jekyll:
		ERROR: Failed to build gem native extension.

	        /Users/johanlaidlaw/.rvm/rubies/ruby-1.9.2-p290/bin/ruby extconf.rb
	creating Makefile

	make
	/usr/bin/gcc-4.2 -I. -I/Users/johanlaidlaw/.rvm/rubies/ruby-1.9.2-p290/include/ruby-1.9.1/x86_64-darwin10.8.0 -I/Users/johanlaidlaw/.rvm/rubies/ruby-1.9.2-p290/include/ruby-1.9.1/ruby/backward -I/Users/johanlaidlaw/.rvm/rubies/ruby-1.9.2-p290/include/ruby-1.9.1 -I. -D_XOPEN_SOURCE -D_DARWIN_C_SOURCE   -fno-common -O3 -ggdb -Wextra -Wno-unused-parameter -Wno-parentheses -Wpointer-arith -Wwrite-strings -Wno-missing-field-initializers -Wshorten-64-to-32 -Wno-long-long  -fno-common -pipe  -o porter.o -c porter.c
	make: /usr/bin/gcc-4.2: No such file or directory
	make: *** [porter.o] Error 1


	Gem files will remain installed in /Users/johanlaidlaw/.rvm/rubies/ruby-1.9.2-p290/lib/ruby/gems/1.9.1/gems/fast-stemmer-1.0.1 for inspection.
	Results logged to /Users/johanlaidlaw/.rvm/rubies/ruby-1.9.2-p290/lib/ruby/gems/1.9.1/gems/fast-stemmer-1.0.1/ext/gem_make.out


I knew I had Xcode installed so I tried to reinstall it. That didn't help. gcc-4.2 was installed but it looked like it was placed in the wrong directory.
	
	$ which gcc-4.2 
	=> /Developer/usr/bin/gcc-4.2

So I thought I could create a symlink in the /usr/bin directory.
	
	$ sudo ln -s /Developer/usr/bin/gcc-4.2 /usr/bin/gcc-4.2


But now I got another error message

	Building native extensions.  This could take a while...
	ERROR:  Error installing jekyll:
		ERROR: Failed to build gem native extension.

	        /Users/johanlaidlaw/.rvm/rubies/ruby-1.9.2-p290/bin/ruby extconf.rb
	creating Makefile

	make
	/usr/bin/gcc-4.2 -I. -I/Users/johanlaidlaw/.rvm/rubies/ruby-1.9.2-p290/include/ruby-1.9.1/x86_64-darwin10.8.0 -I/Users/johanlaidlaw/.rvm/rubies/ruby-1.9.2-p290/include/ruby-1.9.1/ruby/backward -I/Users/johanlaidlaw/.rvm/rubies/ruby-1.9.2-p290/include/ruby-1.9.1 -I. -D_XOPEN_SOURCE -D_DARWIN_C_SOURCE   -fno-common -O3 -ggdb -Wextra -Wno-unused-parameter -Wno-parentheses -Wpointer-arith -Wwrite-strings -Wno-missing-field-initializers -Wshorten-64-to-32 -Wno-long-long  -fno-common -pipe  -o porter.o -c porter.c
	porter.c:31:44: error: stdlib.h: No such file or directory
	porter.c:32:47: error: string.h: No such file or directory
	porter.c: In function ‘create_stemmer’:
	porter.c:85: warning: incompatible implicit declaration of built-in function ‘malloc’
	.....
	.....

After some googling a downloaded the OSX GCC installer from [https://github.com/kennethreitz/osx-gcc-installer](https://github.com/kennethreitz/osx-gcc-installer), installed it and then it could find gcc

Then I could start the Jekyll server and develop the pages without pushing to Github. Jekyll starts the server on port 4000.
	
	$ cd /Sites/johanlaidlaw.github.com
	$ sudo jekyll --server


I would recommend going through the [Jekyll quick start](http://jekyllbootstrap.com/usage/jekyll-quick-start.html) and learn the [Markdown syntax](http://daringfireball.net/projects/markdown/syntax)


