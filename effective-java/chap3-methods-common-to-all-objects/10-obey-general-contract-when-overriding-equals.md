When overriding the `equals` method in Java, it is crucial to obey its general contract to ensure the method behaves correctly and consistently. The general contract of `equals` as specified in the Java documentation states that:

1. **Reflexive** : For any non-null reference value `x`, `x.equals(x)` should return `true`.

2. **Symmetric** : For any non-null reference values `x` and `y`, `x.equals(y)` should return `true` if and only if `y.equals(x)` returns `true`.

3. **Transitive** : For any non-null reference values `x`, `y`, and `z`, if `x.equals(y)` returns `true` and `y.equals(z)` returns `true`, then `x.equals(z)` should return `true`.

4. **Consistent** : For any non-null reference values `x` and `y`, multiple invocations of `x.equals(y)` should consistently return `true` or consistently return `false`, provided no information used in `equals` comparisons on the objects is modified.

5. **Non-nullity** : For any non-null reference value `x`, `x.equals(null)` should return `false`.

### Example: Overriding equals

Let's implement a `Person` class and override the `equals` method while adhering to the general contract.**Person.java:**

```java
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
        return age == person.age && name.equals(person.name); // Compare significant fields
    }

    @Override
    public int hashCode() {
        int result = name.hashCode();
        result = 31 * result + age;
        return result;
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
    }
}
```

### Explanation

1. **Reflexive** : The method first checks if the current instance (`this`) is the same as the `obj` reference. If true, it returns `true`.

2. **Symmetric** : The method then checks if `obj` is an instance of the `Person` class. If not, it returns `false`. This ensures type compatibility. Then, it compares the significant fields (`name` and `age`) of both objects. If they are equal, it returns `true`.

3. **Transitive** : The equality check on significant fields ensures that if `person1.equals(person2)` and `person2.equals(person4)`, then `person1.equals(person4)`.

4. **Consistent** : The equality check on significant fields (`name` and `age`) ensures that the result of `equals` is consistent as long as these fields are not modified.

5. **Non-nullity** : The method immediately returns `false` if `obj` is `null`.
   Overriding `hashCode`Whenever `equals` is overridden, `hashCode` should also be overridden to maintain the general contract for `hashCode`, which states that equal objects must have equal hash codes. This is particularly important when objects are stored in collections that use hashing, such as `HashMap` and `HashSet`.In this example, `hashCode` is overridden to generate a hash code based on the `name` and `age` fields. This ensures that equal `Person` objects will have the same hash code.

### Summary

- **Reflexive** : `x.equals(x)` must return `true`.

- **Symmetric** : `x.equals(y)` must return `true` if and only if `y.equals(x)` returns `true`.

- **Transitive** : If `x.equals(y)` and `y.equals(z)` return `true`, then `x.equals(z)` must return `true`.

- **Consistent** : Multiple invocations of `x.equals(y)` must consistently return `true` or `false`.

- **Non-nullity** : `x.equals(null)` must return `false`.
  By following these principles when overriding the `equals` method, you can ensure that your objects behave correctly in collections and other contexts where object equality is important.
