# Factortory Method Pattern

Factory Method is a creational design pattern that lets us abstract out the creation logic of specific class instances, so it provides a mechanism for creation of objects without exposing the instantiation logic to the client.

There are two main and crucial points in understanding this pattern:

1. Objects are created by calling a factory method instead of calling a constructor.
2. Objects are created through an abstraction not a concretion.

   So in the Factory Method design pattern, we create objects without exposing the creation logic to the caller, and the caller refers to the newly created object through a common interface.

   Pros:
   1. It allows sub-classes to choose the type of objects to create
   2. Simple to implement (simpler that Builder pattern)
   3. Promotes loose-coupling by eliminating the need to bind application-specific classes into the code. That means the code interacts only with the resultant interface or abstract class.
   4. Single Responsibility Principle. You can move the creation code into one place in the program, making the code easier to support.
   5. Open/closed Principle. You can introduce new subtypes into the program without breaking existing client code. This results in Clean code.
  
  Cons:
  1. One disadvantage of the Factory  Method pattern is that it can expand the total number of classes in a system. Every concrete class also requires a concrete Creator class. Note: the Parametrized Factory Method avoids this downside.

## There two main variants of the pattern:

1. The very popular Simple Factory Method variant (also called Parametrized Factory Method pattern)
2. Classic GoF Factory Method

```java
public static Shape createShape(ShapeType shapeType, int width, int height, int strokeThickness) {
  int x = random.nextInt(width);
  int y = random.nextInt(height);

  Color color = new Color(random.nextFloat(), random.nextFloat(), random.nextFloat());

  Shape shape;

  switch(shapeType) {
    case RECTANGLE:
        shape = new Rectangle(x, y, 50 , color);
        break;
    case CIRLE:
      shape = new Circle(x, y, 25, color);
      break;
    default:
    throw new IllegalArgumentException("Unknown shape type:" + shapeType)

    
  }

  shape.setStrokeThicness(strokeThicness);
  return shape;
}
```


      
