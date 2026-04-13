# State Pattern

The State Pattern is a behavioral software design pattern that allows an object to alter its behavior when its internal state changes.


Example the toaster state:

State:
1. Idle
2. Bread Loaded
3. Toasting
4. Bread Ejected

When to use:

1. Use the State pattern when you have an object that changes its behaviour depending on its internal state, especially when the number of possible states in non-trivial.
a. Look for many if-else statements that change behaviour of the object.
2. Use it when you have a number of rules that act on an object based on the object;s state, especially when modeling real-world workflows.

When not to use: 
1. If the state transitions are very simple and infrequent it might not be advatageous to use the sate pattern as it would add unnecessary complexity

Pros:
1. State pattern reduces/minimizes conditional complexity by removing bulky and hard to maintain if-then-else or switch-case statement logic.
2. You are able to introduce new states withoud changing the existing state classes or the Context. This follows the Open/Closed Principle.
3. All the code related to a specific state is in its own separate class. This follows the Single Responsibility Principle

Cons:
1. The State pattern can require a lot of code to be written which grows in complexity as more states are modelled,


Design Considerations:

1. Look for a class or logic(if distributed across a few classes) that has some rule dependent or state-dependent code. This will be our Context
2. Declare the State interface and design state-specific method behaviour.
3. For each actual state, create a concrete State implementation.
4. In the Context class, add a reference to the State interface with a public setter
5. For each state, conditionally implement the corresponding method in the Context class.
6. Switching the Context state will be done by setting the correct State instance.
  a. This can be done within the Context itself, in the State instances, or by the client.


## Code

### Step 1: State Interface

```java
public interface VendingState {
    void insertMoney(VendingMachine machine, int amount);
    void selectProduct(VendingMachine machine);
    void dispense(VendingMachine machine);
}
```

### Step 2: Context (Vending Machine)

```java
public class VendingMachine {

    private VendingState state;

    public VendingMachine() {
        this.state = new IdleState(); // initial state
    }

    public void setState(VendingState state) {
        this.state = state;
    }

    public void insertMoney(int amount) {
        state.insertMoney(this, amount);
    }

    public void selectProduct() {
        state.selectProduct(this);
    }

    public void dispense() {
        state.dispense(this);
    }
}
```

### Step 3: Concrete States

```java
public class IdleState implements VendingState {

    @Override
    public void insertMoney(VendingMachine machine, int amount) {
        System.out.println("Money inserted: " + amount);
        machine.setState(new HasMoneyState());
    }

    @Override
    public void selectProduct(VendingMachine machine) {
        System.out.println("Insert money first!");
    }

    @Override
    public void dispense(VendingMachine machine) {
        System.out.println("Insert money first!");
    }
}

```

### Has Money State

```java

public class HasMoneyState implements VendingState {

    @Override
    public void insertMoney(VendingMachine machine, int amount) {
        System.out.println("Already have money. Extra added: " + amount);
    }

    @Override
    public void selectProduct(VendingMachine machine) {
        System.out.println("Product selected.");
        machine.setState(new DispensingState());
    }

    @Override
    public void dispense(VendingMachine machine) {
        System.out.println("Select product first!");
    }
}
```

### Dispensing State

```java
public class DispensingState implements VendingState {

    @Override
    public void insertMoney(VendingMachine machine, int amount) {
        System.out.println("Wait, dispensing in progress!");
    }

    @Override
    public void selectProduct(VendingMachine machine) {
        System.out.println("Already dispensing!");
    }

    @Override
    public void dispense(VendingMachine machine) {
        System.out.println("Dispensing product...");
        machine.setState(new IdleState());
    }
}
```

### Step 4: Usage

```java
public class Main {
    public static void main(String[] args) {

        VendingMachine machine = new VendingMachine();

        machine.selectProduct();   //  invalid
        machine.insertMoney(100);  // → Idle → HasMoney
        machine.selectProduct();   // → HasMoney → Dispensing
        machine.dispense();        // → back to Idle
    }
}
```

What is doing above code:

| State      | Behavior           |
| ---------- | ------------------ |
| Idle       | only accepts money |
| HasMoney   | allows selection   |
| Dispensing | only dispenses     |
