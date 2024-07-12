Favoring composition over inheritance is a principle in object-oriented design that emphasizes using object composition (i.e., building complex objects by combining simpler ones) instead of class inheritance for code reuse and flexibility. This approach promotes a more modular, flexible, and maintainable codebase by reducing coupling, improving encapsulation, and allowing for easier changes and extensions.

### Benefits of Favoring Composition

1. **Reduced Coupling** : Composition allows classes to be loosely coupled, as objects are composed of other objects rather than inheriting behavior from a parent class.

2. **Improved Encapsulation** : Composition encourages encapsulation by hiding the internal details of objects behind well-defined interfaces, reducing the impact of changes to internal implementations.

3. **Flexibility** : Objects composed through composition can easily change their behavior by swapping out components, making the system more flexible and adaptable to change.

4. **Code Reuse** : Composition promotes code reuse through the use of reusable components or "has-a" relationships.

5. **Easier Testing** : Composition often leads to classes that are easier to test in isolation, as dependencies can be mocked or replaced more easily.

### Example: Composition vs. Inheritance

Consider a scenario where you have a `Car` class that needs to have features such as `Engine`, `Wheels`, and `Steering`.

#### Using Inheritance:

```java
// Using inheritance
public class Car extends Vehicle {
    // Car-specific implementation
}

public class Vehicle {
    // Common vehicle features
}
```

#### Using Composition:

```java
// Using composition
public class Car {
    private Engine engine;
    private Wheels wheels;
    private Steering steering;

    public Car(Engine engine, Wheels wheels, Steering steering) {
        this.engine = engine;
        this.wheels = wheels;
        this.steering = steering;
    }

    // Car-specific methods using composition
}
```

### Explanation

- **Inheritance** : Inheritance creates a "is-a" relationship where a subclass (e.g., `Car`) inherits from a superclass (e.g., `Vehicle`). While inheritance can promote code reuse, it can also lead to tightly coupled designs, where changes in the superclass can affect subclasses, and vice versa.

- **Composition** : Composition creates a "has-a" relationship where a class (e.g., `Car`) contains instances of other classes (`Engine`, `Wheels`, `Steering`). This approach allows for more flexibility, as the components can be easily swapped or modified independently of each other.

### Guidelines for Using Composition

1. **Identify "has-a" Relationships** : Determine if an object should be composed of other objects based on "has-a" relationships.

2. **Use Interfaces** : Define interfaces for components to promote loose coupling and flexibility.

3. **Prefer Dependency Injection** : Use dependency injection to inject components into the composed class, allowing for easy swapping or configuration.

4. **Encapsulate Behavior** : Encapsulate behavior in components and expose only necessary interfaces to the composed class.

5. **Avoid Deep Nesting** : Avoid overly deep hierarchies of composed objects, as it can lead to complexity and maintenance issues.

### Example: Using Composition for Car Components

Let's expand on the composition example with `Car`, `Engine`, `Wheels`, and `Steering`.

```java
public interface Engine {
    void start();
    void stop();
}

public class ElectricEngine implements Engine {
    @Override
    public void start() {
        // Implementation for starting an electric engine
    }

    @Override
    public void stop() {
        // Implementation for stopping an electric engine
    }
}

public interface Wheels {
    void rotate();
}

public class StandardWheels implements Wheels {
    @Override
    public void rotate() {
        // Implementation for rotating standard wheels
    }
}

public interface Steering {
    void turnLeft();
    void turnRight();
}

public class ManualSteering implements Steering {
    @Override
    public void turnLeft() {
        // Implementation for turning left with manual steering
    }

    @Override
    public void turnRight() {
        // Implementation for turning right with manual steering
    }
}

public class Car {
    private Engine engine;
    private Wheels wheels;
    private Steering steering;

    public Car(Engine engine, Wheels wheels, Steering steering) {
        this.engine = engine;
        this.wheels = wheels;
        this.steering = steering;
    }

    public void start() {
        engine.start();
        wheels.rotate();
    }

    public void stop() {
        engine.stop();
        // Additional actions for stopping the car
    }

    public void turnLeft() {
        steering.turnLeft();
    }

    public void turnRight() {
        steering.turnRight();
    }
}
```

### Conclusion

Favoring composition over inheritance promotes a more modular, flexible, and maintainable design in object-oriented programming. By composing objects through "has-a" relationships, you can achieve greater code reuse, reduced coupling, improved encapsulation, and easier extensibility, making your codebase more adaptable to changes and enhancements over time.
