# about self

Everything in Ruby is an object. If that's true it means that every piece of code you write "belongs" to some object.

**self** is a special variable that points to the object that "owns" the currently executing code. Ruby uses self everwhere:

* For instance variables: @myvar
* For method and constant lookup
* When defining methods, classes and modules.

In theory, self is pretty obvious. But in practice, it's easy for tricky situations to pop up. That's why I wrote this post.


# Examples of self

```
class Player
  class << self 
    def method1
    end

    def method2
    end
  end
end
```

```
class MyClass
  def do_work
    water = "variable"
    puts water
    puts self.water
  end
  def water
    "method"
  end
end
```

MyClass.new.do_work
## "variable"  => puts water
## "method"    => puts self.water
