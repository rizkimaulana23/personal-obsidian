## Array
This data structure is for holding the primitive
### Making a New Array 

```java
int[] arr = new int[10]; 
```
## ArrayList
Dynamic array for storing non-primitive data type. 

Memory allocations for it:
1. Object Overhead for the metadata of the Array List itself
2. Each element of the Object[] is a reference to an actual Object that is allocated on the heap separately.

Untuk perlakuan operasi, terdapat size dan capacity. Pada saat membuat array baru, jika tidak didefinisikan, capacity-nya adalah 10 dan size-nya adalah 0. Jika capacity-nya penuh, maka Array akan memperbanyak capacity-nya menjadi 1.5 capacity yang lama. Perbanyakan capacity tersebut akan membuat Object[] yang baru dengan capacity yang baru tersebut. Setelah itu Object Array yang lama akan dibuat ke garbage collector. 
### Making a new Array List

```java
ArrayList<String> array = new ArrayList<>();
```

