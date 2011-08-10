rchardet
========

rchardet is an encoding auto-detection library in Ruby. This library is a port of the auto-detection code in Mozilla. It means taking a sequence of bytes in an unknown character encoding, and attempting to determine the encoding so you can read the text. It’s like cracking a code when you don’t have the decryption key.

This fork is compatible with ruby 1.9, and runs in production at [webtranslateit.com](https://webtranslateit.com).

Usage
-----

```ruby
require 'rubygems'
require 'rchardet'

cd = CharDet.detect(some_data)
encoding = cd['encoding']
confidence = cd['confidence'] # 0.0 <= confidence <= 1.0
```

Encoding Detection Strategy
---------------------------

rchardet isn’t a very reliable tool to determine a file encoding and should be used as the last resort. There are plenty of ways to detect a file’s encoding before having to use rchardet. For instance, by reading and detecting the  [BOM](http://en.wikipedia.org/wiki/Byte_order_mark), or by looking for hints in the text you’re working on (for instance, don’t headers or footers have `charset="utf-8` somewhere?

You can read an [introductory blog post to our encoding detection strategy](http://blog.webtranslateit.com/post/6380685137).

I suggest you open your file to detect in `ASCII-8BIT`.

``` ruby
file_content = open(self.file_path, external_encoding: 'ASCII-8BIT') { |f| f.read }
encoding = CharDet.detect(file_content)
```

You don’t know what’s your file’s encoding just yet, so in which encoding will you open your file? Ruby defines the encoding `ASCII-8BIT`, with an alias of `BINARY`, which does not correspond to any known encoding. It is intended to be associated with binary data or for text of unknown encoding.

Once you’ve detected the encoding you can then convert it:

``` ruby
converter = Encoding::Converter.new(encoding[:encoding].name.upcase, "UTF-8")
converter.convert(file_content)
```

Running tests
-------------

    ruby spec/all.rb
