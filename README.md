# Kotlin_Docs
Learn Kotlin from basic to advanced

**Package definition and imports**
- Package specification should be at the top of the source file.
```
package my.demo
import kotlin.text.*
```

- It is not required to match directories and packages: source files can be placed arbitrarily in the file system.

<details>
<summary><font size="5">Variable</font></summary>

- Read-only local variables are defined using the keyword val. They can be assigned a value only once

``` 
val a: Int = 1  // immediate assignment
val b = 2   // `Int` type is inferred
val c: Int  // Type required when no initializer is provided
c = 3       // deferred assignment
```

- Variables that can be reassigned use the var keyword.

```
var x = 5 // `Int` type is inferred
x += 1
```
</details>



<details>
<summary><font size="5">Data Type</font></summary>

1. Numbers

![Screen Shot 2022-11-25 at 09 29 38](https://user-images.githubusercontent.com/67398186/203888441-6c3c5da5-37e2-4d18-a383-dca46ced8367.png)

```
val one = 1 // Int
val threeBillion = 3000000000 // Long
val oneLong = 1L // Long
val oneByte: Byte = 1
```

![Screen Shot 2022-11-25 at 09 45 30](https://user-images.githubusercontent.com/67398186/203890043-1178c426-ff89-4589-acf5-64f909682290.png)

- You can use underscores to make number constants more readable:
```
val oneMillion = 1_000_000
val creditCardNumber = 1234_5678_9012_3456L
val socialSecurityNumber = 999_99_9999L
val hexBytes = 0xFF_EC_DE_5E
val bytes = 0b11010010_01101001_10010100_10010010
```
- All number types support conversions to other types:
```
toByte(): Byte
toShort(): Short
toInt(): Int
toLong(): Long
toFloat(): Float
toDouble(): Double
```
2. Boolean
```
val myTrue: Boolean = true
val myFalse: Boolean = false
val boolNull: Boolean? = null
println(myTrue || myFalse)
println(myTrue && myFalse)
println(!myTrue)
true
false
false
```
3. Characters
```
val aChar: Char = 'a'
println(aChar)
println('\n') // Prints an extra newline character
println('\uFF00')
```

4. Strings
* Strings in Kotlin are represented by the type String. Generally, a string value is a sequence of characters in double quotes ("):
```
val str = "abcd 123"
```
* String templates
```
val i = 10
println("i = $i") // Prints "i = 10"
```

5. Arrays
* Arrays in Kotlin are represented by the Array class
```
// Creates an Array<String> with values ["0", "1", "4", "9", "16"]
val asc = Array(5) { i -> (i * i).toString() }
asc.forEach { println(it) }

To create an array, use the function arrayOf() and pass the item values to it, so that arrayOf(1, 2, 3) creates an array [1, 2, 3]
```
* Primitive type arrays: Kotlin also has classes that represent arrays of primitive types without boxing overhead: ByteArray, ShortArray, IntArray
```
val x: IntArray = intArrayOf(1, 2, 3)
x[0] = x[1] + x[2]

// Array of int of size 5 with values [0, 0, 0, 0, 0]
val arr = IntArray(5)

// Example of initializing the values in the array with a constant
// Array of int of size 5 with values [42, 42, 42, 42, 42]
val arr = IntArray(5) { 42 }

// Example of initializing the values in the array using a lambda
// Array of int of size 5 with values [0, 1, 2, 3, 4] (values initialized to their index value)
var arr = IntArray(5) { it * 1 }
```
6. Type checks and casts
***is and !is operators***
- Use the is operator or its negated form !is to perform a runtime check that identifies whether an object conforms to a given type:
```
if (obj is String) {
    print(obj.length)
}

if (obj !is String) { // same as !(obj is String)
    print("Not a String")
} else {
    print(obj.length)
}

```
- Smart casts work for when expressions and while loops as well:
```

when (x) {
    is Int -> print(x + 1)
    is String -> print(x.length + 1)
    is IntArray -> print(x.sum())
}
```
</details>


<details>
<summary><font size="5">Control flow (if else, condition, loop...)</font></summary>

**Conditions and loops**

- If expression: In Kotlin, if is an expression: it returns a value. Therefore, there is no ternary operator (condition ? then : else) 
```
val max = if (a > b) a else b
```

- When expression: it is similar to the switch statement in C-like languages
```
when (x) {
    1 -> print("x == 1")
    2 -> print("x == 2")
    else -> {
        print("x is neither 1 nor 2")
    }
}
```

- For loops: 
```
for (item in collection) print(item)
for (i in 1..3) {
    println(i)
}
for (i in 6 downTo 0 step 2) {
    println(i)
}
```

- While loops: while and do-while
```
while (x > 0) {
    x--
}
do {
    val y = retrieveData()
} while (y != null) // y is visible here!
```
**Break and continue labels**

```
break for first
loop@ for (i in 1..100) {
    for (j in 1..100) {
        if (j=2) break@loop
    }
}

break for second
loop@ for (i in 1..10) {
   loop1@  for (j in 1..100) {
        if (j==2) break@loop1
        else
        println("hihi")
    }
}
```
</details>


<details>
<summary><font size="5">Null safety</font></summary>

**Nullable types and non-null types**
```
var a: String = "abc" // Regular initialization means non-null by default
a = null // compilation error

To allow nulls, you can declare a variable as a nullable string by writing String?:
var b: String? = "abc" // can be set to null
b = null // ok
print(b)
```
**Checking for null in conditions**
```
val b: String? = "Kotlin"
if (b != null && b.length > 0) {
    print("String of length ${b.length}")
} else {
    print("Empty string")
}
```
**Safe calls**
```
val a = "Kotlin"
val b: String? = null
println(b?.length)
println(a?.length) // Unnecessary safe call
```

**Elvis operator**
- When you have a nullable reference, b, you can say "if b is not null, use it, otherwise use some non-null value":
```
val l: Int = if (b != null) b.length else -1
```

- Instead of writing the complete if expression, you can also express this with the Elvis operator `?:`
```
val l = b?.length ?: -1
```

**The !! operator**
- the not-null assertion operator (!!) converts any value to a non-null type and throws an exception if the value is null
```
val l = b!!.length
```

**Safe casts**
```
val aInt: Int? = a as? Int
```
**Collections of a nullable type**
- If you have a collection of elements of a nullable type and want to filter non-null elements, you can do so by using filterNotNull
```
val nullableList: List<Int?> = listOf(1, 2, null, 4)
val intList: List<Int> = nullableList.filterNotNull()
```

</details>



<details>
<summary><font size="5">Classes and objects</font></summary>


## Classes
- To define a class, use the `class` keyword.
```
class Shape
```

- Properties of a class can be listed in its declaration or body.
```
class Rectangle(var height: Double, var length: Double) {
    var perimeter = (height + length) * 2
}
```

**Constructors**
- A class in Kotlin can have a primary constructor and one or more secondary constructors. The primary constructor is a part of the class header, and it goes after the class name and optional type parameters
```
class Person constructor(firstName: String) { /*...*/ }
```
- The primary constructor cannot contain any code. Initialization code can be placed in initializer blocks prefixed with the init keyword.
```
class InitOrderDemo(name: String) {
    val firstProperty = "First property: $name".also(::println)
    
    // after class create througth primary constructor
    init {
        println("First initializer block that prints $name")
    }
    
    val secondProperty = "Second property: ${name.length}".also(::println)
    
    init {
        println("Second initializer block that prints ${name.length}")
    }
}

```
- Kotlin has a concise syntax for declaring properties and initializing them from the primary constructor

```
class Person(val firstName: String, val lastName: String, var age: Int)
```
**Creating instances of classes**
```
class User(name:String)
val user = User("kyle")
```
**Class members**
- Classes can contain:
1.Constructors and initializer blocks
2.Functions
3.Properties
4.Nested and inner classes
5.Object declarations

**Abstract classes**
- A class may be declared abstract, along with some or all of its members. An abstract member does not have an implementation in its class. You don't need to annotate abstract classes or functions with open.
```
abstract class Polygon {
    abstract fun draw()
}

class Rectangle : Polygon() {
    override fun draw() {
        // draw the rectangle
    }
}

```

## Inheritance
- All classes in Kotlin have a common superclass, Any, which is the default superclass for a class with no supertypes declared
```
class Example // Implicitly inherits from Any
```
- `Any` has three methods: `equals()`, `hashCode()`, and `toString()`. Thus, these methods are defined for all Kotlin classes.

- By default, Kotlin classes are final – they can't be inherited. To make a class inheritable, mark it with the `open` keyword:
```
open class Base // Class is open for inheritance
```

```
open class Person(type: String)

class Student(type: String) : Person(type)
```
***Overriding methods***

```
open class Shape {
    open fun draw() { /*...*/ } // need `open` key word
    fun fill() { /*...*/ }
}

class Circle() : Shape() {
    override fun draw() { /*...*/ }
}
```

***Overriding properties***
```
open class Shape {
    open val vertexCount: Int = 0
}

class Rectangle : Shape() {
    override val vertexCount = 4
}
```

***Calling the superclass implementation***
```
open class Rectangle {
    open fun draw() { println("Drawing a rectangle") }
    val borderColor: String get() = "black"
}

class FilledRectangle : Rectangle() {
    override fun draw() {
        super.draw()
        println("Filling the rectangle")
    }

    val fillColor: String get() = super.borderColor
}
```
</details>




<details>
<summary><font size="5">Data classe</font></summary>

-  In Kotlin, these are called data classes and are marked with data: main purpose is to hold data
```
data class User(val name: String, val age: Int)
```

- The compiler automatically derives the following members from all properties declared in the primary constructor:
```
equals()/hashCode() pair
toString() of the form "User(name=John, age=42)"
componentN() functions corresponding to the properties in their order of declaration.
copy() function (see below).
```

- To ensure consistency and meaningful behavior of the generated code, data classes have to fulfill the following requirements:
> The primary constructor needs to have at least one parameter.
> All primary constructor parameters need to be marked as val or var.
> Data classes cannot be abstract, open, sealed, or inner.

***Copying***

- Use the copy() function to copy an object, allowing you to alter some of its properties while keeping the rest unchanged.
```
data class User(val name:String,val age:Int)
val jack = User(name = "Jack", age = 1)
val olderJack = jack.copy(age=2)
print(olderJack) // User(name=Jack, age=2)
```
***Properties declared in the class body***
```
data class Person(val name: String) {
    var age: Int = 0
}
val person1 = Person("John")
val person2 = Person("John")
person1.age = 10
person2.age = 20
person1 == person2: true
person1 with age 10: Person(name=John)
person2 with age 20: Person(name=John)
```

***Data classes and destructuring declarations***


```
val jane = User("Jane", 35)
val (name, age) = jane
println("$name, $age years of age") // prints "Jane, 35 years of age"
```
[Reference](http://https://kotlinlang.org/docs/destructuring-declarations.html#destructuring-in-lambdas)

### Note
```
data class User(val name:String,val age:Int)
val user1 = User("user", 35)
val user2 = User("user", 35)

println(user1.equals(user2)) // same value
```


</details>















