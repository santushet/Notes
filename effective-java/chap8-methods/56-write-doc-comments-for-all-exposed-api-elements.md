Documenting exposed API elements with Javadoc comments is essential for providing clear and useful information to users of your API. Here’s how to write comprehensive doc comments for the examples provided earlier, covering classes, methods, and parameters.

### Example 1: Using Optional as a Return Type

```java
import java.util.Optional;

/**
 * Service class for user-related operations.
 */
public class UserService {

    /**
     * Finds a user by their ID.
     *
     * @param userId the ID of the user to find
     * @return an {@code Optional} containing the found user, or {@code Optional.empty()} if no user was found
     */
    public Optional<User> findUserById(String userId) {
        // Simulate a user lookup
        if ("123".equals(userId)) {
            return Optional.of(new User("123", "Alice"));
        } else {
            return Optional.empty(); // Return an empty Optional if user is not found
        }
    }

    /**
     * Main method to demonstrate usage of {@code UserService}.
     *
     * @param args command-line arguments
     */
    public static void main(String[] args) {
        UserService userService = new UserService();
        Optional<User> userOptional = userService.findUserById("123");

        userOptional.ifPresent(user -> System.out.println("User found: " + user.getName()));
        // Or handle the absence of the user
        User user = userOptional.orElse(new User("0", "Default User"));
        System.out.println("User: " + user.getName());
    }
}

/**
 * Represents a user with an ID and a name.
 */
class User {
    private String id;
    private String name;

    /**
     * Constructs a new {@code User} with the specified ID and name.
     *
     * @param id the ID of the user
     * @param name the name of the user
     */
    public User(String id, String name) {
        this.id = id;
        this.name = name;
    }

    /**
     * Returns the name of the user.
     *
     * @return the name of the user
     */
    public String getName() {
        return name;
    }
}
```

### Example 2: Using Optional with Streams

```java
import java.util.Arrays;
import java.util.List;
import java.util.Optional;

/**
 * Demonstrates the use of {@code Optional} with Java Streams.
 */
public class StreamExample {

    /**
     * Main method to demonstrate finding the first short name in a list of names.
     *
     * @param args command-line arguments
     */
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        Optional<String> firstShortName = names.stream()
                .filter(name -> name.length() <= 3)
                .findFirst();

        firstShortName.ifPresent(name -> System.out.println("First short name: " + name));
    }
}
```

### General Tips for Writing Javadoc Comments

1. **Class-Level Comments** : Describe the purpose of the class and its key features.

2. **Method-Level Comments** : Explain what the method does, its parameters, return value, and any exceptions it may throw.

3. **Parameter Tags** : Use `@param` to describe each parameter.

4. **Return Tags** : Use `@return` to describe the return value.

5. **Exception Tags** : Use `@throws` to describe any exceptions the method might throw.

6. **Examples** : Provide examples when necessary to illustrate how to use the API.

By following these guidelines, you ensure that your API is well-documented, making it easier for others to understand and use.
