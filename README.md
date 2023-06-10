# OOP-practice

## Basic Circle class

This first exercise shall lead you through all the basic concepts in OOP.

![Circle](res/Circle%201.PNG)

A class called `Circle` is designed as shown in the following class diagram. It contains:

- Two private instance variables: `radius` (of the type double) and `color` (of the type String), 
with default value of 1.0 and "red", respectively.
- Two overloaded constructors - a default constructor with no argument, and a constructor which takes a 
double argument for radius.
- Two public methods: `getRadius()` and `getArea()`, which return the radius and area of this instance, respectively.

The source codes for `Circle.java` is as follows:

```
/**
 * The Circle class models a circle with a radius and color.
 */
public class Circle {
   // private instance variable, not accessible from outside this class
   private double radius;
   private String color;
   
   // Constructors (overloaded)
   /** Constructs a Circle instance with default value for radius and color */
   public Circle() {  // 1st (default) constructor
      radius = 1.0;
      color = "red";
   }
   
   /** Constructs a Circle instance with the given radius and default color */
   public Circle(double r) {  // 2nd constructor
      radius = r;
      color = "red";
   }
   
   /** Returns the radius */
   public double getRadius() {
     return radius; 
   }
   
   /** Returns the area of this Circle instance */
   public double getArea() {
      return radius*radius*Math.PI;
   }
}
```
This Circle class does not have a main() method. Hence, it cannot be run directly.
This Circle class is a “building block” and is meant to be used in another program.

Let us write a test program called `TestCircle` (in another source file called `TestCircle.java`) 
which uses the `Circle` class, as follows:

```
/**
 *  A Test Driver for the Circle class
 */
public class TestCircle {
   public static void main(String[] args) {
      // Declare an instance of Circle class called c1.
      // Construct the instance c1 by invoking the "default" constructor
      // which sets its radius and color to their default value.
      Circle c1 = new Circle();
      // Invoke public methods on instance c1, via dot operator.
      System.out.println("The circle has radius of " 
         + c1.getRadius() + " and area of " + c1.getArea());
      //The circle has radius of 1.0 and area of 3.141592653589793
   
      // Declare an instance of class circle called c2.
      // Construct the instance c2 by invoking the second constructor
      // with the given radius and default color.
      Circle c2 = new Circle(2.0);
      // Invoke public methods on instance c2, via dot operator.
      System.out.println("The circle has radius of " 
         + c2.getRadius() + " and area of " + c2.getArea());
      //The circle has radius of 2.0 and area of 12.566370614359172
   }
}
```

Now, run the `TestCircle` and study the results.

## Add a new constructor
Modify the class `Circle` to include a third constructor for constructing a `Circle` instance with two arguments:
a double for `radius` and a String for `color`.

```
// 3rd constructor to construct a new instance of Circle with the given radius and color
public Circle (double r, String c) { ... }
```

Modify the test program `TestCircle` to construct an instance of `Circle` using this constructor.

## Add a new getter
Add a getter for variable color for retrieving the color of this instance.
```
// Getter for instance variable color
public String getColor() { ... }
```
Modify the test program to test this method.

## `public` VS `private`
In `TestCircle`, can you access the instance variable `radius` directly (e.g., `System.out.println(c1.radius)`); 
or assign a new value to `radius` (e.g., `c1.radius=5.0`)? Try it out and explain the error messages.

## Add setters
Is there a need to change the values of `radius` and `color` of a `Circle` instance after it is constructed? 
If so, add two public methods called setters for changing the `radius` and `color` of a `Circle` instance as follows:
```
// Setter for instance variable radius
public void setRadius(double newRadius) {
    radius = newRadius;
}

// Setter for instance variable color
public void setColor(String newColor) { ... }
```

Modify the `TestCircle` to test these methods, e.g.:

```
Circle c4 = new Circle();   // construct an instance of Circle
c4.setRadius(5.5);          // change radius
System.out.println("radius is: " + c4.getRadius()); // Print radius via getter
c4.setColor("green");       // Change color
System.out.println("color is: " + c4.getColor());   // Print color via getter

// You cannot do the following because setRadius() returns void, which cannot be printed
System.out.println(c4.setRadius(4.4));
```

## `this` keyword
Instead of using variable names such as `r` (for radius) and `c` (for color) in the methods' arguments, 
it is better to use variable names `radius` (for radius) and `color` (for color) and use the special 
keyword "`this`" to resolve the conflict between instance variables and methods' arguments. For example,
```
// Instance variable
private double radius;

/** Constructs a Circle instance with the given radius and default color */
public Circle(double radius) {
   this.radius = radius;   // "this.radius" refers to the instance variable
                           // "radius" refers to the method's parameter
   color = "red";
}

/** Sets the radius to the given value */
public void setRadius(double radius) {
   this.radius = radius;   // "this.radius" refers to the instance variable
                           // "radius" refers to the method's argument
}
```
Modify ALL the constructors and setters in the `Circle` class to use the keyword "`this`".

## `toString()` method

Every well-designed Java class should contain a public method called 
`toString()` that returns a description of the instance 
(in the return type of String). 
The `toString()` method can be called explicitly 
(via `instanceName.toString()`) just like any other method; 
or implicitly through `println()`. If an instance is passed to 
the `println(anInstance)` method, the `toString()` method of 
that instance will be invoked implicitly. 
For example, include the following `toString()` methods to the `Circle` class:

```
/** Return a self-descriptive string of this instance in the form of Circle[radius=?,color=?] */
public String toString() {
   return "Circle[radius=" + radius + " color=" + color + "]";
}
```

Try calling `toString()` method explicitly, just like any other method:

```
Circle c5 = new Circle(5.5);
System.out.println(c5.toString());   // explicit call
```

`toString()` is called implicitly when an instance is passed to println() method, for example,

```
Circle c6 = new Circle(6.6);
System.out.println(c6.toString());  // explicit call
System.out.println(c6);             // println() calls toString() implicitly, same as above
System.out.println("Operator '+' invokes toString() too: " + c6);  // '+' invokes toString() too
```

The final class diagram for the `Circle` class is as follows:

![Circle](res/Circle%202.PNG)
