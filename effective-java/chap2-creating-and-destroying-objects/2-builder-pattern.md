The Builder Pattern is a creational design pattern that provides a way to construct complex objects step by step. It allows you to produce different types and representations of an object using the same construction code.

Here's a detailed example to illustrate the Builder Pattern in Java:

### Scenario

Suppose we have a `Pizza` class with various attributes like size, crust type, cheese, and toppings. We want to create instances of `Pizza` with different combinations of these attributes.

### Pizza Class with Builder Pattern

1. **Define the `Pizza` class and its Builder inner class:**

```java
public class Pizza {
    // Required parameters
    private final String size;
    private final String crust;

    // Optional parameters
    private final boolean cheese;
    private final boolean pepperoni;
    private final boolean bacon;
    private final boolean mushrooms;

    // Private constructor to be called by the builder
    private Pizza(PizzaBuilder builder) {
        this.size = builder.size;
        this.crust = builder.crust;
        this.cheese = builder.cheese;
        this.pepperoni = builder.pepperoni;
        this.bacon = builder.bacon;
        this.mushrooms = builder.mushrooms;
    }

    // Static inner builder class
    public static class PizzaBuilder {
        // Required parameters
        private final String size;
        private final String crust;

        // Optional parameters - initialize with default values
        private boolean cheese = false;
        private boolean pepperoni = false;
        private boolean bacon = false;
        private boolean mushrooms = false;

        // Constructor with required parameters
        public PizzaBuilder(String size, String crust) {
            this.size = size;
            this.crust = crust;
        }

        // Setter methods for optional parameters
        public PizzaBuilder withCheese(boolean cheese) {
            this.cheese = cheese;
            return this;
        }

        public PizzaBuilder withPepperoni(boolean pepperoni) {
            this.pepperoni = pepperoni;
            return this;
        }

        public PizzaBuilder withBacon(boolean bacon) {
            this.bacon = bacon;
            return this;
        }

        public PizzaBuilder withMushrooms(boolean mushrooms) {
            this.mushrooms = mushrooms;
            return this;
        }

        // Build method to create the Pizza object
        public Pizza build() {
            return new Pizza(this);
        }
    }

    // Getter methods for the attributes
    public String getSize() {
        return size;
    }

    public String getCrust() {
        return crust;
    }

    public boolean hasCheese() {
        return cheese;
    }

    public boolean hasPepperoni() {
        return pepperoni;
    }

    public boolean hasBacon() {
        return bacon;
    }

    public boolean hasMushrooms() {
        return mushrooms;
    }

    @Override
    public String toString() {
        return "Pizza{" +
                "size='" + size + '\'' +
                ", crust='" + crust + '\'' +
                ", cheese=" + cheese +
                ", pepperoni=" + pepperoni +
                ", bacon=" + bacon +
                ", mushrooms=" + mushrooms +
                '}';
    }
}
```

1. **Using the Builder Pattern:**

```java
public class Main {
    public static void main(String[] args) {
        Pizza pizza1 = new Pizza.PizzaBuilder("Large", "Thin Crust")
                .withCheese(true)
                .withPepperoni(true)
                .build();

        Pizza pizza2 = new Pizza.PizzaBuilder("Medium", "Pan Crust")
                .withCheese(true)
                .withBacon(true)
                .withMushrooms(true)
                .build();

        System.out.println(pizza1);
        System.out.println(pizza2);
    }
}
```

### Explanation

1. **Required Parameters:**

- The `PizzaBuilder` constructor takes the required parameters `size` and `crust`.

2. **Optional Parameters:**

- The optional parameters `cheese`, `pepperoni`, `bacon`, and `mushrooms` are set using the builder's setter methods, which return the builder object itself (this enables method chaining).

3. **Build Method:**

- The `build()` method constructs the `Pizza` object using the `PizzaBuilder` instance's attributes.

4. **Private Constructor:**

- The `Pizza` class has a private constructor that takes a `PizzaBuilder` instance. This constructor initializes the `Pizza` object's fields with the values from the builder.

5. **Fluent API:**

- The builder pattern provides a fluent API, making the object creation code readable and easy to understand.

### Benefits of the Builder Pattern

- **Readability:** The code for creating objects is more readable and can be understood at a glance.

- **Immutability:** The `Pizza` class can be made immutable, as its fields are final and set only once via the builder.

- **Flexibility:** The builder pattern allows for optional parameters, avoiding the need for numerous constructors with different combinations of parameters.

- **Maintainability:** Adding new parameters is easier. You can simply add new setter methods to the builder without modifying existing constructors.

By using the Builder Pattern, you create a flexible and readable way to construct complex objects in Java.
