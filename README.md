rchardet
========

rchardet is an encoding auto-detection library in Ruby. This library is a port of the auto-detection code in Mozilla. It means taking a sequence of bytes in an unknown character encoding, and attempting to determine the encoding so you can read the text. It’s like cracking a code when you don’t have the decryption key.

This fork is compatible with ruby 1.9, and runs in production at [webtranslateit.com](https://webtranslateit.com). Here’s an [introductory blog post to our encoding detection strategy](http://blog.webtranslateit.com/post/6380685137).

Usage
-----

```ruby
require 'rubygems'
require 'rchardet'

cd = CharDet.detect(some_data)
encoding = cd['encoding']
confidence = cd['confidence'] # 0.0 <= confidence <= 1.0
```

Running tests
-------------

    ruby spec/all.rb
