
## Adapter Pattern

 Adapter is a structural design pattern which is used to convert the interface contract of one class to be compatible with another.

 This 'conversion' can take two different elements into account
 1. Adapter can convert source data into formats that the client can understand.
 2. Adapter can also help objects with different (or incompatible) interfaces collaborate
  example:
    Legacy Rectangle has (x, y, w, h)       Interface adapter accept the legacy variables and call the new Rectangle interface -> (x, y, w, h -> )Interface -> x1, y1, x2, y2  finally the interface call the Rectangle Interface -> Rectangle (x1, y1, x2, y2)


## When to use:
1. Use the Adapter pattern when you have an existing class or contract that you would to reuse , but its interface isn't compatible with the rest of your code.

## When not to use:

1. When your system is very time-sensitive since 'waping' the Adaptee creates a but of an overhead as it creates an extra call layer,

Pros: 
1. You can separate data conversion code from the main business logic of your application. This follows the Single Responsibility Principle.
2. You can introduce Adapters into your code without breaking any existing client code. This follows the open/Closed Principle.

Cons:
1. The Adapter pattern can increase the overall complexity of your code since you introduce a set of new interfaces and classes


## Code
```java

public class Contact {
 private String fullName;
 private String email;
 private String phoneNumber;
 private boolean friend;

 public Contact(String fullName, String email, String phoneNumber, boolean friend) {
 this.fullName = fullName;
 this.email = email;
 this,phoneNumber = phoneNumber;
 this.friend = friend;
}

//Getters
public String getFullName(){
 return fullName;
 }

public String getEmail(){
 return email;
}

public String getPhoneNumber() {
 return phoneNumber;
}

public boolean isFriend() {
 return friend;
}

@Override
public String toString() {
 return "Contact" + "FUlname ......"
}


}
```

