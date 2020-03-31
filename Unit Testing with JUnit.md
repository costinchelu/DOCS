# Unit Testing with JUnit
A *software test* is a piece of software, which executes another piece of software. It validates if that code results in the expected state (state testing) or executes the expected sequence of events (behavior testing).

Software unit tests help the developer to verify that the logic of a piece of the program is correct.

Running tests automatically helps to identify software regressions introduced by changes in the source code. Having a high test coverage of your code allows you to continue developing features without having to perform lots of manual tests.  
## 
A test *fixture* is a fixed state of a set of objects which are used as a baseline for running tests. Another way to describe this is a test precondition.

For example, a test fixture might be a a fixed string, which is used as input for a method. The test would validate if the method behaves correctly with this input.
## 
A *unit test* is a piece of code written by a developer that executes a specific functionality in the code to be tested and asserts a certain behavior or state.

The percentage of code which is tested by unit tests is typically called *test coverage*.

A unit test targets a small unit of code, e.g., a method or a class. External dependencies should be removed from unit tests, e.g., by replacing the dependency with a *test implementation or a (mock)* object created by a test framework.

Unit tests are not suitable for testing complex user interface or component interaction. For this, you should develop integration tests.
## 
- import org.junit.*

Import statement for using the following annotations.

- @Test

Identifies a method as a test method.

- @Before

Executed before each test. It is used to prepare the test environment (e.g., read input data, initialize the class).

- @After

Executed after each test. It is used to cleanup the test environment (e.g., delete temporary data, restore defaults). It can also save memory by cleaning up expensive memory structures.

- @BeforeClass

Executed once, before the start of all tests. It is used to perform time intensive activities, for example, to connect to a database. Methods marked with this annotation need to be defined as static to work with JUnit.

- @AfterClass

Executed once, after all tests have been finished. It is used to perform clean-up activities, for example, to disconnect from a database. Methods annotated with this annotation need to be defined as static to work with JUnit.

- @Ignore or @Ignore("Why disabled")

Marks that the test should be disabled. This is useful when the underlying code has been changed and the test case has not yet been adapted. Or if the execution time of this test is too long to be included. It is best practice to provide the optional description, why the test is disabled.

- @Test (expected = Exception.class)

Fails if the method does not throw the named exception.

- @Test(timeout=100)

Fails if the method takes longer than 100 milliseconds.
## 
JUnit provides static methods to test for certain conditions via the Assert class. These assert statements typically start with assert. They allow you to specify the error message, the expected and the actual result. An assertion method compares the actual value returned by a test to the expected value. It throws an AssertionException if the comparison fails.

- fail([message])

Let the method fail. Might be used to check that a certain part of the code is not reached or to have a failing test before the test code is implemented. The message parameter is optional.

- assertTrue([message,] boolean condition)

Checks that the boolean condition is true.

- assertFalse([message,] boolean condition)

Checks that the boolean condition is false.

- assertEquals([message,] expected, actual)

Tests that two values are the same. Note: for arrays the reference is checked not the content of the arrays.

- assertEquals([message,] expected, actual, tolerance)

Test that float or double values match. The tolerance is the number of decimals which must be the same.

- assertNull([message,] object)

Checks that the object is null.

- assertNotNull([message,] object)

Checks that the object is not null.

- assertSame([message,] expected, actual)

Checks that both variables refer to the same object.

- assertNotSame([message,] expected, actual)

Checks that both variables refer to different objects.

- @RepeatedTest(<Number>)

Repeats the test a <Number> of times

- @TestFactory

Method is a Factory for dynamic tests

- @BeforeEach

Executed before each test. It is used to prepare the test environment (e.g., read input data, initialize the class).

- @AfterEach

Executed after each test. It is used to cleanup the test environment (e.g., delete temporary data, restore defaults). It can also save memory by cleaning up expensive memory structures.

- @BeforeAll

Executed once, before the start of all tests. It is used to perform time intensive activities, for example, to connect to a database. Methods marked with this annotation need to be defined as static to work with JUnit.

- @AfterAll

Executed once, after all tests have been finished. It is used to perform clean-up activities, for example, to disconnect from a database. Methods annotated with this annotation need to be defined as static to work with JUnit.

- @Nested

Lets you nest inner test classes to force a certain execution order

- @Tag("<TagName>")

Tests in JUnit 5 can be filtered by tag. Eg., run only tests tagged with "fast".

- @ExtendWith

Lets you register an Extension class that integrates with one or more extension points

- @Disabled or @Disabled("Why disabled")

Marks that the test should be disabled. This is useful when the underlying code has been changed and the test case has not yet been adapted. Or if the execution time of this test is too long to be included. It is best practice to provide the optional description, why the test is disabled.

- @DisplayName("<Name>")

<Name> that will be displayed by the test runner. In contrast to method names the DisplayName can contain spaces.

- @SelectPackages  

Used to specify the names of packages for the test suite

- @SelectClasses  

Used to specify the classes for the test suite. They can be located in different packages.

## 
If you have several test classes, you can combine them into a *test suite*. Running a test suite executes all test classes in that suite in the specified order. A test suite can also contain other test suites.

The following example code demonstrates the usage of a test suite. It contains two test classes (MyClassTest and MySecondClassTest). If you want to add another test class, you can add it to the `@Suite.SuiteClasses` statement.  

`import org.junit.runner.RunWith;`  
`import org.junit.runners.Suite;`  
`import org.junit.runners.Suite.SuiteClasses;`

`@RunWith(Suite.class)`  
`@SuiteClasses({MyClassTest.class, MySecondClassTest.class})`  
`public class AllTests { }`
## 
The @Ignore annotation allow to statically ignore a test. Alternatively you can use Assume.assumeFalse or Assume.assumeTrue to define a condition for the test. Assume.assumeFalse marks the test as invalid, if its condition evaluates to true. Assume.assumeTrue evaluates the test as invalid if its condition evaluates to false. For example, the following disables a test on Linux:  
`Assume.assumeFalse(System.getProperty("os.name").contains("Linux"));`
## 


