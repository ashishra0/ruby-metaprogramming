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