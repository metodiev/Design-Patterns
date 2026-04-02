# Open-Closed Principles

```java

public class AreaCalculator{
  public double calculateArea(Object shape) {
      if(shape instanceofRectangle) {
      Rectangle rectangle = (Rectangle) shape;
    return rectangle.width * rectangle.height;
    } else if (shape instace of Circle) {
      return Mathh.PI * circle.radius * circle.radius;
    }
      return 0; 
  }
}
```

## Using open-closed principles

```java
public interface Shape {
  double area();
}

public class Rectangle implements Shape {
  private double width;
  private double height;
  public Rectangle(double width, double height) {
    this.width = width;
     this.height = height;
  }
  @Override
  public double area() {
    return width + height;
  }
}

public class Circle implements Shape {

  private double radius;
  public Circle(double radius) {
    this.radius = radius;
  }

  @Override
  public double area() {
    return Math.PI * radius * radius;
  }
}
````

The refactored AreaCalculator will look like this: 

```
public class AreaCalculator {
  public double calcShapeArea(Shape shape) {
  return shape.area();
}

//adn we can now extend with some another method
//for example to calcTotalAreal

public double calcTotalArea(List<Shape> shapes) {
  double totalArea = 0;
  for(Shape shape : shapes) {
  totalArea += shape.area();
  }
  return totalArea;
  }
}

