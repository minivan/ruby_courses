# Lesson 4. Classes & Objects

## Recall what classes are.

A _class_ is a blueprint for objects. You only have one class called `Car`, but with it you can create multiple _instances_ of cars (car _objects_), all of which have the methods and attributes defined by the `Car` class.

An _object_ is an _instance_ of a class. If `Car` is the class, then `x = Car.new` creates a new Car instance and assigns the object to the variable `x`. You would then say x is a `car` object, or an object of class `Car`.

Class declaration in Ruby:

    class Car
      ...
    end

Object instantiation in Ruby:

    my_porsche = Car.new

## Variable scope

+ In order to detect the scope, use the `Object.defined?` method as follows:
    a = 5
    defined? a   # => "local-variable"
+ Local variables: `name`
+ Global variables: `$name`
+ Instance variables: `@name`
+ Class variables: `@@name`

## The `initialize` method

    class Person
      def initialize(name)
        @name = name
      end

      def say_hello
        puts "Hello, #{@name}"
      end
    end

    v = Person.new("Vasea")

_food for thought: What would happen if we write_ `v = Person.new(4)`? _How can we get_ `@name` _to be_ `nil`?

## Instance methods and Class methods

    class Person
      def self.gets_old_at(sex)
        if sex == :male
          65
        else
          70
        end
      end
    end

    Person.gets_old_at(:male)   # => 65

**Homework Excercise:**
Create an instance method that would count the number of instances of a class. For example:

    Person.count                # => 0
    a = Person.new("Galina")
    Person.count                # => 1
    b = Person.new("Olga")
    Person.count                # => 2

## Private methods

    class Example
      def a_public_method
      end
   
      private
   
      def a_private_method
      end
    end

## Default parameters

    class Person
      def initialize(name = "Vasea Pupkin", age = 100)
        ...
      end
    end

## Variabe number of arguments

    def example (first, *test)
      puts "The number of parameters is #{test.length}"
      for i in 0...test.length
        puts "The parameters are #{test[i]}"
      end
      puts "The first one was #{first}"
    end

## Today's exercise
