There are four pillars of Object Oriented Programming.
1. Encapsulation
2. Abstraction
3. Inheritance
4. Polymorphism
5. Association / Composition / Aggregation (Relationships); this is often debated
# Encapsulation
Bundling the data and the methods within a single unit (a class). Restricting access to the object's component and only allowing what we could access.

This could be achieved by using a private access modifier and setting a Public Getter and Setter method.
# Abstraction
Showing only the essential information and hiding the complex implementation detail. It's about "what" not about the "how". 

This could be achieve by using abstract classes and interfaces.
# Inheritance
Inheritance allows a new class to inherit properties and behaviors from an existing class. 

This could be achieve by using the `extends` keyword. But, in Java, Java could only support single inheritance. 
# Polymorphism
Polymorphism means "many form". This refers to the ability of an object to take many forms, or the ability of a variable, function, or object to take on different types.

This could be achieved by method overriding using the `@Override` annotation, Method overloading by setting a same function name but accept different parameters, and interface implementation. 
# Relationships
Explains how objects relates to each other.
- Association: General relationship between two classes
- Aggregation: "has-a" relationship. Weak has-a relationship.
- Composition: "has-a" relationship. Strong has-a relationship. 

This could be achieved by having instance variables in the Class itself.