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

## Inheritance

    class Sedan < Car
    end

The `super` method:

    class Person
      def initialize(name)
        @name = name
      end
      def name
        return @name
      end
    end

    class Doctor < Person
      def name
        "Dr. " + super
      end
    end

Overriding existing methods:

    class String
      def length
        20
      end
    end

## Polymorphism

    class Animal
      def initialize(name)
        puts name
      end
    end

    class Cat < Animal
      def talk
        "Meaow!"
      end
    end

    class Dog < Animal
      def talk
        "Woof!"
      end
    end

    animals = [Cat.new("Boris"), Dog.new("Tuzik"), Cat.new("KOT")]
    animals.each do |animal|
    puts animal.talk
    end

_note: the_ `talk` _method is called on the child class!_

Ruby uses the concept of **duck typing**. It is defined as follows:
> When I see a bird that walks like a duck and swims like a duck and quacks like a duck, I call that bird a duck.

## `attr` methods
    
    class Dog
      attr :bark, true
    end

    Dog.instance_methods - Object.instance_methods # => ["bark", "bark="]
    
Repeat the example using `attr_reader`, `attr_writer` and `attr_accessor`. When to use which?

## Modules

    module UsefulFeatures
      def class_name
        self.class.to_s
      end
    end
    
    class Person
      include UsefulFeatures
    end

    x = Person.new
    puts x.class_name

**`Enumerable`**, **`Comparable`** are all Ruby modules. The `each` iterator is defined on something that is `Enumerable`.
It takes a block as an argument, so wo can redefine it as follows:

    class RubyCourse
      include Enumerable
      attr_accessor :students

      def each
        @students.select{ |s| s.is_a_good_student? }.each{ |s| yield s }
      end
    end

Then you'll be able to use a lot of methods from `Enumerable` on an instance of `RubyCourse`

**Homework exercise:** Create a similar working example with Modules. Use `respond_to?` to see which of the methods from `Enumerable` does your new class respond to.
