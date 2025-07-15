This is the implementation of the `Map` interface. It stores data in key-value pairs.

Characteristics:
- Key-Value pairs
- Unordered
## Performance
Using hashing to store the index of its pair. When we put a key-value pair, the hashcode() is used to calculate an index where the pair should be stored. 

Operations like `put`, `get`, and `remove`, ideally is average time complexity of O(1).
## Operations
### Creating
```java
// Creating new hashmap with String as key and Integer as Value
Map<String, Integer> scores =  new HashMap<>();

// Creating hashmap from another hashmap
Map<String, Integer> anotherMap = new HashMap<>(scores);
```
### Adding and Updating Elements
```java
scores.put("Alice", 95);

// Updating existing key
scores.put("Alice", 100);
```
### Retrieving Elements
Returns null if the key is not found.
```java
scores.get("Alice");
```
### Removing Elements
```java
scores.remove("Alice");
```
### Checking Existence
```java
scores.containsKey("Alice");
```
### Checking Size
```java
scores.size();
```
### Iterating
#### Iterating as A Set
```java
for (Map.Entry<String, Integer> entry: scores.entrySet()) {

}
```
#### Iterating the Key
```java
for (String name: studentScores.keySet()) {

}
```
#### Using For Each
```java
scores.forEach(
	(key, value) -> System.out.println("Student: " + key + ", Grade: " + value)
)
```
### Clearing the Map
```java
scores.clear()
```