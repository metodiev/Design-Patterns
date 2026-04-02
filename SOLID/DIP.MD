# Dependency Inversion Principle DIP

Depend upon abstractions, not concretions.

What does that mean that: 

1. Identify direct dependencies between high-level and low-level modules in your 
code.
2. Introduce an interface or abstract class to decouple these modules.
3. Modify the high-level module to depend on the abstraction, not on the low-level
module
4. Implement the abstraction in each low-level module.
5. Use Dependency injection to provide the low-level module to the high-level module.

```java
class LightBulb{
  void trunOn(){
    System.out.println("Light bulb turned on")'
  }
  void turnOff(){
    System.out.println("Light bulb turned off");
  }
}

class Switch {
  private LightBulb lightBulb;
  private boolean isOn = false;

  public Switch(LightBulb lightBub){
    this.lightBulb = lightBulb;
  }

  void toggle(){
    if (isOn){
      lightBulb.turnOff();
      isOn = false;
      System.out.println("Switched off");
    } else {
      lightBulb.turnOn();
      isOn = true;
      System.out.println("Switched on");
    }
  }
}
```


The solution is to create an interface 


```java

public interface Switchable {
  void turnOn();
  void turnOff();

}

public class LightBulb implements Switchable {}

```

```
