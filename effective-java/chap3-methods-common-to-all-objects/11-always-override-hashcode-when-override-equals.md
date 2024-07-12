When you override the `equals` method in Java, you must also override the `hashCode` method to maintain the general contract for `hashCode`. This contract states that equal objects must have equal hash codes. Failing to do so can lead to unexpected behavior when objects are stored in hash-based collections such as `HashMap` or `HashSet`.

### Why Override hashCode?

The general contract for `hashCode` is:

1. **Consistency** : The hash code must remain consistent as long as the object is not modified.

2. **Equality** : If two objects are equal according to the `equals` method, they must have the same hash code.

3. **Inequality** : It's not required that two unequal objects must have different hash codes, but doing so can improve the performance of hash-based collections.

### Example: Overriding equals and hashCode

Let's create a `Person` class and correctly override both `equals` and `hashCode`.**Person.java:**

```java
import java.util.Objects;

public class Person {
    private final String name;
    private final int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Getters
    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true; // Reflexive
        if (obj == null || getClass() != obj.getClass()) return false; // Nullity and type check

        Person person = (Person) obj;
        return age == person.age && Objects.equals(name, person.name); // Compare significant fields
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, age); // Generate hash code from significant fields
    }

    public static void main(String[] args) {
        Person person1 = new Person("Alice", 30);
        Person person2 = new Person("Alice", 30);
        Person person3 = new Person("Bob", 25);

        // Reflexive
        System.out.println(person1.equals(person1)); // true

        // Symmetric
        System.out.println(person1.equals(person2)); // true
        System.out.println(person2.equals(person1)); // true

        // Transitive
        Person person4 = new Person("Alice", 30);
        System.out.println(person1.equals(person2)); // true
        System.out.println(person2.equals(person4)); // true
        System.out.println(person1.equals(person4)); // true

        // Consistent
        System.out.println(person1.equals(person2)); // true
        System.out.println(person1.equals(person2)); // true

        // Non-nullity
        System.out.println(person1.equals(null)); // false

        // Test hashCode
        System.out.println(person1.hashCode() == person2.hashCode()); // true
        System.out.println(person1.hashCode() == person3.hashCode()); // false
    }
}
```

### Explanation

1. **equals Method** :

- **Reflexive** : Checks if the object is compared with itself.

- **Type and Null Check** : Ensures the object is non-null and of the same type.

- **Field Comparison** : Compares the significant fields (`name` and `age`).

2. **hashCode Method** :

- Uses `Objects.hash(name, age)` to generate a hash code from the significant fields. This ensures that equal objects will have the same hash code, satisfying the hash code contract.

### Using hashCode and equals in Collections

**Example: Using Person in HashSet and HashMap**

```java
import java.util.HashMap;
import java.util.HashSet;
import java.util.Map;
import java.util.Set;

public class Main {
    public static void main(String[] args) {
        Person person1 = new Person("Alice", 30);
        Person person2 = new Person("Alice", 30);
        Person person3 = new Person("Bob", 25);

        // Using HashSet
        Set<Person> peopleSet = new HashSet<>();
        peopleSet.add(person1);
        peopleSet.add(person2); // Will not be added as it's equal to person1
        peopleSet.add(person3);

        System.out.println("HashSet size: " + peopleSet.size()); // Output: 2

        // Using HashMap
        Map<Person, String> peopleMap = new HashMap<>();
        peopleMap.put(person1, "Person 1");
        peopleMap.put(person2, "Person 2"); // Will replace the value for person1 key
        peopleMap.put(person3, "Person 3");

        System.out.println("HashMap size: " + peopleMap.size()); // Output: 2
        System.out.println("Value for person1 key: " + peopleMap.get(person1)); // Output: Person 2
    }
}
```

### Explanation

1. **HashSet** :

- When adding `person2` to the `HashSet`, it won't be added because it is considered equal to `person1` and has the same hash code.

- The size of the `HashSet` will be 2, containing only unique `Person` objects.

2. **HashMap** :

- When putting `person2` into the `HashMap`, it will replace the value for the `person1` key because they are equal and have the same hash code.

- The size of the `HashMap` will be 2, with `person1` and `person3` as keys.

### Summary

- **Overriding equals** : Ensures logical equality based on significant fields.

- **Overriding hashCode** : Ensures that equal objects have the same hash code, which is crucial for hash-based collections.

- **Consistency** : Ensure both methods are consistent with each other to maintain the general contract for `equals` and `hashCode`.
  By following these guidelines, you can ensure your Java classes work correctly with collections and other data structures that rely on `equals` and `hashCode`.
