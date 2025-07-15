## String Builder
#### Make a New String Builder Objects
```java
StringBuilder strBuilder = new StringBuilder();
```
#### Appending String
```java
strBuilder.append("String");
```
#### Insert
Function ini akan memasukkan string pada index tertentu
```java
StringBuilder sb = new StringBuilder("Java is fun"); sb.insert(8, "very "); // Output: Java is very fun
```

#### Replace
```java

```
#### Converting to String
```java
strBuilder.toString();
```
## String
String adalah immutable object. Jadi, ketika kita memanggil method yang mengubah String-nya, maka Java akan membuat Object String yang baru. 
#### Length
```java
String text = "Hello World";
int len = text.length();
```
#### Checking Empty String
Mengecek jika String-nya memiliki panjang 0
```java
String string = "";
boolean isEmpty = string.isEmpty();
```
#### Concatenate
#### Comparing Operations
Ketika kita menggunakan `==`, maka kita akan membandingkan referensi String itu sendiri, sedangkan jika kita menggunakan `equals()`, maka kita akan membandingkan nilai dari String itu sendiri.
#### Getting String at Index

