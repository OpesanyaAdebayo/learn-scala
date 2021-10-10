# learn-scala
My Scala journey in a repo. I'm learning with the [Scala Book](https://docs.scala-lang.org/overviews/scala-book/introduction.html).

## Hello World
- `scalac <scala_file_path>.scala` compiles code in a file.
- `scala <class_name>` runs the compiled application.
- `scalac` creates tow _.class_ files which are JVM bytecode files; same as those you get from running `javac` if you're writing Java.

## Variables and Built-in Types
- Scala has two types of variables. `val` creates an _immutable_ variable, while `var` creates a _mutable_ variable.

```scala
val s = "hello"   // immutable
var i = 42        // mutable

val p: String  = "hello"
val n: Int = 3
```
- Variables data type can be infered, so it's not compulsory to have the data type in the declaration.
- `Int` and `Double` are default data types for numbers. You have to be specific if you want the others: `Byte`, `Long`, `Short` and `Float`.

```scala
val b: Byte = 1
val x: Int = 1
val l: Long = 1
val s: Short = 1
val d: Double = 2.0
val f: Float = 3.0
```

- For large numbers Scala allows `BigInt` and `BigDecimal`, and they support normal arithmetic operators

```scala
var b = BigInt(1234567890)
var b = BigDecimal(123456.789)
```

- Other data types are `String` and `Char`. Double quotes are used for `String`s while single quotes are used for `Char`s

```scala
val name: String = "Bill"
val c: Char = 'a'
```

- You can concatenate strings using the `+` operator or string interpolation.

```scala
val firsName = "Bayo"
val lastName = "John"

val stringInterpolation = s"$firstName $lastName"
val plusOperator = firstName + lastName
```

- You can create a multiline string by putting th string in triple quotes. To avoid the the text being indented, put a `|` symbol at the start of each new line and call the `stripMargin` method.
```scala
val text = """There is a man
              |Who lived in the jungle
              |But had no food """.stripMaargin

```

## Command-line I/O
- You can use `println` to write to STDOUT. If you don't want a new line after,  use `print`. You can also write to STDERR with `System.err.println`.

```scala
println("Hello, world")

System.err.println("yikes, an error happened")

```
- You can use the `readLine` method to read command-line input but it needs to be imported first. (check `HelloInteractive.scala` for example).

## Control Structures
- `if` statements look like this

```scala
if (a == b) doSomething()

// OR 
if (a == b) {
    doSomething()
} else {
    doSomethingElse()
}

// OR
if (a == b) {
    doSomething()
} else if (a < b) {
    doSomethingElse()
} else {
    doThisInstead()
}
```

- For Loops
```scala
// With Sequence. Same thing applies for Lists
val nums = Seq(1,2,3,4)

for (n <- nums) println(n)

// With Maps
val ratings = Map(
     "Lady in the Water"  -> 3.0, 
    "Snakes on a Plane"  -> 4.0, 
    "You, Me and Dupree" -> 3.5
)

for ((name, rating) <- ratings) println(s"Movie: $name, Rating: $rating")

ratings.forEach {
    case(movie, rating) => println(s"key: $movie, value: $rating)
}
```

- For-expressions can be used to create new collections from existing ones.
```scala
val nums = (1,2,3,4,5)
val doubleNums = for (n <- nums) yield n*2
```

- `match` is used like a `switch` statement in other languages.
```scala
// i is an integer
i match {
    case 1  => println("January")
    case 2  => println("February")
    case 3  => println("March")
    case 4  => println("April")
    case 5  => println("May")
    case 6  => println("June")
    case 7  => println("July")
    case 8  => println("August")
    case 9  => println("September")
    case 10 => println("October")
    case 11 => println("November")
    case 12 => println("December")
    // catch the default with a variable so you can print it
    case _  => "Invalid month"
}
```
- A `match` expression can also be used as the body of a method, since it returns a value.
```scala
def convertBooleanToString(bool: Boolean): String = bool match {
    case true => "you said true"
    case false => "you said false"
}
```

- You can also handle multiple cases in one `case` statement
```scala
def isTrue(a: Any) = a match {
    case 0 | "" => flasme
    case _ => true
}

val evenOrOdd = i match {
    case 1 | 3 | 5 | 7 | 9 => println("odd")
    case 2 | 4 | 6 | 8 | 10 => println("even")
    case _ => println("some other number")
}
```

- You can also use `if` expressions in `case` statements.
```scala
count match {
    case 1 =>
        println("one is a lonely number")
    case x if (x == 2 || x == 3) =>
        println("two is company, three is a crowd")
    case x if (x > 3) =>
        println("4+, that's a party")
    case _ => println("i'm guessing your number is zero or less")
}
```
- try/catch/finally
```scala
var text = ""
try {
    text = openAndReadAFile(filename)
} catch {
    case e: FileNotFoundException => println("Couldn't find that file.")
    case e: IOException => println("Had an IOException trying to read that file")
} finally {
    // some other code
}

```