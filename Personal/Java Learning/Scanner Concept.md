### Initiating Scanner
```java
Scanner scanner = new Scanner(System.in); 
```

We could also use Scanner to read from a file.
```java
Scanner fileScanner = new Scanner(new File("input.txt"));
```
### Reading Input
There are many ways to reading an input from the terminal from the user.
#### `next()`
Read the user input until a whitespace is encountered.
```java
Scanner scanner = new Scanner(System.in); 
String word = scanner.next();
```
#### `nextLine()`
Read the user input until a nextline is encountered.
```java
Scanner scanner = new Scanner(System.in); 
String sentence = scanner.nextLine();
```
#### `nextInt()`, `nextDouble()`, etc
Read the user input and then convert into the corresponding data types. Tips while using this is the `next` function will not read the nextline. This could lead into the input of user to be skipped. To prevent this, add `scanner.nextLine()` after the `next..` function.

```java
System.out.print("Enter your age: "); 
int age = scanner.nextInt(); 
scanner.nextLine();
```

