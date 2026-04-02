# Interface Segregation Principle (ISP)

Clients should not be forced to depend upon interfaces that they do not use

```java
public interface Worker {
  void eat();
  void work();
}

public class HumanWorker implements Worker {


}

public class RobotWorker implements Worker {


}
```
