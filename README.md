## TinyMapper

A simple tool that automatically maps a ResultSet to a POJO, using the power of reflection.

\
Usage:
```java
// Certain code has been omitted as to focus only on TinyMapper.

// Make a new mapper of type T. In this case Student.
var studentMapper = new TinyMapper<>(Student.class);

// Use the mapper to map the resultSet to a Student.
var student = studentMapper.map(resultSet);
```

\
POJO:

Use the @Column annotation to specify the name of the column that corresponds to the field. \
Or embed a POJO in another POJO with @Embed.
```java
public class Student {

    @Column(name="id")
    private String id;

    @Column(name="email_address")
    private String email;
    
    @Embed
    private FullName fullName;
    
    ...
```

\
The POJO must have an <ins>empty constructor</ins> and <ins>setter methods</ins> for each field for TinyMapper to work.
```java
    public Student() {}
    
    public void setId(String id) {
        this.id = id;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public void setFullName(FullName fullName) {
        this.fullName = fullName;
    }
}
```

\
The embedded class must still follow the POJO rules.
```java
public class FullName {
    
    @Column(name="firstname")
    private String firstName;

    @Column(name="lastname")
    private String lastName;

    public FullName() {}

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }
}
```
