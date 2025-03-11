
# 📘 Tutorial Java OOP #11: Menggunakan Lambda Expression

> *"Lambda expression adalah revolusi dalam penulisan kode Java—memungkinkan fungsi menjadi warga kelas satu, menyederhanakan kode, dan membuka pintu bagi gaya pemrograman fungsional yang elegan dan ekspresif."*

## 🎯 Tujuan Pembelajaran

Setelah mempelajari materi ini, Anda diharapkan dapat:
- Memahami konsep dasar lambda expression dalam Java
- Mengidentifikasi dan menggunakan functional interface
- Menulis lambda expression dengan berbagai sintaks
- Menggunakan method references sebagai alternatif lambda
- Memanfaatkan built-in functional interfaces dari package java.util.function
- Menerapkan lambda expression dalam pemrosesan collection dan stream
- Membandingkan lambda expression dengan anonymous class
- Menggunakan lambda expression untuk meningkatkan keterbacaan dan mengurangi boilerplate code

## 📋 Daftar Isi

1. [Pendahuluan](#pendahuluan)
2. [Apa itu Lambda Expression?](#apa-itu-lambda-expression)
   - [Definisi dan Konsep Dasar](#definisi-dan-konsep-dasar)
   - [Latar Belakang dan Tujuan](#latar-belakang-dan-tujuan)
   - [Lambda dalam Paradigma Pemrograman Fungsional](#lambda-dalam-paradigma-pemrograman-fungsional)
3. [Functional Interface](#functional-interface)
   - [Definisi Functional Interface](#definisi-functional-interface)
   - [Anotasi @FunctionalInterface](#anotasi-functionalinterface)
   - [Membuat Custom Functional Interface](#membuat-custom-functional-interface)
4. [Sintaks Lambda Expression](#sintaks-lambda-expression)
   - [Format Dasar](#format-dasar)
   - [Parameter](#parameter)
   - [Body Lambda](#body-lambda)
   - [Return Value](#return-value)
   - [Variasi Sintaks](#variasi-sintaks)
5. [Method References](#method-references)
   - [Jenis-jenis Method References](#jenis-jenis-method-references)
   - [Sintaks Method References](#sintaks-method-references)
   - [Kapan Menggunakan Method References](#kapan-menggunakan-method-references)
6. [Built-in Functional Interfaces](#built-in-functional-interfaces)
   - [Package java.util.function](#package-javautilfunction)
   - [Consumer and Supplier](#consumer-and-supplier)
   - [Predicate](#predicate)
   - [Function](#function)
   - [Operator](#operator)
   - [BiConsumer, BiFunction, dan BiPredicate](#biconsumer-bifunction-dan-bipredicate)
7. [Lambda Expression vs Anonymous Class](#lambda-expression-vs-anonymous-class)
   - [Perbandingan Sintaks](#perbandingan-sintaks)
   - [Perbedaan Perilaku dan Keterbatasan](#perbedaan-perilaku-dan-keterbatasan)
   - [Kapan Menggunakan Lambda vs Anonymous Class](#kapan-menggunakan-lambda-vs-anonymous-class)
8. [Penggunaan Lambda dengan Collections](#penggunaan-lambda-dengan-collections)
   - [Sorting](#sorting)
   - [Filtering](#filtering)
   - [Iterating](#iterating)
   - [Transforming](#transforming)
9. [Stream API dan Lambda](#stream-api-dan-lambda)
   - [Dasar-dasar Stream](#dasar-dasar-stream)
   - [Stream Operations](#stream-operations)
   - [Contoh Pemrosesan Data dengan Stream dan Lambda](#contoh-pemrosesan-data-dengan-stream-dan-lambda)
10. [Latihan Praktik dengan NetBeans](#latihan-praktik-dengan-netbeans)
11. [Best Practices](#best-practices)
12. [Rangkuman](#rangkuman)
13. [Latihan Soal](#latihan-soal)
14. [Referensi](#referensi)

## Pendahuluan

Pada tutorial sebelumnya, kita telah mempelajari konsep anonymous class—cara untuk mendefinisikan dan menginstansiasi class secara bersamaan tanpa memberikan nama. Anonymous class sangat berguna, tetapi terkadang sintaksnya terlalu bertele-tele untuk tugas-tugas sederhana, terutama ketika kita hanya perlu mengimplementasikan interface dengan satu method.

Java 8 (dirilis pada tahun 2014) memperkenalkan fitur baru yang revolusioner bernama **Lambda Expression**, yang menyediakan cara yang lebih ringkas dan ekspresif untuk menulis anonymous class untuk functional interface. Lambda expression merupakan langkah signifikan dalam evolusi Java, membawa elemen pemrograman fungsional ke dalam bahasa yang telah lama didominasi oleh paradigma pemrograman berorientasi objek.

Dalam tutorial ini, kita akan menjelajahi dunia lambda expression dalam Java, mempelajari bagaimana menggunakannya, dan memahami kapan harus mengaplikasikannya dalam kode kita.

## Apa itu Lambda Expression?

### Definisi dan Konsep Dasar

**Lambda expression** adalah blok kode ringkas (anonymous function) yang dapat diteruskan dan dieksekusi kemudian. Lambda expression dapat dianggap sebagai method tanpa nama yang tidak perlu dideklarasikan dalam class tertentu.

Secara formal, lambda expression adalah representasi ringkas dari anonymous class untuk interface yang hanya memiliki satu abstract method (functional interface). Lambda expression memungkinkan kita untuk memperlakukan fungsionalitas sebagai parameter method, atau kode sebagai data.

Analogi sederhana: Jika method biasa adalah pekerja tetap dengan nama dan job description, lambda expression adalah pekerja lepas yang dipanggil untuk tugas spesifik tanpa perlu formalitas penuh.

### Latar Belakang dan Tujuan

Java awalnya dirancang sebagai bahasa pemrograman berorientasi objek (OOP) murni. Seiring waktu, kebutuhan untuk menyederhanakan penulisan kode dan meningkatkan ekspresi fungsional menjadi semakin penting.

Beberapa tujuan utama diperkenalkannya lambda expression dalam Java:

1. **Menyederhanakan Kode**: Mengurangi boilerplate code, terutama untuk implementasi sederhana dari interface dengan satu method.

2. **Meningkatkan Readability**: Membuat kode lebih ringkas dan mudah dibaca.

3. **Mendukung Programming Fungsional**: Memfasilitasi gaya pemrograman fungsional dengan memperlakukan fungsi sebagai "first-class citizens".

4. **Meningkatkan Performa**: Memungkinkan pemrosesan paralel yang efisien pada collections dengan Stream API.

5. **Mendukung API Modern**: Membuat Java lebih cocok untuk API modern yang mengandalkan callback dan event-driven programming.

### Lambda dalam Paradigma Pemrograman Fungsional

Lambda expression berakar pada kalkulus lambda (lambda calculus), yang dikembangkan oleh matematikawan Alonzo Church pada tahun 1930-an sebagai sistem formal untuk ekspresi komputasi. Kalkulus lambda menjadi dasar untuk banyak bahasa pemrograman fungsional modern seperti Haskell, Scala, dan sekarang mempengaruhi Java.

Prinsip-prinsip utama pemrograman fungsional yang didukung oleh lambda expression di Java:

1. **Functions as First-Class Citizens**: Fungsi dapat disimpan dalam variabel, diteruskan sebagai argumen, dan dikembalikan dari fungsi lain.

2. **Immutability**: Mendorong penggunaan data yang tidak berubah (immutable).

3. **Pure Functions**: Fungsi-fungsi yang tidak memiliki side effects dan selalu mengembalikan hasil yang sama untuk input yang sama.

4. **Higher-Order Functions**: Fungsi yang dapat mengambil fungsi lain sebagai argumen atau mengembalikan fungsi sebagai hasil.

## Functional Interface

### Definisi Functional Interface

**Functional interface** adalah interface yang hanya memiliki satu abstract method (tidak termasuk method dari class `Object`). Functional interface juga kadang disebut sebagai **SAM interfaces** (Single Abstract Method interfaces).

Contoh functional interface yang sudah ada di Java bahkan sebelum Java 8:
- `Runnable` dengan method `run()`
- `Comparator` dengan method `compare()`
- `ActionListener` dengan method `actionPerformed()`

Functional interface adalah pondasi untuk lambda expression, karena lambda expression hanya dapat digunakan di tempat di mana tipe targetnya adalah functional interface.

### Anotasi @FunctionalInterface

Java 8 memperkenalkan anotasi `@FunctionalInterface` untuk menandai interface sebagai functional interface. Anotasi ini adalah anotasi informasional dan membantu kompiler dalam memverifikasi bahwa interface tersebut memang memiliki tepat satu abstract method.

```java
@FunctionalInterface
public interface Converter<F, T> {
    T convert(F from);
}
```

Jika Anda menandai interface dengan `@FunctionalInterface` dan interface tersebut memiliki lebih dari satu abstract method, kompiler akan menampilkan error.

### Membuat Custom Functional Interface

Anda dapat membuat functional interface Anda sendiri sesuai kebutuhan:

```java
@FunctionalInterface
public interface MathOperation {
    int operate(int a, int b);
}

@FunctionalInterface
public interface StringProcessor {
    String process(String input);
}

@FunctionalInterface
public interface Validator {
    boolean validate(String input);
}
```

Perhatikan bahwa interface dapat memiliki banyak default, static, atau private methods, tetapi hanya boleh memiliki satu abstract method untuk dianggap sebagai functional interface.

## Sintaks Lambda Expression

### Format Dasar

Sintaks dasar lambda expression adalah:

```
(parameters) -> expression
```

atau

```
(parameters) -> { statements; }
```

Contoh sederhana:

```java
// Lambda dengan satu parameter dan satu expression
Runnable runnable = () -> System.out.println("Hello World");

// Lambda dengan dua parameter dan block statements
Comparator<String> comparator = (s1, s2) -> {
    int result = s1.length() - s2.length();
    return result;
};
```

### Parameter

Parameter dalam lambda expression dapat memiliki beberapa bentuk:

1. **Tanpa Parameter**:
   ```java
   Runnable r = () -> System.out.println("No parameters");
   ```

2. **Satu Parameter (tanda kurung opsional)**:
   ```java
   Consumer<String> c = s -> System.out.println(s);
   // atau
   Consumer<String> c = (s) -> System.out.println(s);
   ```

3. **Beberapa Parameter**:
   ```java
   BiFunction<Integer, Integer, Integer> add = (a, b) -> a + b;
   ```

4. **Parameter dengan Tipe Data Eksplisit**:
   ```java
   BiFunction<Integer, Integer, Integer> add = (Integer a, Integer b) -> a + b;
   ```

### Body Lambda

Body lambda expression dapat berupa:

1. **Single Expression** (tanpa return eksplisit, tanpa semicolon, tanpa braces):
   ```java
   Function<Integer, Integer> square = n -> n * n;
   ```

2. **Block Statements** (memerlukan braces, semicolons, dan return eksplisit jika mengembalikan nilai):
   ```java
   Function<Integer, Integer> factorial = n -> {
       int result = 1;
       for (int i = 1; i <= n; i++) {
           result *= i;
       }
       return result;
   };
   ```

### Return Value

Untuk lambda expression dengan single expression, nilai return adalah hasil evaluasi expression tersebut. Keyword `return` tidak diperlukan.

```java
// Implicit return
Predicate<Integer> isEven = n -> n % 2 == 0;
```

Untuk lambda expression dengan block statements, Anda harus menggunakan keyword `return` secara eksplisit jika method interface mengembalikan nilai.

```java
// Explicit return
Function<String, Integer> wordCount = text -> {
    if (text == null || text.isEmpty()) {
        return 0;
    }
    return text.split("\\s+").length;
};
```

### Variasi Sintaks

Berikut adalah beberapa variasi sintaks lambda expression:

1. **Lambda Tanpa Parameter**:
   ```java
   Runnable noParams = () -> System.out.println("No parameters");
   ```

2. **Lambda dengan Satu Parameter (Tanpa Tipe)**:
   ```java
   Consumer<String> oneParam = s -> System.out.println(s);
   ```

3. **Lambda dengan Satu Parameter (Dengan Tipe)**:
   ```java
   Consumer<String> oneParamWithType = (String s) -> System.out.println(s);
   ```

4. **Lambda dengan Multiple Parameters**:
   ```java
   BiFunction<Integer, Integer, Integer> add = (a, b) -> a + b;
   ```

5. **Lambda dengan Multiple Parameters (Dengan Tipe)**:
   ```java
   BiFunction<Integer, Integer, Integer> addWithTypes = 
       (Integer a, Integer b) -> a + b;
   ```

6. **Lambda dengan Block Body**:
   ```java
   BiFunction<Integer, Integer, Integer> multiply = (a, b) -> {
       int result = a * b;
       return result;
   };
   ```

## Method References

Method references adalah sintaks singkat untuk lambda expression yang hanya memanggil satu method. Mereka membuat kode lebih ringkas dan lebih mudah dibaca dengan menghilangkan boilerplate untuk mengarahkan parameter.

### Jenis-jenis Method References

Ada empat jenis method references:

1. **Reference ke Static Method**:
   ```java
   Function<String, Integer> parseInt = Integer::parseInt;
   // Equivalent lambda: s -> Integer.parseInt(s)
   ```

2. **Reference ke Instance Method dari Objek Tertentu**:
   ```java
   String greeting = "Hello";
   Supplier<Integer> length = greeting::length;
   // Equivalent lambda: () -> greeting.length()
   ```

3. **Reference ke Instance Method dari Tipe Tertentu**:
   ```java
   Function<String, Integer> lengthFunc = String::length;
   // Equivalent lambda: s -> s.length()
   ```

4. **Reference ke Constructor**:
   ```java
   Supplier<ArrayList<String>> listCreator = ArrayList::new;
   // Equivalent lambda: () -> new ArrayList<>()
   ```

### Sintaks Method References

Sintaks method reference menggunakan operator double colon (`::`) antara nama tipe/objek dan nama method:

```
TypeName::methodName
objectReference::methodName
ClassName::new (for constructor references)
```

### Kapan Menggunakan Method References

Method references sangat berguna ketika lambda expression hanya memanggil method yang sudah ada tanpa melakukan operasi tambahan. Ini membuat kode lebih ringkas dan lebih fokus pada apa yang dilakukan daripada bagaimana melakukannya.

```java
// With lambda expression
list.forEach(s -> System.out.println(s));

// With method reference (cleaner)
list.forEach(System.out::println);
```

Namun, jika lambda perlu melakukan beberapa operasi atau memerlukan transformasi parameter, method reference mungkin tidak cocok:

```java
// Cannot be simplified with method reference
list.forEach(s -> System.out.println("Item: " + s));
```

## Built-in Functional Interfaces

### Package java.util.function

Java 8 memperkenalkan package `java.util.function` yang berisi berbagai functional interface standar untuk digunakan dengan lambda expression. Menggunakan interface ini membuat kode lebih konsisten dan mengurangi proliferasi custom functional interfaces.

### Consumer and Supplier

**Consumer**: Menerima satu input dan tidak mengembalikan hasil (melakukan operasi "konsumsi").

```java
@FunctionalInterface
public interface Consumer<T> {
    void accept(T t);
}

// Example usage
Consumer<String> printer = s -> System.out.println(s);
printer.accept("Hello, Consumer!");
```

**Supplier**: Tidak menerima input tetapi mengembalikan hasil (menyediakan atau "memasok" nilai).

```java
@FunctionalInterface
public interface Supplier<T> {
    T get();
}

// Example usage
Supplier<LocalDateTime> currentTime = () -> LocalDateTime.now();
System.out.println(currentTime.get());
```

### Predicate

**Predicate**: Menerima satu input dan mengembalikan boolean (mengevaluasi kondisi).

```java
@FunctionalInterface
public interface Predicate<T> {
    boolean test(T t);
}

// Example usage
Predicate<String> isEmpty = s -> s == null || s.isEmpty();
System.out.println(isEmpty.test(""));  // true
System.out.println(isEmpty.test("Not empty"));  // false
```

Predicate juga mendukung operasi komposisi dengan methods `and()`, `or()`, dan `negate()`:

```java
Predicate<String> hasLength10 = s -> s.length() == 10;
Predicate<String> startsWithA = s -> s.startsWith("A");

// Combining predicates
Predicate<String> p = hasLength10.and(startsWithA);
```

### Function

**Function**: Menerima satu input dan mengembalikan hasil yang mungkin berbeda tipe.

```java
@FunctionalInterface
public interface Function<T, R> {
    R apply(T t);
}

// Example usage
Function<String, Integer> length = s -> s.length();
System.out.println(length.apply("Hello"));  // 5
```

Function juga mendukung operasi komposisi dengan methods `compose()` dan `andThen()`:

```java
Function<Integer, Integer> multiplyBy2 = n -> n * 2;
Function<Integer, Integer> add3 = n -> n + 3;

Function<Integer, Integer> multiplyThenAdd = add3.compose(multiplyBy2);
System.out.println(multiplyThenAdd.apply(5));  // 5*2+3 = 13

Function<Integer, Integer> addThenMultiply = add3.andThen(multiplyBy2);
System.out.println(addThenMultiply.apply(5));  // (5+3)*2 = 16
```

### Operator

**Operator**: Varian khusus dari Function di mana tipe input dan output sama.

- **UnaryOperator**: Operasi pada satu argumen yang mengembalikan hasil dengan tipe yang sama.

```java
@FunctionalInterface
public interface UnaryOperator<T> extends Function<T, T> {
}

// Example usage
UnaryOperator<String> toUpperCase = s -> s.toUpperCase();
System.out.println(toUpperCase.apply("hello"));  // HELLO
```

- **BinaryOperator**: Operasi pada dua argumen dengan tipe yang sama, mengembalikan hasil dengan tipe yang sama.

```java
@FunctionalInterface
public interface BinaryOperator<T> extends BiFunction<T, T, T> {
}

// Example usage
BinaryOperator<Integer> add = (a, b) -> a + b;
System.out.println(add.apply(5, 3));  // 8
```

### BiConsumer, BiFunction, dan BiPredicate

Untuk operasi yang memerlukan dua input:

- **BiConsumer**: Menerima dua input dan tidak mengembalikan hasil.

```java
@FunctionalInterface
public interface BiConsumer<T, U> {
    void accept(T t, U u);
}

// Example usage
BiConsumer<String, Integer> printRepeated = (str, count) -> {
    for (int i = 0; i < count; i++) {
        System.out.println(str);
    }
};
printRepeated.accept("Hello", 3);
```

- **BiFunction**: Menerima dua input dan mengembalikan hasil.

```java
@FunctionalInterface
public interface BiFunction<T, U, R> {
    R apply(T t, U u);
}

// Example usage
BiFunction<String, String, String> concat = (s1, s2) -> s1 + s2;
System.out.println(concat.apply("Hello, ", "world!"));  // Hello, world!
```

- **BiPredicate**: Menerima dua input dan mengembalikan boolean.

```java
@FunctionalInterface
public interface BiPredicate<T, U> {
    boolean test(T t, U u);
}

// Example usage
BiPredicate<String, Integer> checkLength = (str, len) -> str.length() == len;
System.out.println(checkLength.test("Hello", 5));  // true
```

## Lambda Expression vs Anonymous Class

### Perbandingan Sintaks

Perbandingan antara lambda expression dan anonymous class:

```java
// Anonymous class implementation
Runnable anonymousRunnable = new Runnable() {
    @Override
    public void run() {
        System.out.println("Anonymous class implementation");
    }
};

// Lambda expression implementation
Runnable lambdaRunnable = () -> System.out.println("Lambda implementation");
```

```java
// Anonymous class implementation
Comparator<String> anonymousComparator = new Comparator<String>() {
    @Override
    public int compare(String s1, String s2) {
        return s1.length() - s2.length();
    }
};

// Lambda expression implementation
Comparator<String> lambdaComparator = (s1, s2) -> s1.length() - s2.length();
```

### Perbedaan Perilaku dan Keterbatasan

Selain perbedaan sintaks, ada beberapa perbedaan perilaku penting antara lambda expression dan anonymous class:

1. **Scope `this`**:
   - Dalam anonymous class, `this` mereferensikan instance anonymous class itu sendiri.
   - Dalam lambda expression, `this` mereferensikan enclosing class di mana lambda didefinisikan.

   ```java
   public class ThisExample {
       private String name = "Outer Class";
       
       public void testThis() {
           // Anonymous class
           Runnable anonymousRunnable = new Runnable() {
               private String name = "Anonymous Class";
               
               @Override
               public void run() {
                   System.out.println(this.name);  // "Anonymous Class"
               }
           };
           
           // Lambda expression
           Runnable lambdaRunnable = () -> {
               // No shadowing possible here
               System.out.println(this.name);  // "Outer Class"
           };
           
           anonymousRunnable.run();
           lambdaRunnable.run();
       }
   }
   ```

2. **Shadowing Variables**:
   - Anonymous class dapat mendefinisikan variabel dengan nama yang sama dengan variabel di enclosing scope (shadowing).
   - Lambda expression tidak dapat melakukan shadowing variabel pada enclosing scope.

3. **Tipe Target**:
   - Anonymous class dapat digunakan untuk class maupun interface, dengan satu atau banyak methods.
   - Lambda expression hanya dapat digunakan untuk functional interface (interface dengan satu abstract method).

4. **Method Overloading Resolution**:
   - Anonymous class memiliki tipe spesifik yang sudah jelas.
   - Lambda expression bersifat polymorphic, artinya tipe tergantung pada context.

### Kapan Menggunakan Lambda vs Anonymous Class

**Gunakan Lambda Expressions ketika**:
- Kode Anda mengimplementasikan functional interface
- Implementasinya sederhana dan singkat
- Tidak perlu mengakses instance-specific state melalui `this`
- Tidak perlu menambahkan fields atau methods tambahan

**Gunakan Anonymous Class ketika**:
- Kode Anda mengimplementasikan interface dengan lebih dari satu abstract method
- Kode Anda perlu meng-extend class (bukan interface)
- Kode Anda perlu menambahkan fields atau methods tambahan
- Kode Anda perlu mengakses instance-specific state melalui `this`
- Kode Anda perlu melakukan shadowing variables

## Penggunaan Lambda dengan Collections

Lambda expression sangat berguna ketika bekerja dengan collections. Beberapa operasi umum yang dapat disederhanakan dengan lambda:

### Sorting

Sebelum Java 8:
```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");
Collections.sort(names, new Comparator<String>() {
    @Override
    public int compare(String a, String b) {
        return a.compareTo(b);
    }
});
```

Dengan lambda expression:
```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");
Collections.sort(names, (a, b) -> a.compareTo(b));

// Even simpler with method reference
Collections.sort(names, String::compareTo);

// Or using List.sort() introduced in Java 8
names.sort(String::compareTo);
```

### Filtering

Sebelum Java 8, kita perlu membuat iterasi dan filter manual. Dengan lambda dan Stream API:

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");
List<String> filteredNames = names.stream()
                               .filter(name -> name.startsWith("A"))
                               .collect(Collectors.toList());
```

### Iterating

Sebelum Java 8:
```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");
for (String name : names) {
    System.out.println(name);
}
```

Dengan lambda expression:
```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");
names.forEach(name -> System.out.println(name));

// Even simpler with method reference
names.forEach(System.out::println);
```

### Transforming

Sebelum Java 8, kita perlu iterasi manual untuk transformasi. Dengan lambda dan Stream API:

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");
List<Integer> nameLengths = names.stream()
                              .map(name -> name.length())
                              .collect(Collectors.toList());

// Using method reference
List<Integer> nameLengths = names.stream()
                              .map(String::length)
                              .collect(Collectors.toList());
```

## Stream API dan Lambda

### Dasar-dasar Stream

**Stream** adalah urutan elemen yang mendukung operasi agregat sekuensial dan paralel. Stream API bekerja sangat baik dengan lambda expression dan method references.

Beberapa karakteristik Stream:
- Stream tidak menyimpan elemen. Elemen mungkin disimpan dalam struktur data yang mendasarinya atau dihasilkan sesuai kebutuhan.
- Operasi Stream adalah lazy—tidak dieksekusi sampai diperlukan.
- Stream tidak dapat digunakan kembali. Setelah operasi terminal dipanggil, stream tidak dapat digunakan lagi.
- Stream tidak mengubah sumber data.

```java
// Creating a stream from collection
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");
Stream<String> nameStream = names.stream();

// Creating a stream directly
Stream<String> directStream = Stream.of("Alice", "Bob", "Charlie", "David");
```

### Stream Operations

Stream API menyediakan dua jenis operasi:

1. **Intermediate Operations**: Mengembalikan stream baru, memungkinkan chaining. Operasi ini adalah lazy.
   - `filter()`, `map()`, `flatMap()`, `distinct()`, `sorted()`, `limit()`, `skip()`, dll.

2. **Terminal Operations**: Menghasilkan hasil atau side effect. Setelah operasi terminal, stream tidak dapat digunakan lagi.
   - `forEach()`, `collect()`, `reduce()`, `count()`, `min()`, `max()`, `anyMatch()`, `allMatch()`, `noneMatch()`, `findFirst()`, `findAny()`, dll.

Contoh pipeline operasi stream:

```java
List<String> result = names.stream()         // Create stream
                         .filter(n -> n.length() > 4)  // Intermediate operation
                         .map(String::toUpperCase)     // Intermediate operation
                         .sorted()                     // Intermediate operation
                         .collect(Collectors.toList()); // Terminal operation
```

### Contoh Pemrosesan Data dengan Stream dan Lambda

**Filtering dan Transformasi**:
```java
List<Person> people = getPeopleList();
List<String> adultNames = people.stream()
                             .filter(person -> person.getAge() >= 18)
                             .map(Person::getName)
                             .collect(Collectors.toList());
```

**Grouping**:
```java
Map<String, List<Person>> peopleByCity = people.stream()
                                           .collect(Collectors.groupingBy(Person::getCity));
```

**Averaging**:
```java
double averageAge = people.stream()
                      .mapToInt(Person::getAge)
                      .average()
                      .orElse(0.0);
```

**Finding Max/Min**:
```java
Optional<Person> oldestPerson = people.stream()
                              .max(Comparator.comparing(Person::getAge));
```

**Joining Strings**:
```java
String allNames = people.stream()
                     .map(Person::getName)
                     .collect(Collectors.joining(", "));
```

**Parallel Processing**:
```java
// Using parallel stream for potentially better performance on large collections
long count = people.parallelStream()
                .filter(person -> person.getAge() > 30)
                .count();
```

## Latihan Praktik dengan NetBeans

Mari kita praktikkan konsep lambda expression dengan membuat aplikasi sederhana di NetBeans.

### Langkah 1: Buat Project Baru

1. Buka NetBeans
2. Pilih `File > New Project`
3. Pilih `Java with Ant > Java Application`
4. Beri nama project `LambdaExpressionDemo` dan klik `Finish`

### Langkah 2: Buat Class Person

1. Klik kanan pada package project > `New > Java Class`
2. Beri nama `Person` dan klik `Finish`
3. Isi dengan kode berikut:

```java
package lambdaexpressiondemo;

public class Person {
    private String name;
    private int age;
    private String city;
    private String gender;
    private double salary;
    
    public Person(String name, int age, String city, String gender, double salary) {
        this.name = name;
        this.age = age;
        this.city = city;
        this.gender = gender;
        this.salary = salary;
    }
    
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
    
    public String getCity() {
        return city;
    }
    
    public String getGender() {
        return gender;
    }
    
    public double getSalary() {
        return salary;
    }
    
    @Override
    public String toString() {
        return "Person{" + "name=" + name + ", age=" + age + 
               ", city=" + city + ", gender=" + gender + 
               ", salary=" + salary + '}';
    }
}
```

### Langkah 3: Buat Custom Functional Interfaces

1. Klik kanan pada package project > `New > Java Interface`
2. Beri nama `StringProcessor` dan klik `Finish`
3. Isi dengan kode berikut:

```java
package lambdaexpressiondemo;

@FunctionalInterface
public interface StringProcessor {
    String process(String input);
}
```

4. Buat interface baru dengan nama `MathOperation`:

```java
package lambdaexpressiondemo;

@FunctionalInterface
public interface MathOperation {
    int operate(int a, int b);
}
```

5. Buat interface baru dengan nama `PersonPredicate`:

```java
package lambdaexpressiondemo;

@FunctionalInterface
public interface PersonPredicate {
    boolean test(Person person);
}
```

### Langkah 4: Buat Class Helper untuk Demonstrasi

1. Klik kanan pada package project > `New > Java Class`
2. Beri nama `LambdaHelper` dan klik `Finish`
3. Isi dengan kode berikut:

```java
package lambdaexpressiondemo;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Predicate;

public class LambdaHelper {
    
    // Method yang menerima functional interface sebagai parameter
    public static void processString(String str, StringProcessor processor) {
        String result = processor.process(str);
        System.out.println("Processing \"" + str + "\" resulted in: \"" + result + "\"");
    }
    
    public static int calculate(int a, int b, MathOperation operation) {
        return operation.operate(a, b);
    }
    
    // Method yang bekerja dengan built-in functional interfaces
    public static <T> List<T> filter(List<T> list, Predicate<T> predicate) {
        List<T> result = new ArrayList<>();
        for (T item : list) {
            if (predicate.test(item)) {
                result.add(item);
            }
        }
        return result;
    }
    
    public static <T, R> List<R> map(List<T> list, Function<T, R> mapper) {
        List<R> result = new ArrayList<>();
        for (T item : list) {
            result.add(mapper.apply(item));
        }
        return result;
    }
    
    public static <T> void forEach(List<T> list, Consumer<T> consumer) {
        for (T item : list) {
            consumer.accept(item);
        }
    }
    
    // Method untuk filtering people berdasarkan kriteria
    public static List<Person> filterPeople(List<Person> people, PersonPredicate predicate) {
        List<Person> result = new ArrayList<>();
        for (Person person : people) {
            if (predicate.test(person)) {
                result.add(person);
            }
        }
        return result;
    }
}
```

### Langkah 5: Buat Kelas Main untuk Demonstrasi

1. Buka file main (biasanya `LambdaExpressionDemo.java`)
2. Ubah kode menjadi:

```java
package lambdaexpressiondemo;

import java.util.Arrays;
import java.util.Comparator;
import java.util.List;
import java.util.Map;
import java.util.function.Function;
import java.util.function.Predicate;
import java.util.stream.Collectors;

public class LambdaExpressionDemo {
    public static void main(String[] args) {
        System.out.println("===== LAMBDA EXPRESSION DEMO =====\n");
        
        // Custom functional interface demo
        System.out.println("--- Custom Functional Interface Demo ---");
        
        // Lambda with StringProcessor interface
        StringProcessor toUpperCase = s -> s.toUpperCase();
        StringProcessor removeSpaces = s -> s.replaceAll("\\s", "");
        StringProcessor reverser = s -> new StringBuilder(s).reverse().toString();
        
        LambdaHelper.processString("Hello World", toUpperCase);
        LambdaHelper.processString("Hello World", removeSpaces);
        LambdaHelper.processString("Hello World", reverser);
        
        // Method reference with StringProcessor
        StringProcessor trimmer = String::trim;
        LambdaHelper.processString("   Padded String   ", trimmer);
        
        // Lambda with MathOperation interface
        MathOperation addition = (a, b) -> a + b;
        MathOperation subtraction = (a, b) -> a - b;
        MathOperation multiplication = (a, b) -> a * b;
        MathOperation division = (a, b) -> a / b;
        
        System.out.println("\n10 + 5 = " + LambdaHelper.calculate(10, 5, addition));
        System.out.println("10 - 5 = " + LambdaHelper.calculate(10, 5, subtraction));
        System.out.println("10 * 5 = " + LambdaHelper.calculate(10, 5, multiplication));
        System.out.println("10 / 5 = " + LambdaHelper.calculate(10, 5, division));
        
        // Different lambda syntax variations
        System.out.println("\n--- Lambda Syntax Variations ---");
        
        // Single parameter, expression body
        StringProcessor simpleExpression = s -> s + "!";
        LambdaHelper.processString("Hello", simpleExpression);
        
        // Multiple parameters, expression body
        MathOperation expressionWithMultipleParams = (a, b) -> a * b + a;
        System.out.println("5 * 3 + 5 = " + LambdaHelper.calculate(5, 3, expressionWithMultipleParams));
        
        // Single parameter with explicit type, block body
        StringProcessor blockWithReturn = (String s) -> {
            StringBuilder builder = new StringBuilder();
            for (char c : s.toCharArray()) {
                builder.append(Character.isUpperCase(c) ? Character.toLowerCase(c) : 
                                                         Character.toUpperCase(c));
            }
            return builder.toString();
        };
        LambdaHelper.processString("Hello World", blockWithReturn);
        
        // Built-in functional interfaces demo
        System.out.println("\n--- Built-in Functional Interfaces Demo ---");
        
        List<String> names = Arrays.asList("John", "Alice", "Bob", "Charlie", "Dave", "Eve");
        
        // Predicate<T>
        Predicate<String> startsWithA = name -> name.startsWith("A");
        List<String> namesStartingWithA = LambdaHelper.filter(names, startsWithA);
        System.out.println("Names starting with 'A': " + namesStartingWithA);
        
        Predicate<String> lengthGreaterThan4 = name -> name.length() > 4;
        List<String> longNames = LambdaHelper.filter(names, lengthGreaterThan4);
        System.out.println("Names longer than 4 characters: " + longNames);
        
        // Function<T, R>
        Function<String, Integer> nameLength = String::length;
        List<Integer> nameLengths = LambdaHelper.map(names, nameLength);
        System.out.println("Name lengths: " + nameLengths);
        
        // Consumer<T>
        System.out.println("\nNames in uppercase:");
        LambdaHelper.forEach(names, name -> System.out.println(name.toUpperCase()));
        
        // Person list demo
        System.out.println("\n--- Person List Processing Demo ---");
        
        List<Person> people = Arrays.asList(
            new Person("John", 28, "New York", "Male", 50000),
            new Person("Alice", 24, "London", "Female", 60000),
            new Person("Bob", 32, "Paris", "Male", 75000),
            new Person("Charlie", 45, "New York", "Male", 90000),
            new Person("Diana", 36, "London", "Female", 85000),
            new Person("Eve", 22, "Paris", "Female", 45000)
        );
        
        // Custom PersonPredicate
        PersonPredicate isAdult = person -> person.getAge() >= 18;
        PersonPredicate isNYResident = person -> person.getCity().equals("New York");
        PersonPredicate isFemale = person -> person.getGender().equals("Female");
        
        List<Person> adults = LambdaHelper.filterPeople(people, isAdult);
        System.out.println("All people are adults: " + (adults.size() == people.size()));
        
        List<Person> nyResidents = LambdaHelper.filterPeople(people, isNYResident);
        System.out.println("New York residents: " + nyResidents.size());
        
        List<Person> females = LambdaHelper.filterPeople(people, isFemale);
        System.out.println("Female persons: " + females.size());
        
        // Combining predicates
        PersonPredicate isFemaleNYResident = person -> 
            person.getGender().equals("Female") && person.getCity().equals("New York");
        
        List<Person> femaleNYResidents = LambdaHelper.filterPeople(people, isFemaleNYResident);
        System.out.println("Female New York residents: " + femaleNYResidents.size());
        
        // Stream API demo
        System.out.println("\n--- Stream API Demo ---");
        
        // Filtering
        List<Person> highEarners = people.stream()
                                     .filter(p -> p.getSalary() > 70000)
                                     .collect(Collectors.toList());
        
        System.out.println("High earners (>70000): " + highEarners.size());
        
        // Mapping
        List<String> personNames = people.stream()
                                      .map(Person::getName)
                                      .collect(Collectors.toList());
        
        System.out.println("Person names: " + personNames);
        
        // Sorting
        List<Person> sortedByAge = people.stream()
                                      .sorted(Comparator.comparing(Person::getAge))
                                      .collect(Collectors.toList());
        
        System.out.println("\nPeople sorted by age:");
        sortedByAge.forEach(p -> System.out.println(p.getName() + ": " + p.getAge()));
        
        // Grouping
        Map<String, List<Person>> peopleByCity = people.stream()
                                               .collect(Collectors.groupingBy(Person::getCity));
        
        System.out.println("\nPeople grouped by city:");
        peopleByCity.forEach((city, cityPeople) -> {
            System.out.println(city + ": " + 
                            cityPeople.stream()
                                     .map(Person::getName)
                                     .collect(Collectors.joining(", ")));
        });
        
        // Statistics
        double averageSalary = people.stream()
                               .mapToDouble(Person::getSalary)
                               .average()
                               .orElse(0.0);
        
        double totalSalary = people.stream()
                            .mapToDouble(Person::getSalary)
                            .sum();
        
        System.out.println("\nSalary statistics:");
        System.out.println("Average salary: " + averageSalary);
        System.out.println("Total salary: " + totalSalary);
        
        // Method references demo
        System.out.println("\n--- Method References Demo ---");
        
        // Static method reference
        Function<String, Integer> parseInt1 = s -> Integer.parseInt(s);
        Function<String, Integer> parseInt2 = Integer::parseInt;
        
        System.out.println("Lambda: " + parseInt1.apply("123"));
        System.out.println("Method reference: " + parseInt2.apply("456"));
        
        // Instance method reference of particular object
        String prefix = "User: ";
        Function<String, String> addPrefix1 = s -> prefix.concat(s);
        Function<String, String> addPrefix2 = prefix::concat;
        
        System.out.println("Lambda: " + addPrefix1.apply("John"));
        System.out.println("Method reference: " + addPrefix2.apply("Alice"));
        
        // Instance method reference of arbitrary object of particular type
        Function<String, String> toUpper1 = s -> s.toUpperCase();
        Function<String, String> toUpper2 = String::toUpperCase;
        
        System.out.println("Lambda: " + toUpper1.apply("hello"));
        System.out.println("Method reference: " + toUpper2.apply("world"));
        
        // Constructor reference
        Function<String, StringBuilder> builderCreator1 = s -> new StringBuilder(s);
        Function<String, StringBuilder> builderCreator2 = StringBuilder::new;
        
        System.out.println("Lambda: " + builderCreator1.apply("Hello").reverse());
        System.out.println("Constructor reference: " + builderCreator2.apply("World").reverse());
    }
}
```

### Langkah 6: Jalankan Program

1. Klik tombol Run (F6) untuk menjalankan program
2. Amati output yang dihasilkan

## Best Practices

1. **Gunakan Lambda untuk Kode yang Singkat dan Ekspresif**:
   - Lambda expression ideal untuk implementasi sederhana.
   - Jika implementasi lebih dari beberapa baris, pertimbangkan named method.

2. **Gunakan Method References Bila Memungkinkan**:
   - Method references membuat kode lebih ringkas dan fokus pada apa yang dilakukan.

3. **Manfaatkan Built-in Functional Interfaces**:
   - Gunakan interface dari `java.util.function` daripada membuat custom functional interface jika sudah sesuai.

4. **Hindari Side Effects dalam Lambda**:
   - Lambda expression sebaiknya bersifat stateless dan tidak mengubah state luar.
   - Ikuti prinsip pure function saat memungkinkan.

5. **Gunakan Parameter Type Inference**:
   - Biarkan compiler menyimpulkan tipe parameter ketika jelas dari konteks.

6. **Perhatikan Kejelasan dan Readability**:
   - Lambda yang terlalu padat dapat mengurangi readability.
   - Pilih antara lambda singkat dan method bernama berdasarkan kejelasan.

7. **Gunakan Stream API untuk Operasi Collection**:
   - Manfaatkan Stream API untuk operasi pada collections daripada iterasi manual.

8. **Gunakan Parallel Streams dengan Hati-hati**:
   - Parallel streams bisa meningkatkan performa tetapi juga bisa menyebabkan overhead.
   - Gunakan untuk collections besar dan operasi yang independen.

## Rangkuman

Dalam tutorial ini, kita telah mempelajari:

✅ **Lambda Expression** - Blok kode tanpa nama yang dapat diteruskan sebagai argumen atau disimpan dalam variabel

✅ **Functional Interface** - Interface dengan satu abstract method yang menjadi target lambda expression

✅ **Sintaks Lambda** - Berbagai variasi sintaks untuk parameter, body, dan return values

✅ **Method References** - Cara singkat untuk mereferensikan methods yang sudah ada sebagai lambda

✅ **Built-in Functional Interfaces** - Package `java.util.function` yang menyediakan interfaces standar seperti `Predicate`, `Function`, `Consumer`, dll

✅ **Lambda vs Anonymous Class** - Perbedaan dalam sintaks, perilaku, dan use cases

✅ **Stream API** - API yang powerful untuk operasi pada sequences of elements, bekerja sangat baik dengan lambda

✅ **Best Practices** - Pedoman untuk menggunakan lambda expression secara efektif

Lambda expression adalah fitur yang sangat powerful dalam Java modern yang memungkinkan gaya pemrograman yang lebih ringkas, ekspresif, dan fungsional. Dengan menguasai lambda expression dan APIs terkait, Anda dapat menulis kode Java yang lebih efisien, mudah dibaca, dan mudah dipelihara.

## Latihan Soal

1. Apa yang dimaksud dengan lambda expression dalam Java? Jelaskan karakteristik utamanya.

2. Apa itu functional interface? Berikan contoh built-in functional interface dalam Java beserta method abstractnya.

3. Tuliskan beberapa variasi sintaks lambda expression dengan contoh kode.

4. Jelaskan perbedaan antara lambda expression dan anonymous class. Kapan sebaiknya menggunakan masing-masing?

5. Apa yang dimaksud dengan method reference? Berikan contoh untuk empat jenis method reference.

6. Buatlah custom functional interface bernama `Calculator` dengan satu method `calculate(double a, double b)` yang mengembalikan `double`. Implementasikan interface tersebut menggunakan lambda expression untuk operasi penjumlahan, pengurangan, perkalian, dan pembagian.

7. Bagaimana cara mengakses variabel lokal dari dalam lambda expression? Apa batasan yang perlu diperhatikan?

8. Dengan menggunakan Stream API dan lambda expression, tuliskan kode untuk:
   - Filter list of integers untuk mendapatkan angka genap
   - Transform list of strings menjadi uppercase
   - Find maksimum value dari list of integers
   - Calculate rata-rata dari list of doubles

9. Jelaskan konsep "effectively final" dalam konteks variabel yang diakses oleh lambda expression.

10. Buatlah program sederhana yang memproses list of students dengan fields name, age, dan grade. Gunakan Stream API dan lambda expression untuk:
    - Filter students berdasarkan grade minimal tertentu
    - Group students berdasarkan age
    - Calculate rata-rata grade
    - Find student dengan grade tertinggi

## Referensi

1. Urma, R.-G., Fusco, M., & Mycroft, A. (2014). *Java 8 in Action: Lambdas, Streams, and Functional-Style Programming*. Manning Publications.

2. Bloch, J. (2018). *Effective Java* (3rd ed.). Addison-Wesley Professional. Chapter 7: Lambdas and Streams.

3. Horstmann, C. S. (2019). *Core Java Volume I—Fundamentals* (11th ed.). Prentice Hall. Chapter 6: Interfaces, Lambda Expressions, and Inner Classes.

4. Warburton, R. (2014). *Java 8 Lambdas: Pragmatic Functional Programming*. O'Reilly Media.

5. Oracle. (2023). *Java Language Specification: Lambda Expressions*. [https://docs.oracle.com/javase/specs/jls/se17/html/jls-15.html#jls-15.27](https://docs.oracle.com/javase/specs/jls/se17/html/jls-15.html#jls-15.27)

6. Oracle. (2023). *Java Tutorial: Lambda Expressions*. [https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html)

7. Oracle. (2023). *Package java.util.function*. [https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/function/package-summary.html](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/function/package-summary.html)

8. Schildt, H. (2018). *Java: The Complete Reference* (11th ed.). McGraw-Hill Education. Chapter 14: Lambda Expressions and Method References.

9. Subramaniam, V. (2014). *Functional Programming in Java: Harnessing the Power of Java 8 Lambda Expressions*. Pragmatic Bookshelf.

10. Naftalin, M., & Wadler, P. (2006). *Java Generics and Collections*. O'Reilly Media.

---

[◀️ Kembali ke Tutorial #10: Apa itu Anonymous Class?](10-anonymous-classes.md) | [Lanjut ke Tutorial #12: Exception Handling dalam OOP ▶️](12-exception-handling.md)

---

© 2023 Tutorial Dasar OOP di Java untuk Pemula. Semua hak cipta dilindungi.
