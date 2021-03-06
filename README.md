# ErRuby - an implementation of the Ruby language on Erlang
[![Build Status](https://travis-ci.org/johnlinvc/erruby.svg?branch=develop)](https://travis-ci.org/johnlinvc/erruby)
## About

ErRuby is an implementation of the Ruby language using Erlang.

It aims to bring some concurrency features to ruby by experimenting.

It's still a work in progress. So use it at your own risk.

## Install

### Prerequisites
 
- erlang vm
- rebar2
- ruby (2.3.1)

To install erlang & rebar on OS X, using homebrew

	brew install erlang rebar

### Building

After getting the source of ErRuby, get the gems for parser with bundler using:
	
	bundle install
	
 
Then get the deps of erlang modules by using:

	rebar get-deps
	
Last, compile ErRuby with:

	rebar compile
	
	
Test the build result with:

	./test.rb
	
It should output `everything pass`


## Goals

- Concurrent Features.
- Run mspec.
- GC.
- Friendly installation with rvm/rbenv

## Supported features

Currently it support some of the basic ruby constructs.

Supported features:

- `method` definition & calling.
- singleton methods, class methods.
- `class` and inheritance.
- `block` and `yield`.
- Constants.
- Local variables.
- Instance variables.
- `load` & `require_relative`.
- `Boolean` & `Integer` with basic methods.
- `String` literal.
- `Array` literal.

Unsupported core features

- class initializer, class instance variables.
- `module` definition, `include`, `extend`.
- variadic argument in function.
- keyword argument in function.
- GC.

### Class & inherentance
```ruby
class Foo
  def to_s
    "foo"
  end
end

class Bar < Foo
end

class Alice < Bar
  def to_s
    "i'm alice"
  end
  def self.name
    "Alice"
  end
end

puts Foo.new.to_s # "foo"
puts Bar.new.to_s # "foo"
puts Alice.new.to_s # "i'm alice"
puts Alice.name # "Alice"
```

### block
```ruby
def yield_with_arg(s,x)
  yield s,x
end

yield_with_arg("yield with","arg") do |ss, xx|
  puts ss # "yield with"
  puts xx # "arg"
end

3.times do |i|
  puts i.to_s
  4.times do |j|
    puts j.to_s
  end
end

([1,2,3]*1000).pmap do |x|
  x+1
end


```


## License

ErRuby is licensed to you under MIT license. See the [COPYING.txt](COPYING.txt) file for more details.
