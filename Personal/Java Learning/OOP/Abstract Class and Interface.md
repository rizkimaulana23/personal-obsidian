## Abstract Class
A class that cannot be instantiated on its own. Designed to be a base class for other classes to inherit from. Declared with `abstract`.  

Characteristics:
1. Cannot be instantiated
2. Can have `abstract` method. No body and implementation.
3. Can have concrete method (have complete implementation).
4. Can have constructor
5. Can have instance variables
6. Can have `static` and `final`
## Interface
Blueprint for a class. Any class that implements an interface must provide implementations for all the abstract methods declared in that interface. Declared with `interface` keyword.  

Characteristics:
1. Cannot be instantiated
2. Has `default` and `static` method
	- `default` could have implementation
	- `static` for utility methods in the class itself
3. Can have private methods
4. Fields are implicitly 
5. No constructors
6. Class can implement many interface
7. No instance variables (state): no non-static and non-final fields
