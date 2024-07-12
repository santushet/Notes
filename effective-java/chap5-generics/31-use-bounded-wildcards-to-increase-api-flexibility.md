Bounded wildcards in Java generics allow you to increase the flexibility of your APIs by defining type constraints that provide more options for parameter types. Bounded wildcards are particularly useful when you want to create methods or classes that can work with a wide range of related types without knowing the exact type in advance. They enhance code reusability and allow clients to use your API with a broader set of types.

### Bounded Wildcards Overview

In Java generics, a bounded wildcard is denoted using the `?` wildcard character along with type bounds. There are two types of bounded wildcards:

1. **Upper Bounded Wildcards** : Denoted as `<? extends T>`, where `T` is the upper bound. It allows any type that is a subtype of `T`.

2. **Lower Bounded Wildcards** : Denoted as `<? super T>`, where `T` is the lower bound. It allows any type that is a supertype of `T`.

### Advantages of Bounded Wildcards

1. **Increased Flexibility** : Bounded wildcards allow your methods or classes to accept a wider range of parameter types, enhancing API flexibility.

2. **Polymorphism** : Bounded wildcards facilitate polymorphism, enabling your code to work seamlessly with different subtypes of a given type.

3. **Code Reusability** : By using bounded wildcards, you can write generic code that can be reused with various related types without duplicating code.

### Example and Explanation

Let's consider an example of using bounded wildcards to increase API flexibility.

```java
import java.util.List;

public class APIFlexibilityExample {
    // Upper bounded wildcard
    public static double calculateAverage(List<? extends Number> numbers) {
        double sum = 0.0;
        for (Number number : numbers) {
            sum += number.doubleValue();
        }
        return sum / numbers.size();
    }

    // Lower bounded wildcard
    public static void addNumbers(List<? super Integer> numbers) {
        numbers.add(10);
        numbers.add(20);
        numbers.add(30);
    }

    public static void main(String[] args) {
        List<Integer> integerList = List.of(5, 10, 15);
        List<Double> doubleList = List.of(2.5, 5.0, 7.5);

        System.out.println("Average of integers: " + calculateAverage(integerList));
        // System.out.println("Average of doubles: " + calculateAverage(doubleList)); // Compile-time error

        addNumbers(integerList);  // Integer list can accept numbers using lower bounded wildcard
        System.out.println("Modified integer list: " + integerList);
    }
}
```

In this example:

- The `calculateAverage` method uses an upper bounded wildcard `<? extends Number>`, allowing it to accept lists of any subtype of `Number`, such as `Integer`, `Double`, etc., to calculate their average.

- The `addNumbers` method uses a lower bounded wildcard `<? super Integer>`, enabling it to accept lists of any supertype of `Integer`, such as `Number` or `Object`, and add integers to the list.

### Guidelines for Using Bounded Wildcards

1. **Choose Appropriate Bound** : Decide whether an upper or lower bounded wildcard is appropriate based on the method's requirements.

2. **Avoid Unbounded Wildcards** : Prefer bounded wildcards over unbounded wildcards (`<?>`) when you need to impose type constraints.

3. **Document Usage** : Clearly document the usage of bounded wildcards in your API to guide users on how to use them effectively.

4. **Understand PECS Principle** : PECS stands for "Producer Extends, Consumer Super." Use `<? extends T>` for producer methods (reading from the collection) and `<? super T>` for consumer methods (writing to the collection).

### Conclusion

Using bounded wildcards in Java generics is a powerful technique to increase API flexibility and promote code reusability. By allowing your methods or classes to accept a broader range of related types, bounded wildcards enhance polymorphism and enable your code to work seamlessly with different data structures. When used appropriately and documented clearly, bounded wildcards improve the usability and versatility of your APIs.
