# Liskov Substitution Principle (LSP)

The Liskov Subtitution principle: Functions that are use pointers, or references to base
classes, must be able to use objects of derived classes without knowing it.

## The problem:
```java
abstract class Vehicle {
  abstract void refuel();
  abstract void move();
}

class ElectricCar extends Vehicle {
  @Override
  void refuel() {
    System.out.printl("Charging baterry...");
  }

@Override
void move(){
  System.out.println("Moving...")
}
}

class PetrolCar extends Vehicle {
  @override
  void refuel() {
    System,.out.println("Refilling petron..");
  }

 @Override
 void move() {
    System.out.println("Moving...");
 }

 public static void serviceVehicle(Vehicle vehicle) {
  vehicle.refuel();
  //some mroe servicing activities
 }
}

class PetrolCar Extends FuelVehicle {}

```


How to solve the problem


```java
abstract class Vehicle {
  abstract void move();

}

abstract class FuelVehicle extends Vehicle {
  abstract void charge();

}

class ElectricCar extends ElectricVehicle {

@Override
void charge() {
System.out.println("Charging battery...");

}

@override 
void move(){
  System.out.println("Moving...")

}
}
