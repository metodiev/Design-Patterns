
# Builder Pattern

It hides the process of building complex objects. A builder is an object able to construct other objects. It constructs and assembles different object parts to build the result objects.
The builder pattern is not just about encapsulation and hiding of the creation process; it is also designed for reusability and flexibility.

When to use the builder pattern: 
1. When you have a complex class with many constructors
2. When you have to build complex composite tree objects.
3. When you want to build different representations of your complex objects, but still use the same general steps.

Pros:
1. Provides clear separation between the construction and representation of an object.
2. Provides finer control over the steps of the construction process.
3. It supports changing the internal representation of objects.

Cons:
1. A distinct Concrete Builder must be created for each type of object.
2. Builder classes must be mutable
3. May hamper/complicate dependency injection.


Design Consideration:

1. Encapsulate creating and assembling the parts of a complex object in a separate Buidelr object,
2. Create a specific class (a Director) which will delegate object creation to a Builder object instead of creating the objects directly,
3. Look for synergy in the family of the object you are modelling. You should be able to use the same construction process by delegating to different Builder objects to create diffrent representations of a complex object. 


## Code

```java
public class Pizza {

  private final String name;
  private final String size;
  private final String crust;
  private final List<String> toppings;

 //constructor
  private Pizza(PizzaBuilder builder) {
    this.name = builder.name;
    this.size = builder.sizer;
    this.crust = builder.crust;
    this.toppings = builder.toppings;  
  }

 //Getter methods to access the properties of Pizza
 public String getName(){
    return name;
 }

 public String getSize() {
    return size;
 }

public String getCrust() {
    return crust;

}

public List<String> getToppings() {
  return new ArrayList<>(toppings);
}

public static class PizzaBuilder {

  private String name;
  private String size;
  private String crust;
  private List<String> toppings = new ArrayList<>();

  //Builder method for settings properties
  public PizzaBuilder name(String name){
    this.name = name;
    return this;
  }

  public PizzaBuilder size(String size) {
    this.size = size;
    return this;
  }

  public PizzaBuilder crust(String crust) {
    this.crust = crust;
    return this;
  }

  public PizzaBuilder toppings(String topping) {
    this.toppings.add(topping)
    return this;
  }

  //Builds the new Pizza object using the attributes set in the builder.
  public Pizza build() {
    return nre Pizza(this);
  }
}

}
```


Now let's create our PizzaDirector 

```java
public class PizzaDirector {
  public static void constructNeapolitanPizza(Pizza.PizzaBuilder builder) {
    builder.name("Neapolitan Pizza")
    .size("Medium")
    .crust("Thin")
    .topping("Tomatoes")
    .topping("Mozzarella Cheese"
    .topiing("Basil");      

//.......
)
    
  }

}
```

## Builder with Validation

```java
public class User {
    private final String name;
    private final int age;
    private final String email;

    private User(Builder builder) {
        this.name = builder.name;
        this.age = builder.age;
        this.email = builder.email;
    }

    public static class Builder {
        private final String name;
        private int age;
        private String email;

        public Builder(String name) {
            this.name = name;
        }

        public Builder age(int age) {
            this.age = age;
            return this;
        }

        public Builder email(String email) {
            this.email = email;
            return this;
        }

        public User build() {
            validate();
            return new User(this);
        }

        private void validate() {
            if (name == null || name.isBlank()) {
                throw new IllegalStateException("Name is required");
            }
            if (age < 0 || age > 120) {
                throw new IllegalStateException("Invalid age");
            }
            if (email != null && !email.contains("@")) {
                throw new IllegalStateException("Invalid email");
            }
        }
    }
}
```

## Builder + Immutability

```java
import java.util.List;

public final class Order {
    private final String id;
    private final List<String> items;

    private Order(Builder builder) {
        this.id = builder.id;
        this.items = List.copyOf(builder.items); // defensive copy
    }

    public List<String> getItems() {
        return items; // already unmodifiable
    }

    public static class Builder {
        private final String id;
        private List<String> items;

        public Builder(String id) {
            this.id = id;
        }

        public Builder items(List<String> items) {
            this.items = List.copyOf(items); // defensive copy
            return this;
        }

        public Order build() {
            if (items == null || items.isEmpty()) {
                throw new IllegalStateException("Items cannot be empty");
            }
            return new Order(this);
        }
    }
}
```
