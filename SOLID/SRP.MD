# Single Responsibility

```java
public class UserSettings{
  private User user;
  public UserSettings(User user){
    this.user = user;
  }

//this class violates the SRP
  public void changeEmail(String newEmail){
    if(checkAccess(user)) {
      user.setEmail(newEmail);
      System.out.println("Emaile changed");
    }
  )

private boolen checkAccess(Uuser user){
    //logic to check if user has access rights
    return true;
  }
}

```

## Refactor the class to have Single Responsibility

```java
public class UserSettings{
  private User user;
  public UserSettings(User user){
    this.user = user;
  }

//this class violates the SRP
  public void changeEmail(String newEmail){
    if(checkAccess(user)) {
      user.setEmail(newEmail);
      System.out.println("Emaile changed");
    }
  )
}

//separate the responsibility
public class SecurityService {
  public boolean hasAccess(User user) {
    //Check if the user has access rights
    //
return true;
  }
}
```
