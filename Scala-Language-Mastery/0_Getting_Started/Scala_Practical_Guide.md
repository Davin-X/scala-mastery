> Migrated from Davin-X/tech-notes@a1e8fb480b45d6e7f32735f69337c10be32f04a9 (scala/scala_practical_guide.md) — preserved as a getting-started reference.

# Scala Practical Guide

**Essential Scala for functional programming & JVM development**

---

## 1. Variables & Types

```scala
// Immutable (preferred)
val name: String = "Alice"
val age: Int = 25
val pi: Double = 3.14159
val isActive: Boolean = true

// Mutable (use sparingly)
var counter: Int = 0
counter = 1  // Can be reassigned

// Type inference
val message = "Hello"        // Inferred as String
val number = 42              // Inferred as Int

println(s"$name is $age years old")
```

## 2. Collections

```scala
// Lists (immutable)
val numbers: List[Int] = List(1, 2, 3, 4, 5)
val fruits: List[String] = List("apple", "banana", "cherry")

// Common operations
println(numbers.head)        // 1
println(numbers.tail)        // List(2, 3, 4, 5)
println(numbers.length)      // 5
println(fruits.mkString(", "))  // apple, banana, cherry

// Add elements (returns new list)
val moreNumbers = numbers :+ 6    // Add to end
val evenMore = 0 +: numbers       // Add to beginning

// Arrays (mutable)
val array = Array(1, 2, 3, 4, 5)
array(0) = 10  // Arrays are mutable

// Maps
val ages: Map[String, Int] = Map(
  "Alice" -> 25,
  "Bob" -> 30,
  "Charlie" -> 35
)

println(ages("Alice"))      // 25
println(ages.contains("Bob")) // true

// Sets
val uniqueNumbers: Set[Int] = Set(1, 2, 2, 3)  // Results in Set(1, 2, 3)
```

## 3. Control Structures

```scala
// If expressions (return values)
val age = 20
val category = if (age < 18) "minor"
               else if (age < 65) "adult"
               else "senior"

// For comprehensions
for (i <- 1 to 3) {
  println(s"Count: $i")
}

val fruits = List("apple", "banana", "cherry")
for (fruit <- fruits) {
  println(fruit)
}

// With guards
val numbers = List(1, 2, 3, 4, 5, 6)
for (num <- numbers if num % 2 == 0) {
  println(s"Even: $num")
}

// While loops
var count = 0
while (count < 3) {
  println(s"While count: $count")
  count += 1
}

// Pattern matching
val day = "Monday"
val dayType = day match {
  case "Monday" | "Tuesday" | "Wednesday" | "Thursday" | "Friday" => "Weekday"
  case "Saturday" | "Sunday" => "Weekend"
  case _ => "Unknown"
}

println(s"$day is a $dayType")
```

## 4. Functions

```scala
// Method definition
def add(a: Int, b: Int): Int = {
  a + b
}

def greet(name: String = "World", age: Int = 0): String = {
  s"Hello, $name! You are $age years old."
}

// Higher-order functions
def applyTwice(f: Int => Int, x: Int): Int = {
  f(f(x))
}

def increment(x: Int): Int = x + 1

println(applyTwice(increment, 5))  // 7

// Anonymous functions
val square = (x: Int) => x * x
val isEven = (x: Int) => x % 2 == 0

println(square(4))        // 16
println(isEven(4))        // true
println(isEven(5))        // false
```

## 5. Classes & OOP

```scala
// Simple class
class Person(val name: String, val age: Int) {
  def greet(): String = s"Hello, I'm $name"

  def isAdult: Boolean = age >= 18
}

// Object creation and usage
val alice = new Person("Alice", 25)
println(alice.greet())        // Hello, I'm Alice
println(alice.isAdult)        // true

// Case classes (immutable with automatic methods)
case class Point(x: Int, y: Int) {
  def distanceFromOrigin: Double =
    math.sqrt(x*x + y*y)
}

val point = Point(3, 4)
println(point.distanceFromOrigin)  // 5.0
println(point)                     // Point(3,4)

// Objects (singletons)
object MathUtils {
  def square(x: Int): Int = x * x
  def cube(x: Int): Int = x * x * x
  val PI = 3.14159
}

println(MathUtils.square(4))  // 16
println(MathUtils.PI)         // 3.14159
```

## 6. Inheritance & Traits

```scala
// Base class
class Animal(val name: String) {
  def makeSound(): String = "Some sound"
  def eat(): Unit = println(s"$name is eating")
}

// Inheritance
class Dog(name: String, val breed: String) extends Animal(name) {
  override def makeSound(): String = "Woof!"

  def fetch(): Unit = println(s"$name is fetching")
}

// Traits (mixins)
trait CanFly {
  def fly(): String = "Flying high!"
}

trait CanSwim {
  def swim(): String = "Swimming fast!"
}

class Duck extends Animal("Donald") with CanFly with CanSwim {
  override def makeSound(): String = "Quack!"
}

val duck = new Duck()
println(duck.makeSound())  // Quack!
println(duck.fly())        // Flying high!
println(duck.swim())       // Swimming fast!
```

## 7. Collections Operations

```scala
val numbers = List(1, 2, 3, 4, 5)

// Map (transform each element)
val squares = numbers.map(x => x * x)      // List(1, 4, 9, 16, 25)

// Filter (select elements)
val evens = numbers.filter(x => x % 2 == 0) // List(2, 4)

// Reduce (combine elements)
val sum = numbers.reduce((a, b) => a + b)  // 15
val sum2 = numbers.sum                      // 15

// Find
val firstEven = numbers.find(x => x % 2 == 0)  // Some(2)
val hasThree = numbers.contains(3)            // true

// Grouping
val words = List("apple", "banana", "cherry", "blueberry")
val byLength = words.groupBy(word => word.length)
// Map(5 -> List(apple), 6 -> List(banana, cherry), 10 -> List(blueberry))

// FlatMap (map + flatten)
val nested = List(List(1, 2), List(3, 4))
val flattened = nested.flatMap(x => x)  // List(1, 2, 3, 4)
```

---

## Quick Reference

**Variable Declaration:**
- `val x: Type = value` - Immutable
- `var x: Type = value` - Mutable
- `val x = value` - Type inferred

**Functions:**
- `def funcName(params): ReturnType = { body }`
- Default params: `def func(x: Int = 0) = x`
- Anonymous: `(x: Int) => x * 2`

**Collections:**
- `List(1, 2, 3)` - Immutable ordered collection
- `Array(1, 2, 3)` - Mutable fixed-size array
- `Set(1, 2, 3)` - Unique elements
- `Map(key -> value)` - Key-value pairs

**Classes:**
- `class ClassName(params) { body }`
- `case class Point(x: Int, y: Int)` - Immutable with auto methods
- `object ObjectName { body }` - Singleton

**Common Operators:**
- `::` - Prepend to list
- `:+` - Append to list
- `++` - Concatenate collections
- `==` - Structural equality
- `match` - Pattern matching
