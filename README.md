# Ruby Metaprogramming :rocket:

### Everything in ruby is an object
* No primitive values
 ```ruby
1.class         => # Fixnum 
(1.5).class     => # Float
true.class      => # TrueClass
 ```
All of the above are instances of a particular class.
That's actually why we can have constructs like this
 ```ruby
  3.times do
    # do something
  end

  class Integer
    def times(&block)
      # for "self" times run block
    end
  end
 ```
 * Top level code also runs within an object
 ```ruby
 def foo
  puts "bar"
end

puts "My awesome #{foo} app!"
 ```
 What ruby interpreter does is that it evaluates the code within the context of object class instance.

 ```ruby
puts self         => # main
puts self.class   => # Object
 ```
 So we can assume that ruby code is evaluated within an object class
 
 * Blocks are not objects
 ---

 ### Open Classes
 You can open any class, even standard classes, and modify them

 ```ruby
  class String
    def foo
      "bar"
    end
  end

  "some string".foo  => "bar"
 ```
any instance of the string class will get this foo method.

We can also overwrite existing methods
```ruby
class Array
  def reverse
    raise "Can't reverse arrays!"
  end
end

["one", "two"].reverse # Runtime Error: Can't reverse arrays!
```
### DuckTyped

Ruby is a ducktyped language. Unlike for statically typed language such as java or C++, Ruby will not throw an error if we pass a instance of Class A to a method that is expecting a instance of class B.

```ruby
def reverse_day(array)
  array.reverse
end

reverse_day([1,2,3])      => [3,2,1]
reverse_day( "hello" )    => "olleh"
reverse_day( 12345 )      => NoMethodError
```
As long as Class A has all the methods that are used in all other methods, there will be no complaints from ruby.
