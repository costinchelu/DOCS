## Contract between <u>equals()</u> and <u>hashCode()</u>

The **equals()** method of Object class checks the equality of the objects and accordingly it returns true or false. *The default implementation, as provided by Object class, checks the equality of the objects on the basis if both references refer to the same object*. It does not check the value or state of the objects. But we can override this method to provide own implementation to compare the state or value of the objects.  

**hashCode()** method returns an integer value, which is referred to as the hash code value of an object. Every Object, at the time of creation assigned with a unique 32-bit, signed int value. This value is the hash code value of that object.  

**Equals consistency:** objects that are equal to each other must return the same hashCode.  
If we override equals(), we must also override hashCode() or else, if we create 2 objects with the same state, they will have different hashCode (because they will have different locations in the memory).  

[LINK: implement-equals-method-correctly](https://www.sitepoint.com/implement-javas-equals-method-correctly/)  
[LINK: implement-hashcode-method-correctly](https://www.sitepoint.com/how-to-implement-javas-hashcode-correctly/)


## Rules to create equals method

- **Reflexive**: x.equals(x) == true , an object must equal to itself.  
- **Symmetry**: if(x.equals(y)==true) then y.equals(x) == true.  
- **Transitive**: if x.equals(y) and y.equals(z); then x.equals(z)  
- **Consistent**: if x.equals(y)==true and no value is modified, then it’s always true for every call  
- For any non-null object x, x.equals(null)==false


## Differences between == and .equals() method

In general both equals() and “==” operator are used to compare objects to check equality but:

- Main difference between .equals() method and == operator is that one is method and other is operator.
- We can use **== operators for reference comparison** (address comparison) and **.equals() method for content comparison**. In simple words, == checks if both objects point to the same memory location whereas .equals() evaluates to the comparison of values in the objects.
    - If a class does not override the equals method, then by default it uses equals(Object o) method of the closest parent class that has overridden this method. 


## Object cloning

Object.clone() method is used for creating an exact copy of objects in Java. It acts like a copy constructor. It creates and returns a copy of the object, with the same class and with all the fields having same values of the original object. The return type is an Object so it has to explicitly be cast to actual type.

```java
// (I) it should implement Cloneable
public class Person implements Cloneable {

    private String name;
    private int income;
    private City city;          // deep copy
    private Country country;    // shalow copy


    public Person(String name, int income, City city, Country country) {
        this.name = name;
        this.income = income;
        this.city = city;
        this.country = country;
    }

    // no @Override, means we are not overriding clone
    // (II) it should throw CloneNotSupported
    public Person clone() throws CloneNotSupportedException {

        Person cloneObj = (Person) super.clone();   // (III) calls clone() from Object class

        // all other primitive fields are cloned by default
        // by default it will shallow copy all object references,
        // but we can still make deep copy by implementing clone() in those classes:

        cloneObj.city = (City) this.city.clone();

        // to make a deep copy of city we need to call clone that will also be implemented in City class
        // and let's not forget that clone() will return an Object so we need to cast it to City

        // if we are not implementing clone also for Country, we will just shallow copy it
        
        return cloneObj;
    }
    
    // but we can implement a copy constructor (and also implement copy constructors in aggregated classes):
    public Person(Person original) {

        this.name = original.name;
        this.income = original.income;
        this.city = new City(original.city);
        this.country = new Country(original.country);
    }
}
```

## Comparable vs Comparator

- Comparable
  - a java.lang.Comparable() object is capable of comparing itself with another object (given as a parameter)
  - the class itself must implement Comparable interface to compare its instances
  
- Comparator
  - java.util.Comparator() is external to the element type we are comparing (we can compare two objects given as parameters)
  - it's a separate class 
  - create multiple separate classes (that implement Comparator) to compare by different members
  - for example sort() can take a Comparator
  
Comparable is meant for objects with natural ordering which means the object itself must know how it is to be ordered. For example Roll Numbers of students. Whereas, Comparator interface sorting is done through a separate class.
  
Logically, Comparable interface compares “this” reference with the object specified and Comparator in Java compares two different class objects provided.  

If any class implements Comparable interface in Java then collection of that object either List or Array can be sorted automatically by using Collections.sort() or Arrays.sort() method and objects will be sorted based on there natural order defined by CompareTo method.


```java
class Movie implements Comparable<Movie> {
    private double rating;
    private String name;
    private int year;


    public Movie(String nm, double rt, int yr) {
        this.name = nm;
        this.rating = rt;
        this.year = yr;
    }

    // Getters
    public double getRating() { return rating; }
    public String getName()   { return name; }
    public int getYear()      { return year; }

    // Used to sort movies by year
    public int compareTo(Movie m) {
        return this.year - m.year;
    }
}

// Class to compare Movies by ratings
class RatingCompare implements Comparator<Movie> {
    
    public int compare(Movie m1, Movie m2) {
        if (m1.getRating() < m2.getRating()) return -1;
        if (m1.getRating() > m2.getRating()) return 1;
        else return 0;
    }
}

// Class to compare Movies by name
class NameCompare implements Comparator<Movie> {
    
    public int compare(Movie m1, Movie m2) {
        return m1.getName().compareTo(m2.getName());
    }
}


class Main {
    public static void main(String[] args) {
        
        ArrayList<Movie> list = new ArrayList<Movie>();
        
        list.add(new Movie("Force Awakens", 8.3, 2015));
        list.add(new Movie("Star Wars", 8.7, 1977));
        list.add(new Movie("Empire Strikes Back", 8.8, 1980));
        list.add(new Movie("Return of the Jedi", 8.4, 1983));

        // Sort by rating : (1) Create an object of ratingCompare
        //                  (2) Call Collections.sort
        //                  (3) Print Sorted list
        System.out.println("Sorted by rating");
        RatingCompare ratingCompare = new RatingCompare();
        Collections.sort(list, ratingCompare);
        for (Movie movie: list)
            System.out.println(movie.getRating() + " " +
                    movie.getName() + " " +
                    movie.getYear());


        // Call overloaded sort method with RatingCompare
        // (Same three steps as above)
        System.out.println("\nSorted by name");
        NameCompare nameCompare = new NameCompare();
        Collections.sort(list, nameCompare);
        for (Movie movie: list)
            System.out.println(movie.getName() + " " +
                    movie.getRating() + " " +
                    movie.getYear());

        // Uses Comparable to sort by year
        System.out.println("\nSorted by year");
        Collections.sort(list);
        for (Movie movie: list)
            System.out.println(movie.getYear() + " " +
                    movie.getRating() + " " +
                    movie.getName()+" ");
    }
}
```

To summarize, if sorting of objects needs to be based on natural order then use Comparable whereas if you sorting needs to be done on attributes of different objects, then use Comparator in Java.
