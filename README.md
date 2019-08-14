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
 * Top level code also runs within an Object
 ```ruby
 def foo
  puts "bar"
end

puts "My awesome #{foo} app!"
 ```
 What ruby interpreter does is that it evaluates the code within the context of Object class instance.

 ```ruby
puts self         => # main
puts self.class   => # Object
 ```
 So we can assume that ruby code is evaluated within an Object class
 
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

### Runnable code
Ruby class definitions are just runnable code. It means that you can have logical expressions, other class declarations or method within your class declaration code.

look at this java class definition
``` java
class MyClass {
  private string MyProperty;
  public string  myMethod() {
    return myProperty;
  }
}
```
Now look at ruby class definition, You can run whatever code you want in the class

```ruby 
class MyClass
  puts "Code running inside this class"

  2.times { puts "what" }

  def foo
    "bar"
  end

end
```
This code is valid ruby code.

### Classes are objects.
Classes in ruby are objects. In other words, instances of Class class.

We'll take a look at these points

* Eigenclass
* Singleton class
* Classes are objects themselves

```ruby
class MyClass
end

a = MyClass.new
puts a.class        # MyClass
puts MyClass.class  # Class  
```

```ruby
MyClass = Class.new
MyClass.name       # MyCLass
MyClass.class      # Class

a = MyClass.new
a.class            # MyClass
```

We are initializing a new instance of Class class and assigning it to our constant MyClass.
Ruby interpreter then creates a new class with constant name MyClass.

```ruby
foo = Class.new
foo.name          # nil
foo.class         # Class

Bar = foo
foo.name          # Bar
```
As you can see, you can assign an instance of Class class to any constant (Const = Class.new) and Ruby will treat it as if you were creating a class with that constant name (class Const; end)

```ruby
class MyClass; end
foo = MyClass.new
```

In the above code, foo is an instance of MyClass.
MyClass is a constant that holds an instance of Class class.
This means, foo is an instance of an instance of Class class.

Class's class is called Eigenclass or Singleton class.

Q. How can we access class' class (eigenclass) ?
```ruby
class MyClass
  class << self
    def class_method
      #eigenclass
    end
  end

  def self.class_method2
    #alternative method
  end

  def MyClass.class_method
    # Another alternative
  end
end
```