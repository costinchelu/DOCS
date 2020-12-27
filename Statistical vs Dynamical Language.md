# Statically vs Dynamically Typed Languages
#

![Statistical, dynamical, strong, weak](images/Statistical%20vs%20Dynamical/statistical_vs_dynamical.png)

## Type Checking

The process of verifying and enforcing the constraints of types . 

Type Checking may occur either at **compile-time (a static check)** or at **run-time (dynamic check)**.  
If a language specification requires its typing rules strongly (i.e., more or less allowing only those automatic type conversions that do not lose information), one can refer to the process as **<u>Strongly typed</u>**, if not, as **<u>Weakly typed</u>**.

## Static Typed Languages

<u>A language is statically-typed if the type of a variable is known at compile-time instead of at run-time.</u>  
Common examples of statically-typed languages include Java, C, C++, FORTRAN, Pascal and Scala.

In statically typed languages, once a variable has been declared with a type, it cannot ever be assigned to some other variable of different type and doing so will raise a type error at compile-time

Java example:
```java
int data;
data = 50;
data = "Hello World!"; // causes an compilation error
```

## Dynamically Typed Languages

<u>A language is dynamically-typed if the type of a variable is checked during run-time.</u>  
Common examples of dynamically-typed languages includes JavaScript, Objective-C, PHP, Python, Ruby, Lisp, and Tcl.

In dynamically typed languages, variables are bound to objects at run-time by means of assignment statements, and it is possible to bind the same variables to objects of different types during the execution of the program.

Dynamic type checking typically results in less optimized code than static type checking. It also includes the possibility of run time type errors and forces run time checks to occur for every execution of the program (instead of just at compile-time). But the absence of a separate compilation step means that you don’t have to wait for the compiler to finish before you can test your code changes. This makes the debug cycle much shorter and less cumbersome.

Python example:
```python
data = 10;
data = "Hello World!"; 
# no error caused
```

## Strongly Typed Languages

A strongly-typed language is one in which variables are bound to specific data types, and will result in type errors if types do not match up as expected in the expression — regardless of when type checking occurs.

Python example:
```python
temp = "Hello World!"
temp = temp + 10; 
# program terminates with below stated error
```
*Traceback (most recent call last):  
File "…\Test.py", line 2, in NFG
temp = temp + 10; 
TypeError: cannot concatenate 'str' and 'int' objects*  

In the above example, temp is of string type. In the second line, we tried attempting to add 10 (an integer type) to a variable of string type. As we can see, a TypeError is returned, indicating that a str object cannot be concatenated with an int object. This is what characterizes strong typed languages: variables are bound to a particular data type.

## Weakly Typed Languages

A weakly-typed language is a language in which variables are not bound to a specific data type; they still have a type, but type safety constraints are lower compared to strongly-typed languages.

PHP example:
```php
$temp = “Hello World!”;
$temp = $temp + 10; // no error caused
echo $temp;
```

In this example, variable temp is initially a string type. In the second line, we add this string variable to 10, an integer. This is permitted in PHP, and is characteristic of all weakly-typed languages.


SOURCE:  
https://android.jlelse.eu/magic-lies-here-statically-typed-vs-dynamically-typed-languages-d151c7f95e2b