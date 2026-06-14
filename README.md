# Java Practice Problem — The Shape Area Calculator

**Course:** Object-Oriented Programming  
**Topics Covered:** Abstract Classes · Method Overriding · Early Binding · Downcasting · `toString()`

---

## The Story

Rafi is a first-year student at MBSTU who just started learning Java. His professor gives the class a small project:

> "Build a shape calculator for a geometry app. The app must support **rectangles** and **circles**. Every shape has a color and can be filled or unfilled. Each shape must be able to report its **area**, its **perimeter**, and a text summary of itself."

The professor adds one important rule:

> "You must design this so that any new shape — triangle, pentagon, anything — can be added later without rewriting the calculator code."

Rafi realizes he needs an **abstract class** called `Shape` that enforces a contract: every shape *must* implement `getArea()` and `getPerimeter()`. `Rectangle` and `Circle` will extend `Shape` and provide their own formulas.

---

## UML Class Diagram

*(See diagram above)*

> **Reading the diagram:**  
> `Shape` is the abstract parent at the top. `Rectangle` and `Circle` extend it (open-triangle arrow = inheritance). Italic method names in `Shape` are abstract — subclasses must override them. Every class also has its own `toString()`.

---

## Formulas

| Shape | Area | Perimeter |
|---|---|---|
| Rectangle | `width × length` | `2 × (width + length)` |
| Circle | `π × radius²` | `2 × π × radius` |

Use `Math.PI` for π in Java.

---

## Concepts You Will Practice

| Concept | Where It Appears |
|---|---|
| Abstract class | `Shape` cannot be instantiated directly |
| Abstract method | `getArea()` and `getPerimeter()` declared but not implemented in `Shape` |
| Method overriding | Each subclass provides its own area and perimeter formulas |
| Early binding | Calling `toString()` on a `Shape` reference is resolved at compile time to `Shape`'s version — but at runtime, Java dispatches to the subclass version |
| Downcasting | Casting a `Shape` reference back to `Rectangle` to access rectangle-specific methods |
| `toString()` | Each class formats itself as a readable string |

---

## Starter Code

Create the following files inside a package named `shapes`.

### `Shape.java`

```java
package shapes;

/**
 * Abstract base class representing any 2D geometric shape.
 * Cannot be instantiated directly — you must use a subclass.
 */
public abstract class Shape {

    // ── Private fields ────────────────────────────────────────
    private String  color;
    private boolean filled;

    // ── Constructor ───────────────────────────────────────────
    public Shape(String color, boolean filled) {
        this.color  = color;
        this.filled = filled;
    }

    // ── Abstract methods — subclasses MUST override these ─────

    /** Returns the area of this shape. */
    public abstract double getArea();

    /** Returns the perimeter (circumference) of this shape. */
    public abstract double getPerimeter();

    // ── Concrete method ───────────────────────────────────────

    /**
     * Returns a text summary of this shape.
     * Subclasses should call super.toString() and append their own details.
     */
    @Override
    public String toString() {
        return "Color : " + color + "\n" +
               "Filled: " + (filled ? "Yes" : "No");
    }

    // ── Getters and setters ───────────────────────────────────
    public String  getColor()           { return color;  }
    public boolean isFilled()           { return filled; }
    public void    setColor(String c)   { this.color  = c; }
    public void    setFilled(boolean f) { this.filled = f; }
}
```

### `Rectangle.java`

```java
package shapes;

public class Rectangle extends Shape {

    private double width;
    private double length;

    // ── Constructor ───────────────────────────────────────────
    public Rectangle(String color, boolean filled, double width, double length) {
        super(color, filled);
        this.width  = width;
        this.length = length;
    }

    // ── Method overriding ─────────────────────────────────────

    @Override
    public double getArea() {
        return width * length;
    }

    @Override
    public double getPerimeter() {
        return 2 * (width + length);
    }

    // ── toString ──────────────────────────────────────────────

    @Override
    public String toString() {
        return "[ Rectangle ]\n" +
               super.toString()  + "\n" +
               "Width : " + width  + "\n" +
               "Length: " + length + "\n" +
               String.format("Area      : %.2f", getArea())      + "\n" +
               String.format("Perimeter : %.2f", getPerimeter());
    }

    // ── Getters ───────────────────────────────────────────────
    public double getWidth()  { return width;  }
    public double getLength() { return length; }
}
```

### `Circle.java`

```java
package shapes;

public class Circle extends Shape {

    private double radius;

    // ── Constructor ───────────────────────────────────────────
    public Circle(String color, boolean filled, double radius) {
        super(color, filled);
        this.radius = radius;
    }

    // ── Method overriding ─────────────────────────────────────

    @Override
    public double getArea() {
        return Math.PI * radius * radius;
    }

    @Override
    public double getPerimeter() {
        return 2 * Math.PI * radius;
    }

    // ── toString ──────────────────────────────────────────────

    @Override
    public String toString() {
        return "[ Circle ]\n" +
               super.toString() + "\n" +
               "Radius: " + radius + "\n" +
               String.format("Area         : %.2f", getArea())      + "\n" +
               String.format("Circumference: %.2f", getPerimeter());
    }

    // ── Getter ────────────────────────────────────────────────
    public double getRadius() { return radius; }
}
```

---

## Tasks for Students

Complete `ShapeMain.java` by following the instructions in each comment. Do not change anything outside the marked sections.

### `ShapeMain.java`

```java
package shapes;

public class ShapeMain {

    public static void main(String[] args) {

        // ── TASK 1 ────────────────────────────────────────────
        // Create two Shape references (use the Shape type, NOT
        // Rectangle or Circle) and assign objects to them.
        //
        //   s1 → Rectangle: color="Red",  filled=true,  width=5.0, length=8.0
        //   s2 → Circle:    color="Blue", filled=false, radius=7.0
        //
        // YOUR CODE HERE:
        Shape s1 = /* ??? */;
        Shape s2 = /* ??? */;


        // ── TASK 2 ────────────────────────────────────────────
        // Store both shapes in a Shape array called shapes.
        //
        // YOUR CODE HERE:
        Shape[] shapes = /* ??? */;


        // ── TASK 3 ────────────────────────────────────────────
        // Loop through the array. For each shape:
        //   a) Print the shape info using System.out.println
        //      (this automatically calls toString())
        //   b) Print a blank line between shapes
        //
        // YOUR CODE HERE:


        // ── TASK 4 — Early Binding ────────────────────────────
        // The reference below has type Shape, but the object
        // is a Rectangle at runtime.
        //
        // Q: When toString() is called on shapeRef, which class
        //    version runs — Shape's or Rectangle's? Why?
        //
        // Write your answer as a comment on the line marked ANSWER.
        //
        Shape shapeRef = new Rectangle("Green", true, 4.0, 9.0);
        System.out.println(shapeRef.toString());
        // ANSWER: _______________________________________________


        // ── TASK 5 — Downcasting ─────────────────────────────
        // s1 holds a Rectangle but its declared type is Shape.
        // You cannot call getWidth() on s1 directly.
        //
        // Step 1: Use instanceof to check s1 is a Rectangle.
        // Step 2: Downcast s1 to a Rectangle variable called r.
        // Step 3: Print r.getWidth() and r.getLength().
        //
        // YOUR CODE HERE:


        // ── TASK 6 — Abstract class restriction ───────────────
        // Uncomment the line below. What compiler error appears?
        // Write the error as a comment, then re-comment the line.
        //
        // Shape s = new Shape("Black", false);
        // ERROR: ________________________________________________


        // ── TASK 7 (Bonus) ────────────────────────────────────
        // Write a static method called printShapeInfo that
        // accepts a Shape parameter and prints its area and
        // perimeter. Call it once with s1 and once with s2.
        //
        // Notice: the same method works for BOTH shape types
        // without any if/else. This is called polymorphism.
        //
        // YOUR CODE HERE:
    }

    // ── Bonus method stub ─────────────────────────────────────
    // public static void printShapeInfo(Shape s) { ... }
}
```

---

## Sample Input and Output

The program uses no keyboard input — all values are hardcoded in `main()`. The expected console output for the completed tasks is shown below.

### Task 3 output — printing all shapes

```
[ Rectangle ]
Color : Red
Filled: Yes
Width : 5.0
Length: 8.0
Area      : 40.00
Perimeter : 26.00

[ Circle ]
Color : Blue
Filled: No
Radius: 7.0
Area         : 153.94
Circumference: 43.98
```

### Task 4 output — early binding test

```
[ Rectangle ]
Color : Green
Filled: Yes
Width : 4.0
Length: 9.0
Area      : 36.00
Perimeter : 26.00
```

> The `Shape` reference `shapeRef` points to a `Rectangle` object at runtime. Java's virtual method dispatch (late binding) calls `Rectangle.toString()` — not `Shape.toString()`. The declared type controls what methods you can *call*; the actual object type controls which version *runs*.

### Task 5 output — downcasting

```
Downcasting s1 to Rectangle...
Width : 5.0
Length: 8.0
```

### Task 7 output — bonus polymorphism method

```
--- Shape Info ---
Area     : 40.00
Perimeter: 26.00

--- Shape Info ---
Area     : 153.94
Perimeter: 43.98
```

---

## Full Working Solution (check your work after attempting)

<details>
<summary>Click to reveal solution</summary>

```java
package shapes;

public class ShapeMain {

    public static void main(String[] args) {

        // Task 1
        Shape s1 = new Rectangle("Red",  true,  5.0, 8.0);
        Shape s2 = new Circle(   "Blue", false, 7.0);

        // Task 2
        Shape[] shapes = { s1, s2 };

        // Task 3
        for (Shape s : shapes) {
            System.out.println(s);
            System.out.println();
        }

        // Task 4
        Shape shapeRef = new Rectangle("Green", true, 4.0, 9.0);
        System.out.println(shapeRef.toString());
        // ANSWER: Rectangle's toString() runs. Even though shapeRef is
        // declared as Shape, the object is a Rectangle at runtime.
        // Java uses late binding (dynamic dispatch) for non-static,
        // non-final methods, so the overridden version is always called.

        // Task 5
        if (s1 instanceof Rectangle) {
            Rectangle r = (Rectangle) s1;   // downcast
            System.out.println("Downcasting s1 to Rectangle...");
            System.out.println("Width : " + r.getWidth());
            System.out.println("Length: " + r.getLength());
        }

        // Task 6 — keep commented:
        // Shape s = new Shape("Black", false);
        // ERROR: Shape is abstract; cannot be instantiated

        // Task 7
        System.out.println("\n--- Shape Info ---");
        printShapeInfo(s1);
        System.out.println("\n--- Shape Info ---");
        printShapeInfo(s2);
    }

    public static void printShapeInfo(Shape s) {
        System.out.printf("Area     : %.2f%n", s.getArea());
        System.out.printf("Perimeter: %.2f%n", s.getPerimeter());
    }
}
```

</details>

---

## Concept Explanation Notes

### Abstract class

`Shape` is declared `abstract`, so `new Shape(...)` causes a compile-time error. Its job is to define the *contract* — every shape must provide `getArea()` and `getPerimeter()` — without specifying *how* to compute them.

### Method overriding

When `Rectangle` writes `@Override public double getArea()`, it replaces `Shape`'s declaration with its own formula (`width * length`). Rules for a valid override:

- Same method name and parameter list.
- Same or covariant return type.
- Cannot reduce visibility (cannot change `public` to `private`).

The `@Override` annotation is optional but recommended — the compiler catches typos in the signature.

### Early binding vs late binding

In Java, `static`, `final`, and `private` methods use **early binding** — the exact method call is decided at compile time based on the reference type. All other methods (including `getArea()` and `toString()`) use **late binding (dynamic dispatch)** — the JVM checks the actual object type at runtime and calls the correct overridden version.

```java
Shape s = new Rectangle("Red", true, 5, 8);
s.getArea();     // ← calls Rectangle.getArea() at runtime (late binding)
```

The declared type `Shape` controls what method names are *accessible*. The runtime type `Rectangle` controls which *version* runs.

### Downcasting

```java
Shape s1 = new Rectangle("Red", true, 5.0, 8.0);

// s1.getWidth();   ← compile error: Shape has no getWidth()

if (s1 instanceof Rectangle) {
    Rectangle r = (Rectangle) s1;  // downcast
    r.getWidth();                   // now accessible
}
```

Always use `instanceof` before downcasting. Without the check, an incorrect cast throws `ClassCastException` at runtime.

---

## Common Mistakes to Watch For

| Mistake | What happens |
|---|---|
| `new Shape("Red", true)` | Compile error — cannot instantiate abstract class |
| Forgetting `@Override` on `getArea()` | Silently creates a new method; the abstract version remains unimplemented, causing compile error |
| `(Rectangle) s2` where `s2` holds a `Circle` | `ClassCastException` at runtime |
| Calling `getWidth()` on a `Shape` reference | Compile error — `getWidth()` is not declared in `Shape` |
| `toString()` not calling `super.toString()` | Output loses `color` and `filled` from the parent |

---

## Submission Checklist

- [ ] `Shape.java` — abstract class with two abstract methods and `toString()`
- [ ] `Rectangle.java` — overrides `getArea()`, `getPerimeter()`, `toString()`; adds `getWidth()`, `getLength()`
- [ ] `Circle.java` — overrides `getArea()`, `getPerimeter()`, `toString()`; adds `getRadius()`
- [ ] `ShapeMain.java` — all seven tasks completed with comments answered
- [ ] Output matches the sample output above (values rounded to 2 decimal places)
- [ ] Program compiles with zero errors or warnings
