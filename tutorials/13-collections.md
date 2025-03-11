
# 📘 Tutorial Java OOP #13: Collections Framework

> *"Collections Framework adalah toolkit yang tak ternilai bagi programmer Java—menyediakan struktur data yang powerful dan efisien untuk menyimpan, mengelola, dan memanipulasi kelompok objek tanpa perlu membangun struktur dari awal."*

## 🎯 Tujuan Pembelajaran

Setelah mempelajari materi ini, Anda diharapkan dapat:
- Memahami konsep dasar Collections Framework dalam Java
- Mengenali hierarki interface dan implementasi berbagai collection
- Membedakan dan menggunakan berbagai tipe collection: List, Set, Queue, dan Map
- Memilih implementasi collection yang tepat sesuai kebutuhan
- Memanipulasi data dalam collection (menambah, menghapus, mencari, dan mengurutkan)
- Menggunakan Iterator dan Enhanced for-loop untuk traversal collection
- Memanfaatkan Collections utility class untuk operasi umum
- Menerapkan Collections Framework dalam aplikasi nyata
- Memahami Generic dalam konteks Collections Framework
- Menyesuaikan perilaku collection dengan Comparable dan Comparator

## 📋 Daftar Isi

1. [Pendahuluan](#pendahuluan)
2. [Apa itu Collections Framework?](#apa-itu-collections-framework)
   - [Konsep Dasar](#konsep-dasar)
   - [Keuntungan Menggunakan Collections Framework](#keuntungan-menggunakan-collections-framework)
3. [Hierarki Collection](#hierarki-collection)
   - [Interface Collection](#interface-collection)
   - [Interface dan Implementasi Utama](#interface-dan-implementasi-utama)
4. [Interface dan Implementasi List](#interface-dan-implementasi-list)
   - [ArrayList](#arraylist)
   - [LinkedList](#linkedlist)
   - [Vector dan Stack](#vector-dan-stack)
   - [Perbandingan Implementasi List](#perbandingan-implementasi-list)
5. [Interface dan Implementasi Set](#interface-dan-implementasi-set)
   - [HashSet](#hashset)
   - [LinkedHashSet](#linkedhashset)
   - [TreeSet](#treeset)
   - [Perbandingan Implementasi Set](#perbandingan-implementasi-set)
6. [Interface dan Implementasi Queue](#interface-dan-implementasi-queue)
   - [PriorityQueue](#priorityqueue)
   - [Deque dan ArrayDeque](#deque-dan-arraydeque)
7. [Interface dan Implementasi Map](#interface-dan-implementasi-map)
   - [HashMap](#hashmap)
   - [LinkedHashMap](#linkedhashmap)
   - [TreeMap](#treemap)
   - [Hashtable](#hashtable)
   - [Perbandingan Implementasi Map](#perbandingan-implementasi-map)
8. [Traversal Collection](#traversal-collection)
   - [Iterator dan Iterable](#iterator-dan-iterable)
   - [Enhanced for-loop](#enhanced-for-loop)
   - [forEach() dengan Lambda (Java 8+)](#foreach-dengan-lambda-java-8)
9. [Manipulasi Data dalam Collection](#manipulasi-data-dalam-collection)
   - [Menambah dan Menghapus Elemen](#menambah-dan-menghapus-elemen)
   - [Mencari dan Memeriksa Elemen](#mencari-dan-memeriksa-elemen)
   - [Sorting dan Ordering](#sorting-dan-ordering)
   - [Comparable vs Comparator](#comparable-vs-comparator)
10. [Collections Utility Class](#collections-utility-class)
    - [Method Berguna dalam Collections](#method-berguna-dalam-collections)
    - [Unmodifiable Collections](#unmodifiable-collections)
    - [Synchronized Collections](#synchronized-collections)
11. [Collections Framework dan Generics](#collections-framework-dan-generics)
    - [Type Safety dengan Generics](#type-safety-dengan-generics)
    - [Wildcard dalam Generics](#wildcard-dalam-generics)
12. [Best Practices](#best-practices)
13. [Latihan Praktik dengan NetBeans](#latihan-praktik-dengan-netbeans)
14. [Rangkuman](#rangkuman)
15. [Latihan Soal](#latihan-soal)
16. [Referensi](#referensi)

## Pendahuluan

Pada tutorial sebelumnya, kita telah mempelajari berbagai konsep OOP di Java dari mulai dasar sampai konsep lanjutan seperti polimorfisme, interface, abstract class, anonymous class, lambda expression, dan exception handling. Semua konsep ini membentuk fondasi yang kuat untuk membangun aplikasi Java yang terstruktur dan maintainable.

Namun, hampir semua aplikasi memerlukan pengelolaan data—menyimpan, mengurutkan, mencari, dan memanipulasi kumpulan objek. Tanpa framework yang tepat, Anda akan menemukan diri Anda menulis ulang algoritma pemrosesan data yang sama berulang kali.

Di sinilah Java Collections Framework menjadi sangat berharga. Collections Framework menyediakan sekumpulan interface dan class yang terintegrasi untuk memanipulasi kelompok objek secara efisien. Framework ini merampingkan pengembangan dengan menyediakan implementasi struktur data yang umum digunakan (seperti list, set, queue, dan map) serta algoritma untuk memanipulasinya.

Dalam tutorial ini, kita akan mengeksplorasi Java Collections Framework secara menyeluruh, belajar cara memilih struktur data yang tepat untuk kebutuhan spesifik, dan menggunakan operasi collection untuk mengelola data secara efektif.

## Apa itu Collections Framework?

### Konsep Dasar

**Collections Framework** adalah arsitektur untuk merepresentasikan dan memanipulasi collections, memungkinkan mereka dikelola secara terpisah dari detail implementasinya. Sebuah collection adalah sekelompok objek yang dikelola sebagai unit tunggal. Collections Framework terdiri dari:

- **Interfaces**: Jenis-jenis abstract data yang merepresentasikan collections
- **Implementations**: Implementasi konkrit dari interface collection
- **Algorithms**: Methods yang melakukan operasi umum pada collections, seperti pencarian dan pengurutan

Framework ini tidak hanya menyediakan API untuk manipulasi data, tetapi juga mengikuti prinsip desain yang konsisten, yang membuatnya mudah dipelajari dan digunakan.

### Keuntungan Menggunakan Collections Framework

1. **Mengurangi Usaha Pemrograman**: Anda tidak perlu menulis struktur data dasar dari awal.
2. **Kualitas Program Meningkat**: Implementasi Collections Framework sudah teruji, dioptimalkan, dan di-maintain.
3. **Meningkatkan Kecepatan dan Efisiensi**: Setiap struktur data dioptimalkan untuk use case spesifik.
4. **Reusability**: Collection didesain untuk digunakan kembali dalam berbagai konteks.
5. **Interoperability**: Menggunakan API standar memudahkan interaksi antar komponen.
6. **Mengurangi Effort untuk Mempelajari API**: Konsistensi desain membuatnya lebih mudah dipelajari.
7. **Mendorong Reuse Software**: Promosi arsitektur dan komponen yang dapat digunakan kembali.

## Hierarki Collection

### Interface Collection

Di puncak hierarki collection terdapat interface `Collection`. Interface ini adalah root dari framework collection dan mendeklarasikan fungsionalitas inti yang dimiliki oleh semua collection.

Interface `Collection` menyediakan method dasar untuk:
- Menambah elemen: `add()`, `addAll()`
- Menghapus elemen: `remove()`, `removeAll()`, `clear()`
- Memeriksa konten: `contains()`, `containsAll()`, `isEmpty()`, `size()`
- Traversal: `iterator()`
- Konversi: `toArray()`

### Interface dan Implementasi Utama

Hierarki Collections Framework dapat digambarkan sebagai berikut:

```
Collection (interface)
|
|-- List (interface)
|   |-- ArrayList (class)
|   |-- LinkedList (class)
|   |-- Vector (class)
|       |-- Stack (class)
|
|-- Set (interface)
|   |-- HashSet (class)
|   |   |-- LinkedHashSet (class)
|   |-- SortedSet (interface)
|       |-- NavigableSet (interface)
|           |-- TreeSet (class)
|
|-- Queue (interface)
    |-- PriorityQueue (class)
    |-- Deque (interface)
        |-- ArrayDeque (class)
        |-- LinkedList (class)
```

Di luar hierarki `Collection` terdapat interface `Map` yang memetakan key ke value:

```
Map (interface)
|
|-- HashMap (class)
|   |-- LinkedHashMap (class)
|
|-- SortedMap (interface)
|   |-- NavigableMap (interface)
|       |-- TreeMap (class)
|
|-- Hashtable (class)
```

Perhatikan bahwa `LinkedList` muncul di dua tempat, karena mengimplementasikan baik `List` maupun `Deque`.

## Interface dan Implementasi List

`List` adalah collection terurut (ordered) yang memungkinkan duplikat. Elemen dapat diakses dan dimanipulasi berdasarkan posisi index mereka dalam list.

Operasi utama pada `List`:
- Akses posisional: `get()`, `set()`, `add(index, element)`, `remove(index)`
- Pencarian: `indexOf()`, `lastIndexOf()`
- Iterasi: `listIterator()`
- Range-view: `subList()`

### ArrayList

`ArrayList` adalah implementasi `List` yang menggunakan array dinamis untuk menyimpan elemen. Ini adalah implementasi yang paling umum digunakan karena performa umumnya yang baik.

```java
// Creating an ArrayList
List<String> fruits = new ArrayList<>();

// Adding elements
fruits.add("Apple");
fruits.add("Banana");
fruits.add("Orange");

// Accessing elements
String firstFruit = fruits.get(0);  // "Apple"

// Updating elements
fruits.set(1, "Mango");  // Replace "Banana" with "Mango"

// Removing elements
fruits.remove("Orange");  // Remove by object
fruits.remove(0);        // Remove by index

// Checking size
int size = fruits.size();  // 1

// Checking if list contains an element
boolean hasMango = fruits.contains("Mango");  // true
```

Karakteristik `ArrayList`:
- Pengaksesan cepat (O(1)) berdasarkan index
- Penambahan/penghapusan di akhir list cepat
- Penambahan/penghapusan di tengah list lambat (perlu menggeser elemen)
- Berbasis array: resize secara dinamis saat elemen ditambahkan

### LinkedList

`LinkedList` adalah implementasi `List` (dan juga `Deque`) yang menggunakan double-linked list untuk menyimpan elemen.

```java
// Creating a LinkedList
List<String> animals = new LinkedList<>();

// Adding elements
animals.add("Dog");
animals.add("Cat");
animals.add("Horse");

// LinkedList specific operations
LinkedList<String> linkedAnimals = (LinkedList<String>) animals;
linkedAnimals.addFirst("Lion");  // Add at the beginning
linkedAnimals.addLast("Tiger");  // Add at the end

// Retrieving elements
String first = linkedAnimals.getFirst();  // "Lion"
String last = linkedAnimals.getLast();    // "Tiger"

// Removing elements
linkedAnimals.removeFirst();  // Remove "Lion"
linkedAnimals.removeLast();   // Remove "Tiger"
```

Karakteristik `LinkedList`:
- Pengaksesan lambat (O(n)) berdasarkan index (perlu traversal)
- Penambahan/penghapusan di awal dan akhir list sangat cepat (O(1))
- Penambahan/penghapusan di tengah list cepat jika iterator sudah diposisikan
- Memerlukan lebih banyak memori karena menyimpan pointer ke elemen sebelumnya dan berikutnya

### Vector dan Stack

`Vector` adalah implementasi `List` yang mirip dengan `ArrayList` tetapi tersinkronisasi (thread-safe).

`Stack` adalah subclass dari `Vector` yang mengimplementasikan struktur data stack (LIFO - Last In, First Out).

```java
// Creating a Vector
List<Integer> vector = new Vector<>();
vector.add(1);
vector.add(2);
vector.add(3);

// Creating a Stack
Stack<Integer> stack = new Stack<>();
stack.push(1);  // Add to top
stack.push(2);
stack.push(3);

int top = stack.peek();  // Look at top element (3) without removing
int popped = stack.pop();  // Remove and return top element (3)
```

**Catatan**: `Vector` dan `Stack` adalah class lama yang tersedia sejak awal Java. Untuk aplikasi modern, lebih disarankan menggunakan `ArrayList` (dengan sinkronisasi eksplisit jika diperlukan) dan `ArrayDeque` sebagai pengganti `Stack`.

### Perbandingan Implementasi List

| Operasi | ArrayList | LinkedList | Vector |
|---------|-----------|------------|--------|
| Akses (get) | O(1) | O(n) | O(1) |
| Penambahan/penghapusan di awal | O(n) | O(1) | O(n) |
| Penambahan/penghapusan di akhir | O(1)* | O(1) | O(1)* |
| Penambahan/penghapusan di tengah | O(n) | O(1)** | O(n) |
| Thread Safety | Tidak | Tidak | Ya |
| Penggunaan Memori | Rendah | Tinggi | Rendah |

*Amortized O(1) - bisa menjadi O(n) jika resize diperlukan
**Jika iterator sudah diposisikan di tempat yang tepat

## Interface dan Implementasi Set

`Set` adalah collection yang tidak mengizinkan elemen duplikat. Interface ini memodelkan abstraksi himpunan matematika.

Operasi utama pada `Set`:
- Penambahan dan penghapusan: `add()`, `remove()`
- Query: `contains()`, `size()`, `isEmpty()`

### HashSet

`HashSet` adalah implementasi `Set` yang menggunakan hash table (HashMap) untuk penyimpanan. Ini tidak menjamin urutan elemen.

```java
// Creating a HashSet
Set<String> colors = new HashSet<>();

// Adding elements
colors.add("Red");
colors.add("Green");
colors.add("Blue");
colors.add("Red");  // Duplicate, will be ignored

// Checking size
int size = colors.size();  // 3, not 4 (duplicate not added)

// Checking if set contains an element
boolean hasGreen = colors.contains("Green");  // true

// Removing an element
colors.remove("Blue");

// Iterating over set
for (String color : colors) {
    System.out.println(color);  // No guaranteed order
}
```

Karakteristik `HashSet`:
- Sangat cepat untuk operasi dasar (add, remove, contains) - O(1) dalam kasus rata-rata
- Tidak menjamin urutan elemen
- Memungkinkan satu elemen null
- Tidak thread-safe

### LinkedHashSet

`LinkedHashSet` adalah subclass dari `HashSet` yang mempertahankan insertion order dengan menggunakan linked list.

```java
// Creating a LinkedHashSet
Set<String> fruits = new LinkedHashSet<>();

// Adding elements
fruits.add("Apple");
fruits.add("Banana");
fruits.add("Orange");

// Iterating will maintain insertion order
for (String fruit : fruits) {
    System.out.println(fruit);  // "Apple", "Banana", "Orange" in this order
}
```

Karakteristik `LinkedHashSet`:
- Sama seperti `HashSet` tetapi mempertahankan insertion order
- Performa sedikit lebih lambat daripada `HashSet` karena overhead linked list
- Berguna ketika Anda memerlukan kombinasi dari pencarian cepat dan urutan iterasi yang terprediksi

### TreeSet

`TreeSet` adalah implementasi `SortedSet` yang menyimpan elemen dalam sorted order (menggunakan red-black tree).

```java
// Creating a TreeSet
SortedSet<String> names = new TreeSet<>();

// Adding elements
names.add("Charlie");
names.add("Alice");
names.add("Bob");

// Iterating will be in sorted order
for (String name : names) {
    System.out.println(name);  // "Alice", "Bob", "Charlie" in alphabetical order
}

// SortedSet specific operations
String first = names.first();  // "Alice"
String last = names.last();    // "Charlie"

// Subset operations
SortedSet<String> subset = names.headSet("Bob");  // Names less than "Bob": "Alice"
SortedSet<String> tailSet = names.tailSet("Bob");  // Names >= "Bob": "Bob", "Charlie"
```

Karakteristik `TreeSet`:
- Elemen selalu disimpan dalam sorted order (natural ordering atau dengan Comparator)
- Operasi dasar (add, remove, contains) adalah O(log n)
- Menyediakan operasi navigasi tambahan (first, last, headSet, tailSet)
- Tidak mengizinkan elemen null
- Tidak thread-safe

### Perbandingan Implementasi Set

| Operasi | HashSet | LinkedHashSet | TreeSet |
|---------|---------|---------------|---------|
| Urutan | Tidak Dijamin | Insertion Order | Sorted Order |
| add/remove/contains | O(1) | O(1) | O(log n) |
| Operasi Navigasi | Tidak | Tidak | Ya |
| Elemen Null | Satu Diperbolehkan | Satu Diperbolehkan | Tidak Diperbolehkan |
| Thread Safety | Tidak | Tidak | Tidak |

## Interface dan Implementasi Queue

`Queue` adalah collection yang dirancang untuk memegang elemen sebelum pemrosesan. Queue typically mengikuti urutan FIFO (First-In-First-Out).

Operasi utama pada `Queue`:
- Insertion: `add(e)`, `offer(e)` (lebih disukai, tidak throw exception jika queue penuh)
- Removal: `remove()`, `poll()` (lebih disukai, returns null jika queue kosong)
- Examination: `element()`, `peek()` (lebih disukai, returns null jika queue kosong)

### PriorityQueue

`PriorityQueue` adalah implementasi `Queue` yang menyimpan elemen berdasarkan prioritas mereka (natural ordering atau Comparator).

```java
// Creating a PriorityQueue with natural ordering
Queue<Integer> numbers = new PriorityQueue<>();

// Adding elements
numbers.offer(5);
numbers.offer(2);
numbers.offer(8);
numbers.offer(1);

// Retrieving and removing elements
while (!numbers.isEmpty()) {
    System.out.println(numbers.poll());  // Will print: 1, 2, 5, 8
}

// Creating a PriorityQueue with custom ordering (largest first)
Queue<Integer> reversedNumbers = new PriorityQueue<>(Comparator.reverseOrder());
reversedNumbers.offer(5);
reversedNumbers.offer(2);
reversedNumbers.offer(8);
reversedNumbers.offer(1);

// Retrieving and removing elements
while (!reversedNumbers.isEmpty()) {
    System.out.println(reversedNumbers.poll());  // Will print: 8, 5, 2, 1
}
```

Karakteristik `PriorityQueue`:
- Elemen diproses berdasarkan prioritas (terkecil/terendah terlebih dahulu secara default)
- Tidak dijamin urutan elemen dengan prioritas yang sama
- Tidak thread-safe
- Tidak mengizinkan elemen null
- Operasi add, remove, peek memiliki kompleksitas O(log n)

### Deque dan ArrayDeque

`Deque` (double-ended queue) adalah queue yang mendukung penambahan dan pengambilan elemen dari kedua ujungnya.

`ArrayDeque` adalah implementasi `Deque` yang menggunakan array resizable.

```java
// Creating an ArrayDeque
Deque<String> deque = new ArrayDeque<>();

// Adding elements to both ends
deque.addFirst("First");
deque.addLast("Last");

// Peeking at elements from both ends
String first = deque.peekFirst();  // "First"
String last = deque.peekLast();    // "Last"

// Removing elements from both ends
String removedFirst = deque.removeFirst();  // "First"
String removedLast = deque.removeLast();    // "Last"

// Using as a stack (LIFO)
Deque<String> stack = new ArrayDeque<>();
stack.push("A");  // Same as addFirst()
stack.push("B");
stack.push("C");

while (!stack.isEmpty()) {
    System.out.println(stack.pop());  // Same as removeFirst(), will print: C, B, A
}

// Using as a queue (FIFO)
Deque<String> queue = new ArrayDeque<>();
queue.offer("A");  // Same as addLast()
queue.offer("B");
queue.offer("C");

while (!queue.isEmpty()) {
    System.out.println(queue.poll());  // Same as removeFirst(), will print: A, B, C
}
```

Karakteristik `ArrayDeque`:
- Lebih efisien dari `Stack` ketika digunakan sebagai stack
- Lebih efisien dari `LinkedList` ketika digunakan sebagai queue
- Tidak thread-safe
- Tidak mengizinkan elemen null
- Tidak memiliki batasan kapasitas (grows as needed)
- Performa baik untuk operasi di kedua ujung (O(1))

## Interface dan Implementasi Map

`Map` adalah objek yang memetakan key ke value, di mana sebuah map tidak dapat berisi key duplikat, dan setiap key memetakan ke paling banyak satu value.

Operasi utama pada `Map`:
- Basic operations: `put(key, value)`, `get(key)`, `remove(key)`
- Bulk operations: `putAll(map)`, `clear()`
- Collection views: `keySet()`, `values()`, `entrySet()`
- Query operations: `containsKey(key)`, `containsValue(value)`, `size()`, `isEmpty()`

### HashMap

`HashMap` adalah implementasi `Map` yang menggunakan hash table untuk penyimpanan. Ini adalah implementasi map yang paling banyak digunakan.

```java
// Creating a HashMap
Map<String, Integer> ages = new HashMap<>();

// Adding key-value pairs
ages.put("Alice", 25);
ages.put("Bob", 30);
ages.put("Charlie", 35);

// Retrieving values
int aliceAge = ages.get("Alice");  // 25
Integer davidAge = ages.get("David");  // null (key not found)

// Checking if key/value exists
boolean hasKey = ages.containsKey("Bob");      // true
boolean hasValue = ages.containsValue(40);     // false

// Updating values
ages.put("Alice", 26);  // Updates Alice's age

// Conditional put (only if key doesn't exist)
ages.putIfAbsent("Alice", 27);  // Won't change Alice's age (26)
ages.putIfAbsent("David", 40);  // Will add David with age 40

// Removing entries
ages.remove("Charlie");  // Removes Charlie's entry

// Getting default value if key not found
int eveAge = ages.getOrDefault("Eve", 0);  // 0 (default value)

// Iterating over keys
for (String name : ages.keySet()) {
    System.out.println(name);
}

// Iterating over values
for (int age : ages.values()) {
    System.out.println(age);
}

// Iterating over entries
for (Map.Entry<String, Integer> entry : ages.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}
```

Karakteristik `HashMap`:
- Sangat cepat untuk operasi dasar (put, get, remove) - O(1) dalam kasus rata-rata
- Tidak menjamin urutan key
- Memungkinkan satu key null dan banyak value null
- Tidak thread-safe

### LinkedHashMap

`LinkedHashMap` adalah subclass dari `HashMap` yang mempertahankan urutan insertion dengan menggunakan linked list.

```java
// Creating a LinkedHashMap (maintains insertion order)
Map<String, String> capitals = new LinkedHashMap<>();

// Adding key-value pairs
capitals.put("USA", "Washington DC");
capitals.put("UK", "London");
capitals.put("Japan", "Tokyo");

// Iterating will maintain insertion order
for (Map.Entry<String, String> entry : capitals.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
    // Will print in order: USA: Washington DC, UK: London, Japan: Tokyo
}
```

Karakteristik `LinkedHashMap`:
- Sama seperti `HashMap` tetapi mempertahankan insertion order key
- Performa sedikit lebih lambat daripada `HashMap` karena overhead linked list
- Dapat dikonfigurasi untuk mempertahankan access order (LRU cache)

### TreeMap

`TreeMap` adalah implementasi `SortedMap` yang menyimpan key dalam sorted order.

```java
// Creating a TreeMap (keys are sorted)
SortedMap<String, Double> grades = new TreeMap<>();

// Adding key-value pairs
grades.put("Charlie", 85.6);
grades.put("Alice", 90.5);
grades.put("Bob", 78.2);

// Iterating will be in sorted key order
for (Map.Entry<String, Double> entry : grades.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
    // Will print in order: Alice: 90.5, Bob: 78.2, Charlie: 85.6
}

// SortedMap specific operations
String firstStudent = grades.firstKey();  // "Alice"
String lastStudent = grades.lastKey();    // "Charlie"

// Subset operations
SortedMap<String, Double> subGrades = grades.headMap("Bob");  // Students before "Bob": "Alice"
SortedMap<String, Double> tailGrades = grades.tailMap("Bob");  // Students from "Bob": "Bob", "Charlie"
```

Karakteristik `TreeMap`:
- Key selalu disimpan dalam sorted order (natural ordering atau dengan Comparator)
- Operasi dasar (put, get, remove) adalah O(log n)
- Menyediakan operasi navigasi tambahan (firstKey, lastKey, headMap, tailMap)
- Tidak mengizinkan key null
- Tidak thread-safe

### Hashtable

`Hashtable` adalah implementasi `Map` lama yang mirip dengan `HashMap` tetapi synchronized (thread-safe).

```java
// Creating a Hashtable (thread-safe)
Map<Integer, String> employees = new Hashtable<>();

// Adding key-value pairs
employees.put(1001, "John Smith");
employees.put(1002, "Jane Doe");
employees.put(1003, "David Johnson");

// Basic operations work like other maps
String emp = employees.get(1002);  // "Jane Doe"
```

**Catatan**: `Hashtable` adalah class lama yang tersedia sejak awal Java. Untuk aplikasi modern, lebih disarankan menggunakan `HashMap` (dengan sinkronisasi eksplisit jika diperlukan) atau `ConcurrentHashMap` untuk thread safety.

### Perbandingan Implementasi Map

| Operasi | HashMap | LinkedHashMap | TreeMap | Hashtable |
|---------|---------|---------------|---------|-----------|
| Urutan | Tidak Dijamin | Insertion Order | Sorted Order | Tidak Dijamin |
| put/get/remove | O(1) | O(1) | O(log n) | O(1) |
| Operasi Navigasi | Tidak | Tidak | Ya | Tidak |
| Null Key/Value | Ya | Ya | Hanya Null Value | Tidak |
| Thread Safety | Tidak | Tidak | Tidak | Ya |

## Traversal Collection

### Iterator dan Iterable

`Iterator` adalah interface yang menyediakan metode untuk traversal collection secara sekuensial. Setiap collection yang implementasi `Iterable` (seperti semua collection standard) dapat menghasilkan `Iterator`.

```java
// Using iterator to traverse a List
List<String> names = new ArrayList<>();
names.add("Alice");
names.add("Bob");
names.add("Charlie");

Iterator<String> iterator = names.iterator();
while (iterator.hasNext()) {
    String name = iterator.next();
    System.out.println(name);
    
    // We can also remove elements during iteration
    if (name.equals("Bob")) {
        iterator.remove();  // Safely removes current element
    }
}

// Using ListIterator for bidirectional traversal
ListIterator<String> listIterator = names.listIterator();
while (listIterator.hasNext()) {
    int index = listIterator.nextIndex();
    String name = listIterator.next();
    System.out.println(index + ": " + name);
}

// Backwards traversal
while (listIterator.hasPrevious()) {
    int index = listIterator.previousIndex();
    String name = listIterator.previous();
    System.out.println(index + ": " + name);
}
```

**Penting**: Ketika menggunakan iterasi dan modifikasi bersamaan, selalu gunakan `iterator.remove()` untuk menghapus elemen. Mencoba memodifikasi collection secara langsung selama iterasi bisa menyebabkan `ConcurrentModificationException`.

### Enhanced for-loop

Enhanced for-loop (for-each loop) adalah cara yang lebih simpel untuk traversal collection yang mengimplementasi `Iterable`.

```java
// Using enhanced for-loop with List
List<String> colors = Arrays.asList("Red", "Green", "Blue");
for (String color : colors) {
    System.out.println(color);
}

// Using enhanced for-loop with Set
Set<Integer> numbers = new HashSet<>(Arrays.asList(1, 2, 3, 4, 5));
for (int number : numbers) {
    System.out.println(number);
}

// Using enhanced for-loop with Map entrySet
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 95);
scores.put("Bob", 87);
scores.put("Charlie", 92);

for (Map.Entry<String, Integer> entry : scores.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}

// Using enhanced for-loop with Map keySet
for (String name : scores.keySet()) {
    System.out.println(name + ": " + scores.get(name));
}
```

**Catatan**: Enhanced for-loop tidak memungkinkan Anda untuk memodifikasi collection selama iterasi.

### forEach() dengan Lambda (Java 8+)

Java 8 memperkenalkan method `forEach()` di `Iterable` yang bekerja dengan lambda expressions atau method references.

```java
// Using forEach with lambda expression
List<String> fruits = Arrays.asList("Apple", "Banana", "Orange");
fruits.forEach(fruit -> System.out.println(fruit));

// Using forEach with method reference
fruits.forEach(System.out::println);

// Using forEach with Maps
Map<String, Integer> ages = new HashMap<>();
ages.put("Alice", 25);
ages.put("Bob", 30);
ages.put("Charlie", 35);

ages.forEach((name, age) -> System.out.println(name + " is " + age + " years old"));
```

## Manipulasi Data dalam Collection

### Menambah dan Menghapus Elemen

```java
// Adding to Lists
List<String> fruits = new ArrayList<>();
fruits.add("Apple");             // Adds at the end
fruits.add(0, "Banana");         // Adds at specific index
fruits.addAll(Arrays.asList("Cherry", "Date"));  // Adds all elements from another collection

// Removing from Lists
fruits.remove("Apple");          // Removes first occurrence of object
fruits.remove(0);                // Removes element at index
fruits.removeAll(Arrays.asList("Cherry", "Date"));  // Removes all elements that are in the specified collection
fruits.clear();                  // Removes all elements

// Adding to Sets
Set<Integer> numbers = new HashSet<>();
numbers.add(1);                  // Adds element if not present
numbers.addAll(Arrays.asList(2, 3, 4));  // Adds all elements from another collection

// Removing from Sets
numbers.remove(3);               // Removes element if present
numbers.removeIf(n -> n % 2 == 0);  // Removes elements that satisfy the predicate (Java 8+)

// Adding to Maps
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 95);         // Associates key with value
scores.putIfAbsent("Bob", 87);   // Associates key with value if key not present
scores.putAll(Collections.singletonMap("Charlie", 92));  // Adds all mappings from another map

// Removing from Maps
scores.remove("Alice");          // Removes mapping for key
scores.remove("Bob", 87);        // Removes mapping only if key mapped to specified value
```

### Mencari dan Memeriksa Elemen

```java
// Checking for elements in Lists
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "Alice");
boolean hasName = names.contains("Bob");        // true
int firstIndex = names.indexOf("Alice");        // 0
int lastIndex = names.lastIndexOf("Alice");     // 3
boolean hasAll = names.containsAll(Arrays.asList("Alice", "Charlie"));  // true

// Checking for elements in Sets
Set<Integer> numbers = new HashSet<>(Arrays.asList(1, 2, 3, 4, 5));
boolean hasNumber = numbers.contains(3);        // true
boolean hasSubset = numbers.containsAll(Arrays.asList(1, 5));  // true

// Checking for elements in Maps
Map<String, Integer> ages = new HashMap<>();
ages.put("Alice", 25);
ages.put("Bob", 30);

boolean hasKey = ages.containsKey("Alice");     // true
boolean hasValue = ages.containsValue(30);      // true
Integer age = ages.get("Charlie");              // null (key not found)
Integer defaultAge = ages.getOrDefault("Charlie", 0);  // 0 (default value)
```

### Sorting dan Ordering

```java
// Sorting Lists with Collections.sort()
List<String> names = new ArrayList<>(Arrays.asList("Charlie", "Alice", "Bob"));

// Sort using natural ordering
Collections.sort(names);  // ["Alice", "Bob", "Charlie"]

// Sort using custom Comparator
Collections.sort(names, Collections.reverseOrder());  // ["Charlie", "Bob", "Alice"]

// Using List.sort() (Java 8+)
names.sort(String::compareToIgnoreCase);  // Case-insensitive sort

// Sorting with custom objects
List<Person> people = new ArrayList<>();
people.add(new Person("Charlie", 35));
people.add(new Person("Alice", 25));
people.add(new Person("Bob", 30));

// Sort by age
Collections.sort(people, Comparator.comparing(Person::getAge));

// Sort by name
people.sort(Comparator.comparing(Person::getName));

// Multiple sort criteria (Java 8+)
people.sort(Comparator.comparing(Person::getAge)
                     .thenComparing(Person::getName));

// Reversing order
List<Integer> numbers = Arrays.asList(5, 2, 8, 1, 7);
Collections.reverse(numbers);  // [7, 1, 8, 2, 5]

// Shuffling
List<Integer> cards = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5));
Collections.shuffle(cards);  // Random order
```

### Comparable vs Comparator

`Comparable` adalah interface yang didefinisikan pada class yang elemen-elemennya ingin diberikan "natural ordering".

`Comparator` adalah interface terpisah yang memungkinkan Anda untuk menentukan custom ordering tanpa memodifikasi class elemen.

```java
// Class implementing Comparable
public class Person implements Comparable<Person> {
    private String name;
    private int age;
    
    // Constructor, getters, setters...
    
    @Override
    public int compareTo(Person other) {
        // Compare by age (natural ordering)
        return Integer.compare(this.age, other.age);
    }
}

// Using a Comparator
Comparator<Person> byName = new Comparator<Person>() {
    @Override
    public int compare(Person p1, Person p2) {
        return p1.getName().compareTo(p2.getName());
    }
};

// Using Lambda for Comparator (Java 8+)
Comparator<Person> byName = (p1, p2) -> p1.getName().compareTo(p2.getName());

// Using method reference (Java 8+)
Comparator<Person> byName = Comparator.comparing(Person::getName);

// More complex comparison (Java 8+)
Comparator<Person> byAgeReversedThenName = Comparator.comparing(Person::getAge).reversed()
                                                    .thenComparing(Person::getName);
```

## Collections Utility Class

`Collections` adalah utility class yang berisi berbagai static method untuk manipulasi dan operasi pada collections.

### Method Berguna dalam Collections

```java
// Finding min and max
List<Integer> numbers = Arrays.asList(5, 2, 9, 1, 7);
int min = Collections.min(numbers);  // 1
int max = Collections.max(numbers);  // 9

// Finding min and max with Comparator
List<Person> people = getPeopleList();
Person youngest = Collections.min(people, Comparator.comparing(Person::getAge));
Person oldest = Collections.max(people, Comparator.comparing(Person::getAge));

// Frequency and disjoint
List<String> words = Arrays.asList("apple", "banana", "apple", "cherry");
int frequency = Collections.frequency(words, "apple");  // 2

List<String> fruits = Arrays.asList("apple", "banana");
List<String> colors = Arrays.asList("red", "green");
boolean disjoint = Collections.disjoint(fruits, colors);  // true (no common elements)

// Rotating and swapping
List<Integer> list = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5));
Collections.rotate(list, 2);  // [4, 5, 1, 2, 3]
Collections.swap(list, 0, 2);  // [1, 5, 4, 2, 3]

// Fill and copy
List<Integer> source = Arrays.asList(10, 20, 30);
List<Integer> dest = Arrays.asList(0, 0, 0, 0, 0);
Collections.copy(dest, source);  // dest = [10, 20, 30, 0, 0]

List<String> fillList = new ArrayList<>(Arrays.asList("a", "b", "c"));
Collections.fill(fillList, "X");  // fillList = ["X", "X", "X"]

// Binary search (list must be sorted)
List<Integer> sortedList = Arrays.asList(10, 20, 30, 40, 50);
int index = Collections.binarySearch(sortedList, 30);  // 2
```

### Unmodifiable Collections

`Collections` menyediakan method untuk membuat unmodifiable views dari collections. Ini berguna untuk defensive programming dan ensuring immutability.

```java
// Unmodifiable views
List<String> originalList = new ArrayList<>(Arrays.asList("a", "b", "c"));
List<String> readOnlyList = Collections.unmodifiableList(originalList);

// Any attempt to modify will throw UnsupportedOperationException
// readOnlyList.add("d");  // This would throw exception

// Other unmodifiable views
Set<Integer> readOnlySet = Collections.unmodifiableSet(new HashSet<>(Arrays.asList(1, 2, 3)));
Map<String, Integer> readOnlyMap = Collections.unmodifiableMap(new HashMap<String, Integer>() {{
    put("one", 1);
    put("two", 2);
}});

// Creating empty unmodifiable collections
List<Object> emptyList = Collections.emptyList();
Set<Object> emptySet = Collections.emptySet();
Map<Object, Object> emptyMap = Collections.emptyMap();

// Creating singleton collections
Set<String> singletonSet = Collections.singleton("element");
List<Integer> singletonList = Collections.singletonList(42);
Map<String, Integer> singletonMap = Collections.singletonMap("key", 100);
```

**Penting**: Perubahan pada original collection akan tercermin pada unmodifiable view.

### Synchronized Collections

`Collections` juga menyediakan method untuk membuat thread-safe versions dari collections.

```java
// Synchronized collections
List<String> syncList = Collections.synchronizedList(new ArrayList<>());
Set<Integer> syncSet = Collections.synchronizedSet(new HashSet<>());
Map<String, Double> syncMap = Collections.synchronizedMap(new HashMap<>());

// Safe to use across multiple threads
synchronized (syncList) {
    // Multiple operations on syncList
    for (String item : syncList) {
        // ...
    }
}
```

**Catatan**: Untuk aplikasi concurrent modern, lebih disarankan menggunakan collections dari package `java.util.concurrent` seperti `ConcurrentHashMap` dan `CopyOnWriteArrayList`.

## Collections Framework dan Generics

### Type Safety dengan Generics

Generics memungkinkan collections untuk ditype secara strongly, membantu menghindari ClassCastException dan memperkuat compile-time type checking.

```java
// Without generics (pre-Java 5)
List names = new ArrayList();
names.add("Alice");
names.add(42);  // Legal but problematic

// Runtime error when trying to cast
for (Object obj : names) {
    String name = (String) obj;  // ClassCastException for the Integer
}

// With generics (Java 5+)
List<String> safeNames = new ArrayList<>();
safeNames.add("Alice");
// safeNames.add(42);  // Compile error - type safety enforced

// No casting needed, no runtime type errors
for (String name : safeNames) {
    System.out.println(name.toUpperCase());  // Safe to call String methods
}

// Generic methods
public <T> void printList(List<T> list) {
    for (T item : list) {
        System.out.println(item);
    }
}

// Using with custom objects
List<Person> people = new ArrayList<>();
people.add(new Person("Alice", 25));

// Type-safe operations
for (Person person : people) {
    System.out.println(person.getName());  // Type-safe, no casting needed
}
```

### Wildcard dalam Generics

Wildcards memungkinkan fleksibilitas ketika bekerja dengan generic types.

```java
// Unbounded wildcard (?)
public void processElements(List<?> elements) {
    for (Object o : elements) {
        System.out.println(o);
    }
}

// Upper bounded wildcard (? extends Type)
public double sumNumbers(List<? extends Number> numbers) {
    double sum = 0.0;
    for (Number number : numbers) {
        sum += number.doubleValue();
    }
    return sum;
}

// This can accept List<Integer>, List<Double>, etc.
List<Integer> integers = Arrays.asList(1, 2, 3);
List<Double> doubles = Arrays.asList(1.1, 2.2, 3.3);
double sum1 = sumNumbers(integers);  // Valid
double sum2 = sumNumbers(doubles);   // Valid

// Lower bounded wildcard (? super Type)
public void addNumbers(List<? super Integer> list) {
    list.add(1);
    list.add(2);
    list.add(3);
}

// This can accept List<Integer>, List<Number>, List<Object>, etc.
List<Integer> intList = new ArrayList<>();
List<Number> numList = new ArrayList<>();
addNumbers(intList);  // Valid
addNumbers(numList);  // Valid
```

**PECS Principle** (Producer Extends, Consumer Super):
- Use `<? extends T>` when you only get values from a structure (producer)
- Use `<? super T>` when you only put values into a structure (consumer)
- Use no wildcard when you both get and put values

## Best Practices

1. **Pilih Implementasi yang Tepat**: 
   - Use `ArrayList` untuk random access dan operasi di akhir list
   - Use `LinkedList` untuk frequent insertions/deletions di awal/akhir
   - Use `HashSet` untuk fast lookups tanpa urutan
   - Use `TreeSet` untuk ordered elements
   - Use `HashMap` untuk fast key-value lookups

2. **Gunakan Interface sebagai Tipe Variabel**:
   ```java
   // Better (programming to interface)
   List<String> names = new ArrayList<>();
   Map<String, Integer> scores = new HashMap<>();
   
   // Rather than concrete implementation
   ArrayList<String> names = new ArrayList<>();
   HashMap<String, Integer> scores = new HashMap<>();
   ```

3. **Specify Kapasitas Awal jika Diketahui**:
   ```java
   // More efficient if size is known
   List<String> names = new ArrayList<>(1000);
   Map<String, Double> values = new HashMap<>(500, 0.75f);
   ```

4. **Ukuran yang Tepat untuk Collection**:
   - Jangan memilih collection yang jauh lebih besar dari yang Anda butuhkan
   - Pertimbangkan memory footprint dan performa

5. **Hindari Modifikasi Collection selama Iterasi**:
   ```java
   // Bad - could throw ConcurrentModificationException
   for (String item : list) {
       if (someCondition(item)) {
           list.remove(item);  // Danger!
       }
   }
   
   // Good - using Iterator's remove method
   Iterator<String> iterator = list.iterator();
   while (iterator.hasNext()) {
       if (someCondition(iterator.next())) {
           iterator.remove();  // Safe
       }
   }
   
   // Alternative using removeIf (Java 8+)
   list.removeIf(item -> someCondition(item));
   ```

6. **Implementasikan equals() dan hashCode() dengan Benar**:
   ```java
   public class Person {
       private String name;
       private int age;
       
       // Constructor, getters, setters...
       
       @Override
       public boolean equals(Object o) {
           if (this == o) return true;
           if (o == null || getClass() != o.getClass()) return false;
           Person person = (Person) o;
           return age == person.age && Objects.equals(name, person.name);
       }
       
       @Override
       public int hashCode() {
           return Objects.hash(name, age);
       }
   }
   ```

7. **Gunakan Stream API untuk Operasi Kompleks** (Java 8+):
   ```java
   // Filtering and mapping using Stream API
   List<String> filteredNames = people.stream()
                                     .filter(p -> p.getAge() > 18)
                                     .map(Person::getName)
                                     .collect(Collectors.toList());
   ```

8. **Pertimbangkan Thread Safety**:
   - Gunakan collections dari `java.util.concurrent` untuk aplikasi multithreaded
   - Gunakan unmodifiable collections untuk defensive programming
   - Synchronize akses ke collections shareable jika diperlukan

9. **Gunakan Factory Methods untuk Collection Creation** (Java 9+):
   ```java
   // Java 9+ immutable collection factory methods
   List<String> list = List.of("a", "b", "c");
   Set<Integer> set = Set.of(1, 2, 3);
   Map<String, Integer> map = Map.of("one", 1, "two", 2);
   ```

10. **Pertimbangkan Memory dan Performance**:
    - `EnumSet` dan `EnumMap` untuk collections of enum types
    - `ArrayDeque` daripada `Stack` untuk stack operations
    - `LinkedHashMap` dengan access-order untuk simple LRU cache

## Latihan Praktik dengan NetBeans

Mari kita praktikkan Collections Framework dengan membuat aplikasi sederhana untuk manajemen perpustakaan di NetBeans.

### Langkah 1: Buat Project Baru

1. Buka NetBeans
2. Pilih `File > New Project`
3. Pilih `Java with Ant > Java Application`
4. Beri nama project `LibraryManagementSystem` dan klik `Finish`

### Langkah 2: Buat Model Class

1. Buat class `Book`:

```java
package librarymanagementsystem;

import java.time.LocalDate;
import java.util.Objects;

public class Book implements Comparable<Book> {
    private String isbn;
    private String title;
    private String author;
    private String category;
    private LocalDate publishDate;
    private boolean available;
    
    public Book(String isbn, String title, String author, String category, LocalDate publishDate) {
        this.isbn = isbn;
        this.title = title;
        this.author = author;
        this.category = category;
        this.publishDate = publishDate;
        this.available = true;
    }
    
    // Getters and setters
    public String getIsbn() {
        return isbn;
    }
    
    public String getTitle() {
        return title;
    }
    
    public void setTitle(String title) {
        this.title = title;
    }
    
    public String getAuthor() {
        return author;
    }
    
    public void setAuthor(String author) {
        this.author = author;
    }
    
    public String getCategory() {
        return category;
    }
    
    public void setCategory(String category) {
        this.category = category;
    }
    
    public LocalDate getPublishDate() {
        return publishDate;
    }
    
    public void setPublishDate(LocalDate publishDate) {
        this.publishDate = publishDate;
    }
    
    public boolean isAvailable() {
        return available;
    }
    
    public void setAvailable(boolean available) {
        this.available = available;
    }
    
    // Natural ordering by title
    @Override
    public int compareTo(Book other) {
        return this.title.compareTo(other.title);
    }
    
    // Proper equals and hashCode implementation
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Book book = (Book) o;
        return Objects.equals(isbn, book.isbn);
    }
    
    @Override
    public int hashCode() {
        return Objects.hash(isbn);
    }
    
    @Override
    public String toString() {
        return "Book{" +
                "isbn='" + isbn + '\'' +
                ", title='" + title + '\'' +
                ", author='" + author + '\'' +
                ", category='" + category + '\'' +
                ", publishDate=" + publishDate +
                ", available=" + available +
                '}';
    }
}
```

2. Buat class `Member`:

```java
package librarymanagementsystem;

import java.util.HashSet;
import java.util.Objects;
import java.util.Set;

public class Member {
    private String id;
    private String name;
    private String email;
    private Set<Book> borrowedBooks;
    
    public Member(String id, String name, String email) {
        this.id = id;
        this.name = name;
        this.email = email;
        this.borrowedBooks = new HashSet<>();
    }
    
    // Getters and setters
    public String getId() {
        return id;
    }
    
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
    
    public String getEmail() {
        return email;
    }
    
    public void setEmail(String email) {
        this.email = email;
    }
    
    public Set<Book> getBorrowedBooks() {
        return new HashSet<>(borrowedBooks);  // Return defensive copy
    }
    
    // Borrowing operations
    public boolean borrowBook(Book book) {
        if (book.isAvailable()) {
            book.setAvailable(false);
            return borrowedBooks.add(book);
        }
        return false;
    }
    
    public boolean returnBook(Book book) {
        if (borrowedBooks.contains(book)) {
            book.setAvailable(true);
            return borrowedBooks.remove(book);
        }
        return false;
    }
    
    public int getBorrowedCount() {
        return borrowedBooks.size();
    }
    
    // Proper equals and hashCode implementation
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Member member = (Member) o;
        return Objects.equals(id, member.id);
    }
    
    @Override
    public int hashCode() {
        return Objects.hash(id);
    }
    
    @Override
    public String toString() {
        return "Member{" +
                "id='" + id + '\'' +
                ", name='" + name + '\'' +
                ", email='" + email + '\'' +
                ", borrowedBooks=" + borrowedBooks.size() +
                '}';
    }
}
```

### Langkah 3: Buat Library Service Class

```java
package librarymanagementsystem;

import java.time.LocalDate;
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.HashMap;
import java.util.HashSet;
import java.util.LinkedHashMap;
import java.util.List;
import java.util.Map;
import java.util.Set;
import java.util.TreeSet;
import java.util.stream.Collectors;

public class LibraryService {
    private Map<String, Book> booksByIsbn;           // Fast lookup by ISBN
    private Map<String, Member> membersById;         // Fast lookup by member ID
    private Map<String, Set<Book>> booksByCategory;  // Group books by category
    private Set<Book> allBooks;                      // Set of all unique books
    
    public LibraryService() {
        booksByIsbn = new HashMap<>();
        membersById = new HashMap<>();
        booksByCategory = new HashMap<>();
        allBooks = new HashSet<>();
    }
    
    // Book operations
    public boolean addBook(Book book) {
        if (booksByIsbn.containsKey(book.getIsbn())) {
            return false;  // Book with this ISBN already exists
        }
        
        booksByIsbn.put(book.getIsbn(), book);
        allBooks.add(book);
        
        // Add to category map
        booksByCategory.computeIfAbsent(book.getCategory(), k -> new HashSet<>()).add(book);
        
        return true;
    }
    
    public Book findBookByIsbn(String isbn) {
        return booksByIsbn.get(isbn);
    }
    
    public List<Book> findBooksByTitle(String titleFragment) {
        return booksByIsbn.values().stream()
                .filter(book -> book.getTitle().toLowerCase().contains(titleFragment.toLowerCase()))
                .collect(Collectors.toList());
    }
    
    public Set<Book> getBooksByCategory(String category) {
        return booksByCategory.getOrDefault(category, Collections.emptySet());
    }
    
    public List<Book> getAllBooksAsList() {
        return new ArrayList<>(allBooks);
    }
    
    public Set<Book> getAllBooksAsSet() {
        return new HashSet<>(allBooks);
    }
    
    public Set<Book> getAllBooksSortedByTitle() {
        // Using TreeSet with natural ordering (by title)
        return new TreeSet<>(allBooks);
    }
    
    public List<Book> getAllBooksSortedByAuthor() {
        List<Book> books = new ArrayList<>(allBooks);
        books.sort(Comparator.comparing(Book::getAuthor));
        return books;
    }
    
    public List<Book> getAllAvailableBooks() {
        return booksByIsbn.values().stream()
                .filter(Book::isAvailable)
                .collect(Collectors.toList());
    }
    
    public boolean removeBook(String isbn) {
        Book book = booksByIsbn.get(isbn);
        if (book == null) {
            return false;
        }
        
        // Remove from all collections
        booksByIsbn.remove(isbn);
        allBooks.remove(book);
        Set<Book> categoryBooks = booksByCategory.get(book.getCategory());
        if (categoryBooks != null) {
            categoryBooks.remove(book);
        }
        
        return true;
    }
    
    // Member operations
    public boolean addMember(Member member) {
        if (membersById.containsKey(member.getId())) {
            return false;  // Member with this ID already exists
        }
        
        membersById.put(member.getId(), member);
        return true;
    }
    
    public Member findMemberById(String id) {
        return membersById.get(id);
    }
    
    public List<Member> getAllMembers() {
        return new ArrayList<>(membersById.values());
    }
    
    public boolean removeMember(String id) {
        Member member = membersById.get(id);
        if (member == null) {
            return false;
        }
        
        // Check if member has borrowed books
        if (member.getBorrowedCount() > 0) {
            return false;  // Cannot remove member with borrowed books
        }
        
        membersById.remove(id);
        return true;
    }
    
    // Borrowing operations
    public boolean borrowBook(String memberId, String isbn) {
        Member member = membersById.get(memberId);
        Book book = booksByIsbn.get(isbn);
        
        if (member == null || book == null) {
            return false;
        }
        
        return member.borrowBook(book);
    }
    
    public boolean returnBook(String memberId, String isbn) {
        Member member = membersById.get(memberId);
        Book book = booksByIsbn.get(isbn);
        
        if (member == null || book == null) {
            return false;
        }
        
        return member.returnBook(book);
    }
    
    // Statistics operations
    public Map<String, Integer> getBookCountByCategory() {
        Map<String, Integer> result = new LinkedHashMap<>();
        
        for (Map.Entry<String, Set<Book>> entry : booksByCategory.entrySet()) {
            result.put(entry.getKey(), entry.getValue().size());
        }
        
        return result;
    }
    
    public Member getMemberWithMostBooks() {
        return membersById.values().stream()
                .max(Comparator.comparing(Member::getBorrowedCount))
                .orElse(null);
    }
    
    public List<Book> getRecentlyAddedBooks(int count) {
        return booksByIsbn.values().stream()
                .sorted(Comparator.comparing(Book::getPublishDate).reversed())
                .limit(count)
                .collect(Collectors.toList());
    }
    
    // Demo data initialization
    public void initializeWithDemoData() {
        // Add some books
        addBook(new Book("978-0134685991", "Effective Java", "Joshua Bloch", "Programming", 
                         LocalDate.of(2018, 1, 6)));
        addBook(new Book("978-0596009205", "Head First Design Patterns", "Eric Freeman", "Programming", 
                         LocalDate.of(2004, 10, 1)));
        addBook(new Book("978-0134757599", "Clean Architecture", "Robert C. Martin", "Programming", 
                         LocalDate.of(2017, 9, 10)));
        addBook(new Book("978-0062316097", "Sapiens: A Brief History of Humankind", "Yuval Noah Harari", "History", 
                         LocalDate.of(2015, 2, 10)));
        addBook(new Book("978-0553386790", "A Game of Thrones", "George R.R. Martin", "Fiction", 
                         LocalDate.of(2011, 3, 22)));
        addBook(new Book("978-0307474278", "The Da Vinci Code", "Dan Brown", "Fiction", 
                         LocalDate.of(2009, 3, 31)));
        addBook(new Book("978-0345391803", "The Hitchhiker's Guide to the Galaxy", "Douglas Adams", "Science Fiction", 
                         LocalDate.of(1995, 9, 27)));
        addBook(new Book("978-0062457714", "The Subtle Art of Not Giving a F*ck", "Mark Manson", "Self-Help", 
                         LocalDate.of(2016, 9, 13)));
        
        // Add some members
        addMember(new Member("M001", "John Smith", "john@example.com"));
        addMember(new Member("M002", "Jane Doe", "jane@example.com"));
        addMember(new Member("M003", "Bob Johnson", "bob@example.com"));
        
        // Simulate some borrowing
        borrowBook("M001", "978-0134685991");
        borrowBook("M001", "978-0596009205");
        borrowBook("M002", "978-0062316097");
        borrowBook("M003", "978-0345391803");
        borrowBook("M003", "978-0062457714");
    }
}
```

### Langkah 4: Buat Main Class

```java
package librarymanagementsystem;

import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.util.Comparator;
import java.util.List;
import java.util.Map;
import java.util.Scanner;
import java.util.Set;

public class LibraryManagementSystem {
    private static LibraryService libraryService = new LibraryService();
    private static Scanner scanner = new Scanner(System.in);
    private static DateTimeFormatter dateFormatter = DateTimeFormatter.ofPattern("yyyy-MM-dd");
    
    public static void main(String[] args) {
        System.out.println("===== Library Management System =====");
        System.out.println("Initializing system with demo data...");
        libraryService.initializeWithDemoData();
        
        boolean running = true;
        while (running) {
            displayMenu();
            try {
                int choice = Integer.parseInt(scanner.nextLine());
                
                switch (choice) {
                    case 1:
                        addBook();
                        break;
                    case 2:
                        searchBook();
                        break;
                    case 3:
                        displayAllBooks();
                        break;
                    case 4:
                        displayBooksByCategory();
                        break;
                    case 5:
                        addMember();
                        break;
                    case 6:
                        borrowBook();
                        break;
                    case 7:
                        returnBook();
                        break;
                    case 8:
                        displayStatistics();
                        break;
                    case 9:
                        sortAndFilterDemo();
                        break;
                    case 10:
                        unmodifiableCollectionDemo();
                        break;
                    case 0:
                        running = false;
                        System.out.println("Thank you for using the Library Management System. Goodbye!");
                        break;
                    default:
                        System.out.println("Invalid choice. Please try again.");
                }
            } catch (NumberFormatException e) {
                System.out.println("Please enter a valid number.");
            } catch (Exception e) {
                System.out.println("An error occurred: " + e.getMessage());
            }
            
            if (running) {
                System.out.println("\nPress Enter to continue...");
                scanner.nextLine();
            }
        }
    }
    
    private static void displayMenu() {
        System.out.println("\n===== MENU =====");
        System.out.println("1. Add Book");
        System.out.println("2. Search for Book");
        System.out.println("3. Display All Books");
        System.out.println("4. Display Books by Category");
        System.out.println("5. Add Member");
        System.out.println("6. Borrow Book");
        System.out.println("7. Return Book");
        System.out.println("8. Display Statistics");
        System.out.println("9. Sort and Filter Demo");
        System.out.println("10. Unmodifiable Collection Demo");
        System.out.println("0. Exit");
        System.out.print("Enter your choice: ");
    }
    
    private static void addBook() {
        System.out.println("\n----- Add Book -----");
        
        System.out.print("Enter ISBN: ");
        String isbn = scanner.nextLine();
        
        if (libraryService.findBookByIsbn(isbn) != null) {
            System.out.println("A book with this ISBN already exists.");
            return;
        }
        
        System.out.print("Enter Title: ");
        String title = scanner.nextLine();
        
        System.out.print("Enter Author: ");
        String author = scanner.nextLine();
        
        System.out.print("Enter Category: ");
        String category = scanner.nextLine();
        
        LocalDate publishDate;
        try {
            System.out.print("Enter Publish Date (yyyy-MM-dd): ");
            String dateStr = scanner.nextLine();
            publishDate = LocalDate.parse(dateStr, dateFormatter);
        } catch (Exception e) {
            System.out.println("Invalid date format. Using current date.");
            publishDate = LocalDate.now();
        }
        
        Book book = new Book(isbn, title, author, category, publishDate);
        boolean added = libraryService.addBook(book);
        
        if (added) {
            System.out.println("Book added successfully.");
        } else {
            System.out.println("Failed to add book.");
        }
    }
    
    private static void searchBook() {
        System.out.println("\n----- Search Book -----");
        System.out.println("1. Search by ISBN");
        System.out.println("2. Search by Title");
        System.out.print("Enter your choice: ");
        
        try {
            int choice = Integer.parseInt(scanner.nextLine());
            
            switch (choice) {
                case 1:
                    System.out.print("Enter ISBN: ");
                    String isbn = scanner.nextLine();
                    Book book = libraryService.findBookByIsbn(isbn);
                    
                    if (book != null) {
                        displayBookDetails(book);
                    } else {
                        System.out.println("Book not found.");
                    }
                    break;
                    
                case 2:
                    System.out.print("Enter title fragment: ");
                    String titleFragment = scanner.nextLine();
                    List<Book> books = libraryService.findBooksByTitle(titleFragment);
                    
                    if (!books.isEmpty()) {
                        System.out.println("Found " + books.size() + " books:");
                        for (Book b : books) {
                            displayBookDetails(b);
                            System.out.println("-----------------------");
                        }
                    } else {
                        System.out.println("No books found matching that title.");
                    }
                    break;
                    
                default:
                    System.out.println("Invalid choice.");
            }
        } catch (NumberFormatException e) {
            System.out.println("Please enter a valid number.");
        }
    }
    
    private static void displayAllBooks() {
        System.out.println("\n----- All Books -----");
        List<Book> books = libraryService.getAllBooksAsList();
        
        if (books.isEmpty()) {
            System.out.println("No books in the library.");
            return;
        }
        
        System.out.println("Total books: " + books.size());
        for (Book book : books) {
            System.out.println("ISBN: " + book.getIsbn() + ", Title: " + book.getTitle() + 
                             ", Author: " + book.getAuthor() + ", Available: " + 
                             (book.isAvailable() ? "Yes" : "No"));
        }
    }
    
    private static void displayBooksByCategory() {
        System.out.println("\n----- Books by Category -----");
        System.out.print("Enter category (or leave empty for all categories): ");
        String category = scanner.nextLine();
        
        if (category.isEmpty()) {
            Map<String, Integer> categoryCount = libraryService.getBookCountByCategory();
            System.out.println("Books by Category:");
            for (Map.Entry<String, Integer> entry : categoryCount.entrySet()) {
                System.out.println(entry.getKey() + ": " + entry.getValue() + " books");
            }
        } else {
            Set<Book> books = libraryService.getBooksByCategory(category);
            
            if (books.isEmpty()) {
                System.out.println("No books found in category: " + category);
                return;
            }
            
            System.out.println("Books in category '" + category + "':");
            for (Book book : books) {
                System.out.println("ISBN: " + book.getIsbn() + ", Title: " + book.getTitle() + 
                                 ", Author: " + book.getAuthor());
            }
        }
    }
    
    private static void addMember() {
        System.out.println("\n----- Add Member -----");
        
        System.out.print("Enter Member ID: ");
        String id = scanner.nextLine();
        
        if (libraryService.findMemberById(id) != null) {
            System.out.println("A member with this ID already exists.");
            return;
        }
        
        System.out.print("Enter Name: ");
        String name = scanner.nextLine();
        
        System.out.print("Enter Email: ");
        String email = scanner.nextLine();
        
        Member member = new Member(id, name, email);
        boolean added = libraryService.addMember(member);
        
        if (added) {
            System.out.println("Member added successfully.");
        } else {
            System.out.println("Failed to add member.");
        }
    }
    
    private static void borrowBook() {
        System.out.println("\n----- Borrow Book -----");
        
        System.out.print("Enter Member ID: ");
        String memberId = scanner.nextLine();
        
        Member member = libraryService.findMemberById(memberId);
        if (member == null) {
            System.out.println("Member not found.");
            return;
        }
        
        System.out.print("Enter Book ISBN: ");
        String isbn = scanner.nextLine();
        
        Book book = libraryService.findBookByIsbn(isbn);
        if (book == null) {
            System.out.println("Book not found.");
            return;
        }
        
        boolean borrowed = libraryService.borrowBook(memberId, isbn);
        
        if (borrowed) {
            System.out.println("Book borrowed successfully.");
        } else {
            System.out.println("Failed to borrow book. It may not be available.");
        }
    }
    
    private static void returnBook() {
        System.out.println("\n----- Return Book -----");
        
        System.out.print("Enter Member ID: ");
        String memberId = scanner.nextLine();
        
        Member member = libraryService.findMemberById(memberId);
        if (member == null) {
            System.out.println("Member not found.");
            return;
        }
        
        System.out.print("Enter Book ISBN: ");
        String isbn = scanner.nextLine();
        
        Book book = libraryService.findBookByIsbn(isbn);
        if (book == null) {
            System.out.println("Book not found.");
            return;
        }
        
        boolean returned = libraryService.returnBook(memberId, isbn);
        
        if (returned) {
            System.out.println("Book returned successfully.");
        } else {
            System.out.println("Failed to return book. The member may not have borrowed this book.");
        }
    }
    
    private static void displayStatistics() {
        System.out.println("\n----- Library Statistics -----");
        
        List<Book> allBooks = libraryService.getAllBooksAsList();
        List<Book> availableBooks = libraryService.getAllAvailableBooks();
        List<Member> allMembers = libraryService.getAllMembers();
        
        System.out.println("Total Books: " + allBooks.size());
        System.out.println("Available Books: " + availableBooks.size());
        System.out.println("Borrowed Books: " + (allBooks.size() - availableBooks.size()));
        System.out.println("Total Members: " + allMembers.size());
        
        Map<String, Integer> booksByCategory = libraryService.getBookCountByCategory();
        System.out.println("\nBooks by Category:");
        for (Map.Entry<String, Integer> entry : booksByCategory.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
        
        Member topBorrower = libraryService.getMemberWithMostBooks();
        if (topBorrower != null) {
            System.out.println("\nMember with Most Borrowed Books: " + 
                             topBorrower.getName() + " (" + topBorrower.getBorrowedCount() + " books)");
        }
        
        List<Book> recentBooks = libraryService.getRecentlyAddedBooks(3);
        System.out.println("\nRecently Added Books:");
        for (Book book : recentBooks) {
            System.out.println(book.getTitle() + " by " + book.getAuthor() + 
                             " (" + book.getPublishDate() + ")");
        }
    }
    
    private static void sortAndFilterDemo() {
        System.out.println("\n----- Sort and Filter Demonstration -----");
        
        List<Book> allBooks = libraryService.getAllBooksAsList();
        
        System.out.println("\n1. Books Sorted by Title (Natural Ordering):");
        Set<Book> booksByTitle = libraryService.getAllBooksSortedByTitle();
        for (Book book : booksByTitle) {
            System.out.println(book.getTitle() + " by " + book.getAuthor());
        }
        
        System.out.println("\n2. Books Sorted by Author:");
        List<Book> booksByAuthor = libraryService.getAllBooksSortedByAuthor();
        for (Book book : booksByAuthor) {
            System.out.println(book.getAuthor() + " - " + book.getTitle());
        }
        
        System.out.println("\n3. Books Sorted by Publish Date (Newest First):");
        List<Book> booksCopy = libraryService.getAllBooksAsList();
        booksCopy.sort(Comparator.comparing(Book::getPublishDate).reversed());
        for (Book book : booksCopy) {
            System.out.println(book.getPublishDate() + " - " + book.getTitle());
        }
        
        System.out.println("\n4. Available Books Only:");
        List<Book> availableBooks = libraryService.getAllAvailableBooks();
        for (Book book : availableBooks) {
            System.out.println(book.getTitle() + " - Available: " + book.isAvailable());
        }
        
        // Java 8 Stream API demo
        System.out.println("\n5. Stream API - Books by Specific Author:");
        String authorToSearch = "Douglas Adams";
        allBooks.stream()
                .filter(book -> book.getAuthor().equals(authorToSearch))
                .forEach(book -> System.out.println(book.getTitle()));
        
        System.out.println("\n6. Stream API - Books Published After 2010:");
        LocalDate cutoffDate = LocalDate.of(2010, 1, 1);
        allBooks.stream()
                .filter(book -> book.getPublishDate().isAfter(cutoffDate))
                .sorted(Comparator.comparing(Book::getPublishDate))
                .forEach(book -> System.out.println(book.getPublishDate() + " - " + book.getTitle()));
    }
    
    private static void unmodifiableCollectionDemo() {
        System.out.println("\n----- Unmodifiable Collection Demonstration -----");
        
        Member member = libraryService.findMemberById("M001");
        if (member == null) {
            System.out.println("Member not found.");
            return;
        }
        
        System.out.println("Member: " + member.getName());
        
        Set<Book> borrowedBooks = member.getBorrowedBooks();  // This is a defensive copy
        System.out.println("Borrowed Books: " + borrowedBooks.size());
        
        try {
            System.out.println("\nAttempting to modify the returned set of borrowed books...");
            Book someBook = libraryService.findBookByIsbn("978-0134685991");
            borrowedBooks.remove(someBook);
            System.out.println("Modified successful (not expected behavior)");
        } catch (UnsupportedOperationException e) {
            System.out.println("Cannot modify - UnsupportedOperationException (expected behavior)");
        }
        
        // Check if the actual borrowed books were affected
        Set<Book> checkAgain = member.getBorrowedBooks();
        System.out.println("Borrowed Books after attempt: " + checkAgain.size());
        
        System.out.println("\nNote: In this implementation, getBorrowedBooks() returns a defensive copy,");
        System.out.println("so it allows modification of the returned Set, but it doesn't affect the original collection.");
        System.out.println("For true unmodifiable collections, we could use Collections.unmodifiableSet() instead.");
    }
    
    private static void displayBookDetails(Book book) {
        System.out.println("ISBN: " + book.getIsbn());
        System.out.println("Title: " + book.getTitle());
        System.out.println("Author: " + book.getAuthor());
        System.out.println("Category: " + book.getCategory());
        System.out.println("Published: " + book.getPublishDate().format(dateFormatter));
        System.out.println("Available: " + (book.isAvailable() ? "Yes" : "No"));
    }
}
```

### Langkah 5: Jalankan Program

1. Klik tombol Run (F6) untuk menjalankan program
2. Eksplorasi menu untuk melihat berbagai operasi collection dalam aksi

## Rangkuman

Dalam tutorial ini, kita telah mempelajari:

✅ **Collections Framework** - Hierarki interface dan implementasi untuk mengelola kelompok objek

✅ **Interface dan Implementasi List** - ArrayList, LinkedList, Vector, dan Stack

✅ **Interface dan Implementasi Set** - HashSet, LinkedHashSet, dan TreeSet

✅ **Interface dan Implementasi Queue** - PriorityQueue, Deque, dan ArrayDeque

✅ **Interface dan Implementasi Map** - HashMap, LinkedHashMap, TreeMap, dan Hashtable

✅ **Traversal Collection** - Iterator, enhanced for-loop, dan forEach()

✅ **Manipulasi Data** - Menambah, menghapus, mencari, dan mengurutkan elemen

✅ **Comparable dan Comparator** - Menyediakan ordering untuk objek

✅ **Collections Utility Class** - Methods berguna, unmodifiable collections, dan synchronized collections

✅ **Generics dan Collections** - Type safety dan wildcards

✅ **Best Practices** - Pedoman untuk penggunaan Collections Framework

Collections Framework adalah komponen penting dari Java standard library yang menyediakan struktur data dan algoritma yang siap pakai. Dengan memahami Collections Framework, Anda dapat memilih struktur data yang tepat untuk kebutuhan Anda dan menulis kode yang efisien, maintainable, dan komprehensif.

## Latihan Soal

1. Apa perbedaan utama antara `ArrayList`, `LinkedList`, dan `Vector`? Kapan Anda akan memilih satu di atas yang lain?

2. Jelaskan perbedaan antara `HashSet`, `LinkedHashSet`, dan `TreeSet`. Berikan contoh kasus penggunaan untuk masing-masing.

3. Apa yang dimaksud dengan "iteration order" dalam konteks collections? Implementasi collection mana yang menjamin urutan tertentu dan apa urutannya?

4. Apa perbedaan antara `HashMap` dan `Hashtable`? Mengapa `Hashtable` dianggap sebagai legacy class?

5. Buatlah class `Student` dengan fields: `id`, `name`, dan `grade`. Implementasikan `Comparable` sehingga students bisa diurutkan berdasarkan grade (dari tertinggi ke terendah). Kemudian, buat `Comparator` untuk mengurutkan students berdasarkan name.

6. Jelaskan mengapa kita perlu mengimplementasikan `equals()` dan `hashCode()` saat menggunakan class kustom dengan collections berbasis hash seperti `HashSet` dan `HashMap`.

7. Apa yang terjadi jika Anda mencoba memodifikasi collection secara langsung selama iterasi? Bagaimana cara aman untuk menghapus elemen selama iterasi?

8. Jelaskan konsep "fail-fast" vs "fail-safe" iterators. Berikan contoh collection yang menyediakan masing-masing jenis iterator.

9. Buatlah program yang membaca file teks, menghitung frekuensi kemunculan setiap kata (case-insensitive), dan menampilkan 10 kata yang paling sering muncul. Gunakan Collections Framework secara tepat.

10. Implementasikan simple LRU cache (Least Recently Used) menggunakan `LinkedHashMap`. Cache harus memiliki kapasitas maksimum dan menghapus entri paling lama tidak diakses ketika penuh.

## Referensi

1. Oracle. (2023). *Java Collections Framework Documentation*. [https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/doc-files/coll-overview.html](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/doc-files/coll-overview.html)

2. Horstmann, C. S. (2019). *Core Java Volume I—Fundamentals* (11th ed.). Pearson. Chapter 9: Collections.

3. Bloch, J. (2018). *Effective Java* (3rd ed.). Addison-Wesley Professional. Chapter 9: Generics.

4. Gamma, E., Helm, R., Johnson, R., & Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley Professional.

5. Maurice Naftalin and Philip Wadler. (2006). *Java Generics and Collections*. O'Reilly Media.

6. Oracle. (2023). *The Java Tutorials: Collections*. [https://docs.oracle.com/javase/tutorial/collections/](https://docs.oracle.com/javase/tutorial/collections/)

7. Sedgewick, R., & Wayne, K. (2011). *Algorithms* (4th ed.). Addison-Wesley Professional.

8. Sierra, K., & Bates, B. (2005). *Head First Java* (2nd ed.). O'Reilly Media. Chapter 16: Collections with Generics.

9. Goetz, B., et al. (2006). *Java Concurrency in Practice*. Addison-Wesley Professional. Chapter 5: Building Blocks.

10. Evans, B., & Warburton, R. (2014). *Java in a Nutshell* (6th ed.). O'Reilly Media. Chapter 11: The Collections Framework.

---

[◀️ Kembali ke Tutorial #12: Exception Handling dalam OOP](12-exception-handling.md) | [Lanjut ke Tutorial #14: Implementasi Proyek Sederhana ▶️](14-simple-project.md)

---

© 2023 Tutorial Dasar OOP di Java untuk Pemula. Semua hak cipta dilindungi.
