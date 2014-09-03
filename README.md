PythonToScala
=============
![PyToScala](https://farm4.staticflickr.com/3865/14938431420_58b1ffaaa9.jpg)

The goal of this project is to be a concise guide for those transitioning from Python to Scala. This is by *no means* meant to be a complete guide to Scala, but rather some (hopefully) helpful snippets of code to help you translate between the two languages.

This guide loosely follows along with the text of [Scala for the Impatient](http://www.horstmann.com/scala/index.html), a great introductory book for those learning Scala. You might find it helpful to read it alongside the chapters from this repo.

Note that in general, you should not try to directly translate idioms from one language to another; you don't want to write Scala that looks like Python- you want to write Scala that looks like Scala! You should strive to write idiomatic code whenever possible. A good starting point is Twitter's [Effective Scala](http://twitter.github.io/effectivescala/)

I recommend reading through the guide in the following order:

1. Variables and Arithmetic
2. Conditionals
3. Functions
4. Strings
5. Sequences
6. Maps
7. Tuples
8. Exceptions
9. Classes

Here are some Scala topics not discussed above that I think are important to review:
* **Pattern Matching** This is like a switch statement on turbo, and is very powerful and oft used. The [Scala Cookbook](http://shop.oreilly.com/product/0636920026914.do) has really great practical examples.
* **Auxiliary Constructors** Classes can have multiple constructors that operate on different argument types/number of args.
* **Case Classes** as an immutable, record-like data-structure that can be pattern-matched.
* **Scala Collections** There is a lot of power in all of the methods available to data structures like Vector, Array, List, Sequence, Set, etc. Just take a [look](http://www.scala-lang.org/api/current/index.html#scala.collection.Seq) at all of the available methods.

This can also be read as a [GitBook](http://wrobstory.gitbooks.io/python-to-scala/), which offers pdf/ebook downloads and a nice web format for reading.
