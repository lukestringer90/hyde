---
layout: post
title: Jekyll on the Apple M1
excerpt_separator: <!--more-->
---

Late last year I bought the 2020 Mac Mini with Apple's new M1 chip. Overall the machine is great, and for iOS development it worked "out of the box" with essentially no hitches. However when I came to update this website I had trouble getting the default Ruby install to work with [Jekyll](https://jekyllrb.com) (static site generator) and [Poole](https://github.com/poole/poole) (layout and other helpers for Jekyll).

Specifically I was getting this sort of error message when running `jekyll serve`:

```
LoadError - dlopen(/Library/Ruby/Gems/2.6.0/gems/ffi-1.13.1/lib/ffi_c.bundle, 0x0009): missing compatible arch in /Library/Ruby/Gems/2.6.0/gems/ffi-1.13.1/lib/ffi_c.bundle
```

After some googling I found that I wasn't the first person to come across similar problems. According to [Martin Albrecht](https://medium.com/better-programming/ruby-on-apple-silicon-m1-macs-fb159849b2f5) the default Ruby install on Big Sur for M1 macs is a bit broken. I don't understand all the ins and outs of the problem but I think I've got a workable solution that you may also find useful.

<!--more-->

After some more googling I came across [a post from Go Rails](https://gorails.com/setup/osx/11.0-big-sur) describing how to setup Ruby (and Rails) on Big Sur. With a few tweaks this guide solved my problem with using Jekyll.

First install homebrew.

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Now install `rbenv` and configure the path.

```
brew install rbenv ruby-build

# Add rbenv to bash so that it loads every time you open a terminal
echo 'if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi' >> ~/.zshrc
source ~/.zshrc
```

Next install Ruby 3.0.0.

```
rbenv install 3.0.0
rbenv global 3.0.0
ruby -v
rbenv rehash
```

You may need to restart your terminal at this point.

Now Ruby is installed you'll want to setup Jekyll and Poole. For some reason my fork of Poole did not come with a Gemfile, so I needed to create one like this:

``` ruby
source "https://rubygems.org"

gem "jekyll"
gem "jekyll-gist"
gem "jekyll-paginate"
gem "jekyll-seo-tag"
gem "jekyll-analytics"
gem "webrick" # make sure to add this as otherwise you'll get webrick error
```

Finally you can now install the gems and run Jekyll.

```
bundle install
bundle exec jekyll serve
```

And voilà, your site should now be generated on your local machine!