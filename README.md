# Java Practice Problem — The Zoo Animal System

**Course:** Object-Oriented Programming  
**Topics Covered:** Abstract Classes · Method Overriding · Early Binding · Downcasting · `toString()`

---

## The Story

You have just been hired as a junior software developer at **Dhaka City Zoo**. The zoo manager, Mr. Karim, needs a small Java program to keep track of the animals. The zoo has three kinds of animals right now: **dogs**, **birds**, and **fish**.

Mr. Karim tells you:

> "Every animal has a name, an age, and a habitat. But each animal makes a different sound and moves in a completely different way. I also need a neat summary of each animal I can print on a card."

Your job is to design and implement this system using **Java inheritance and abstract classes** so that future animal types (lions, snakes, etc.) can be added easily without rewriting everything.

---

## UML Class Diagram

*(See diagram above)*

> **Reading the diagram:**  
> `Animal` is the abstract parent class at the top. `Dog`, `Bird`, and `Fish` each extend it (open-triangle arrow = inheritance). Italic method names in `Animal` are abstract — subclasses *must* override them. Every class also provides its own `toString()`.

---

## Concepts You Will Practice

| Concept | Where It Appears in This Problem |
|---|---|
| **Abstract class** | `Animal` cannot be instantiated directly |
| **Abstract method** | `makeSound()` and `move()` are declared but not implemented in `Animal` |
| **Method overriding** | Each subclass provides its own `makeSound()` and `move()` |
| **Early binding** | Calling `toString()` on an `Animal` reference resolves at *compile time* to `Animal.toString()` |
| **Downcasting** | Casting an `Animal` reference back to `Dog` to call `fetch()` |
| **`toString()`** | Each class formats its own information as a readable string |

---

## Starter Code

Create the following files inside a package named `zoo`.

### `Animal.java`

```java
package zoo;

/**
 * Abstract base class representing any animal in the zoo.
 * Cannot be instantiated directly.
 */
public abstract class Animal {

    // ── Fields ────────────────────────────────────────────────
    private String name;
    private int    age;
    private String habitat;

    // ── Constructor ───────────────────────────────────────────
    public Animal(String name, int age, String habitat) {
        this.name    = name;
        this.age     = age;
        this.habitat = habitat;
    }

    // ── Abstract methods (subclasses MUST override these) ─────

    /** Every animal makes a different sound. */
    public abstract void makeSound();

    /** Every animal moves in a different way. */
    public abstract void move();

    // ── Concrete method ───────────────────────────────────────

    /**
     * Returns a formatted summary of this animal.
     * Subclasses may call super.toString() and append extra info.
     */
    @Override
    public String toString() {
        return "Name   : " + name    + "\n" +
               "Age    : " + age     + " years\n" +
               "Habitat: " + habitat;
    }

    // ── Getters ───────────────────────────────────────────────
    public String getName()    { return name;    }
    public int    getAge()     { return age;     }
    public String getHabitat() { return habitat; }
}
```

### `Dog.java`

```java
package zoo;

public class Dog extends Animal {

    private String breed;

    public Dog(String name, int age, String breed) {
        super(name, age, "Land");   // dogs always live on land
        this.breed = breed;
    }

    // ── Method overriding ─────────────────────────────────────

    @Override
    public void makeSound() {
        System.out.println(getName() + " says: Woof! Woof!");
    }

    @Override
    public void move() {
        System.out.println(getName() + " runs on four legs.");
    }

    // ── Dog-specific method ───────────────────────────────────

    public void fetch() {
        System.out.println(getName() + " fetches the ball!");
    }

    // ── toString ─────────────────────────────────────────────

    @Override
    public String toString() {
        return "[ Dog ]\n" +
               super.toString() + "\n" +
               "Breed  : " + breed;
    }
}
```

### `Bird.java`

```java
package zoo;

public class Bird extends Animal {

    private boolean canFly;

    public Bird(String name, int age, boolean canFly) {
        super(name, age, "Sky/Trees");
        this.canFly = canFly;
    }

    @Override
    public void makeSound() {
        System.out.println(getName() + " says: Tweet! Tweet!");
    }

    @Override
    public void move() {
        if (canFly) {
            System.out.println(getName() + " flies through the air.");
        } else {
            System.out.println(getName() + " walks on two legs (cannot fly).");
        }
    }

    public void sing() {
        System.out.println(getName() + " sings a beautiful song!");
    }

    @Override
    public String toString() {
        return "[ Bird ]\n" +
               super.toString() + "\n" +
               "Can fly: " + (canFly ? "Yes" : "No");
    }
}
```

### `Fish.java`

```java
package zoo;

public class Fish extends Animal {

    private String waterType;   // "Freshwater" or "Saltwater"

    public Fish(String name, int age, String waterType) {
        super(name, age, "Water");
        this.waterType = waterType;
    }

    @Override
    public void makeSound() {
        System.out.println(getName() + " blows bubbles silently.");
    }

    @Override
    public void move() {
        System.out.println(getName() + " swims gracefully underwater.");
    }

    public void blowBubbles() {
        System.out.println(getName() + " blows a stream of bubbles!");
    }

    @Override
    public String toString() {
        return "[ Fish ]\n" +
               super.toString() + "\n" +
               "Water  : " + waterType;
    }
}
```

---

## Tasks for Students

Complete the `ZooMain.java` file below by following the instructions in each comment. **Do not change anything outside the marked sections.**

### `ZooMain.java`

```java
package zoo;

public class ZooMain {

    public static void main(String[] args) {

        // ── TASK 1 ────────────────────────────────────────────
        // Create three Animal references (use the Animal type,
        // NOT Dog / Bird / Fish) and assign a Dog, a Bird, and
        // a Fish to them.
        //
        //  Dog  : name="Bruno",  age=3, breed="Labrador"
        //  Bird : name="Tweety", age=1, canFly=true
        //  Fish : name="Nemo",   age=2, waterType="Saltwater"
        //
        // YOUR CODE HERE:
        Animal a1 = /* ??? */;
        Animal a2 = /* ??? */;
        Animal a3 = /* ??? */;


        // ── TASK 2 ────────────────────────────────────────────
        // Store all three animals in an Animal array called zoo.
        //
        // YOUR CODE HERE:
        Animal[] zoo = /* ??? */;


        // ── TASK 3 ────────────────────────────────────────────
        // Loop through the array and for each animal:
        //   a) Print the animal info using println (this calls toString())
        //   b) Call makeSound()
        //   c) Call move()
        //   d) Print a blank line between animals
        //
        // YOUR CODE HERE:


        // ── TASK 4 — Early Binding ────────────────────────────
        // The line below calls toString() on an Animal reference
        // pointing to a Dog object.
        //
        // Question: Which toString() runs — Animal's or Dog's?
        // Write your answer as a comment on the next line.
        //
        Animal earlyRef = new Dog("Rex", 5, "German Shepherd");
        System.out.println(earlyRef.toString());
        // ANSWER: _______________________________________________


        // ── TASK 5 — Downcasting ─────────────────────────────
        // a1 holds a Dog object but its type is Animal.
        // You cannot call fetch() on it directly.
        //
        // Step 1: Check if a1 is actually a Dog using instanceof.
        // Step 2: Downcast a1 to a Dog.
        // Step 3: Call fetch() on the downcasted variable.
        //
        // YOUR CODE HERE:


        // ── TASK 6 — Cannot instantiate abstract class ────────
        // Uncomment the line below. What error do you get?
        // Write the error message as a comment, then re-comment
        // the line so your program compiles.
        //
        // Animal x = new Animal("Ghost", 0, "Unknown");
        // ERROR: ________________________________________________

    }
}
```

---

## Expected Output

```
[ Dog ]
Name   : Bruno
Age    : 3 years
Habitat: Land
Breed  : Labrador
Bruno says: Woof! Woof!
Bruno runs on four legs.

[ Bird ]
Name   : Tweety
Age    : 1 years
Habitat: Sky/Trees
Can fly: Yes
Tweety says: Tweet! Tweet!
Tweety flies through the air.

[ Fish ]
Name   : Nemo
Age    : 2 years
Habitat: Water
Water  : Saltwater
Nemo blows bubbles silently.
Nemo swims gracefully underwater.

[ Dog ]
Name   : Rex
Age    : 5 years
Habitat: Land
Breed  : German Shepherd
Bruno fetches the ball!
```

---

## Concept Explanation Notes

### Abstract class

`Animal` is declared `abstract`, which means:

- You **cannot** write `new Animal(...)` — the compiler forbids it.  
- It may contain both abstract methods (no body) and concrete methods (with body).  
- Its purpose is to define a **contract** that all subclasses must honour.

### Method overriding

When `Dog` writes `@Override public void makeSound()`, it provides its own version. The `@Override` annotation is optional but strongly recommended — the compiler will catch typos in the method signature.

Rules for a valid override:

- Same method name, same parameter list.  
- Return type must be the same or a subtype (covariant return).  
- Cannot reduce visibility (e.g., cannot change `public` to `private`).

### Early binding (`toString()`)

In Java, **all method calls are resolved at runtime** through dynamic dispatch — *except* for `static`, `final`, and `private` methods, which are bound at compile time (early/static binding).

However, `toString()` is interesting here as a teaching tool: when you call `System.out.println(earlyRef)`, the compiler knows at compile time that `earlyRef` has type `Animal` and that `Animal` has a `toString()`. But at **runtime**, because `earlyRef` actually points to a `Dog` object, Java's virtual method table dispatches to `Dog.toString()`. This is **late binding (dynamic dispatch)**.

> **Key takeaway:** Reference type determines what methods are *accessible* at compile time. Object type determines which version *runs* at runtime.

### Downcasting

```java
// a1 is declared as Animal but holds a Dog object
Animal a1 = new Dog("Bruno", 3, "Labrador");

// This line would NOT compile — Animal has no fetch() method:
// a1.fetch();   ✗

// Safe downcast:
if (a1 instanceof Dog) {
    Dog d = (Dog) a1;   // downcast
    d.fetch();           // now accessible ✓
}
```

An unsafe cast (without `instanceof`) throws a `ClassCastException` at runtime if the object is not actually of that type. Always check first.

---

## Common Mistakes to Watch For

| Mistake | What happens |
|---|---|
| `new Animal(...)` | Compile error — cannot instantiate abstract class |
| Forgetting `@Override` on `makeSound()` | Silently creates a new method instead of overriding — `makeSound()` on an `Animal` reference calls the abstract version and crashes |
| Casting `a2` (Bird) to `Dog` | `ClassCastException` at runtime |
| Calling `fetch()` on an `Animal` reference | Compile error — `fetch()` is not in `Animal` |
| `toString()` not calling `super.toString()` | Subclass output loses `name`, `age`, and `habitat` |

---

## Submission Checklist

- [ ] `Animal.java` — abstract class with two abstract methods and `toString()`  
- [ ] `Dog.java` — overrides `makeSound()`, `move()`, `toString()`; adds `fetch()`  
- [ ] `Bird.java` — overrides `makeSound()`, `move()`, `toString()`; adds `sing()`  
- [ ] `Fish.java` — overrides `makeSound()`, `move()`, `toString()`; adds `blowBubbles()`  
- [ ] `ZooMain.java` — all six tasks completed with comments answered  
- [ ] Program compiles with no errors  
- [ ] Output matches the expected output above
