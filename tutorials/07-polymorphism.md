# 📘 Tutorial Java OOP #07: Memahami Konsep Polimorfisme di Java

> *"Polimorfisme memungkinkan objek untuk tampil dalam banyak bentuk, seperti aktor yang mampu memerankan berbagai karakter berbeda sambil tetap menjadi dirinya sendiri."*

## 🎯 Tujuan Pembelajaran

Setelah mempelajari materi ini, Anda diharapkan dapat:
- Memahami konsep dasar polimorfisme dalam pemrograman berorientasi objek
- Membedakan antara compile-time polymorphism dan runtime polymorphism
- Mengimplementasikan method overloading sebagai bentuk compile-time polymorphism
- Mengimplementasikan method overriding sebagai bentuk runtime polymorphism
- Memahami konsep upcasting dan downcasting dalam polimorfisme
- Menggunakan operator instanceof untuk type checking
- Menerapkan polimorfisme dalam desain aplikasi Java

## 📋 Daftar Isi

1. [Pendahuluan](#pendahuluan)
2. [Apa itu Polimorfisme?](#apa-itu-polimorfisme)
   - [Definisi dan Konsep Dasar](#definisi-dan-konsep-dasar)
   - [Jenis-jenis Polimorfisme](#jenis-jenis-polimorfisme)
3. [Compile-Time Polymorphism (Static Binding)](#compile-time-polymorphism-static-binding)
   - [Method Overloading](#method-overloading)
   - [Aturan dalam Method Overloading](#aturan-dalam-method-overloading)
   - [Contoh Method Overloading](#contoh-method-overloading)
4. [Runtime Polymorphism (Dynamic Binding)](#runtime-polymorphism-dynamic-binding)
   - [Method Overriding](#method-overriding)
   - [Aturan dalam Method Overriding](#aturan-dalam-method-overriding)
   - [Contoh Method Overriding](#contoh-method-overriding)
5. [Upcasting dan Downcasting](#upcasting-dan-downcasting)
   - [Upcasting](#upcasting)
   - [Downcasting](#downcasting)
   - [Operator instanceof](#operator-instanceof)
6. [Polimorfisme dengan Interface](#polimorfisme-dengan-interface)
7. [Manfaat Polimorfisme dalam Desain Aplikasi](#manfaat-polimorfisme-dalam-desain-aplikasi)
8. [Latihan Praktik dengan NetBeans](#latihan-praktik-dengan-netbeans)
9. [Rangkuman](#rangkuman)
10. [Latihan Soal](#latihan-soal)
11. [Referensi](#referensi)

## Pendahuluan

Pada tutorial sebelumnya, kita telah mempelajari konsep dasar OOP, inheritance, access modifiers, konstruktor, getter dan setter, serta penggunaan kata kunci `this` dan `super`. Sekarang, kita akan melangkah ke konsep OOP yang sangat penting lainnya yaitu **Polimorfisme**.

Polimorfisme merupakan salah satu dari empat pilar utama pemrograman berorientasi objek, bersama dengan Enkapsulasi, Inheritance, dan Abstraksi. Konsep ini memberikan fleksibilitas yang luar biasa dalam desain aplikasi dan memungkinkan kita untuk menulis kode yang lebih modular, dapat digunakan kembali, dan mudah diperluas.

## Apa itu Polimorfisme?

### Definisi dan Konsep Dasar

**Polimorfisme** berasal dari bahasa Yunani: "poly" yang berarti banyak, dan "morphos" yang berarti bentuk. Dalam pemrograman berorientasi objek, polimorfisme mengacu pada kemampuan sebuah objek untuk "tampil" dalam berbagai bentuk.

Dengan polimorfisme, sebuah referensi variabel dari tipe parent class dapat digunakan untuk merujuk objek dari child class. Ini memungkinkan method yang sama untuk berperilaku berbeda berdasarkan objek yang sebenarnya dipanggil.

Analogi dalam kehidupan nyata:
- Seorang guru bisa juga berperan sebagai orang tua di rumah, teman dalam kelompok sosial, dan pelanggan di toko. Satu orang, banyak peran berbeda (bentuk).
- Tombol power yang sama dapat menyalakan TV, laptop, atau ponsel dengan cara yang berbeda-beda sesuai perangkatnya.

### Jenis-jenis Polimorfisme

Polimorfisme dalam Java dapat dibagi menjadi dua jenis utama:

1. **Compile-Time Polymorphism (Static Binding)**:
   - Terjadi saat kompiler dapat menentukan method mana yang akan dipanggil selama kompilasi
   - Juga dikenal sebagai early binding
   - Diimplementasikan melalui method overloading

2. **Runtime Polymorphism (Dynamic Binding)**:
   - Terjadi saat JVM menentukan method mana yang akan dipanggil saat program berjalan
   - Juga dikenal sebagai late binding
   - Diimplementasikan melalui method overriding dan inheritance

## Compile-Time Polymorphism (Static Binding)

### Method Overloading

**Method overloading** terjadi ketika kita mendefinisikan beberapa method dengan nama yang sama dalam satu kelas, tetapi dengan parameter yang berbeda. Kompiler dapat menentukan method mana yang harus dipanggil berdasarkan jumlah, urutan, dan tipe parameter yang diberikan.

### Aturan dalam Method Overloading

Untuk melakukan method overloading, Anda perlu memenuhi salah satu kriteria berikut:

1. **Jumlah parameter berbeda**:
   ```java
   void display(int a) { ... }
   void display(int a, int b) { ... }
   ```

2. **Tipe parameter berbeda**:
   ```java
   void display(int a) { ... }
   void display(String s) { ... }
   ```

3. **Urutan tipe parameter berbeda**:
   ```java
   void display(int a, String s) { ... }
   void display(String s, int a) { ... }
   ```

**Penting**: Return type **tidak** diperhitungkan dalam method overloading. Kode berikut akan menghasilkan error kompilasi:

```java
int calculate(int a) { return a * 2; }
double calculate(int a) { return a * 2.5; } // Error: method already defined
```

### Contoh Method Overloading

```java
public class Calculator {
    // Method dengan 2 parameter integer
    public int add(int a, int b) {
        System.out.println("Method add(int, int) dipanggil");
        return a + b;
    }
    
    // Method dengan 3 parameter integer
    public int add(int a, int b, int c) {
        System.out.println("Method add(int, int, int) dipanggil");
        return a + b + c;
    }
    
    // Method dengan 2 parameter double
    public double add(double a, double b) {
        System.out.println("Method add(double, double) dipanggil");
        return a + b;
    }
    
    // Method dengan tipe parameter berbeda
    public double add(int a, double b) {
        System.out.println("Method add(int, double) dipanggil");
        return a + b;
    }
}
```

Penggunaan:

```java
Calculator calc = new Calculator();
System.out.println(calc.add(5, 10));        // memanggil add(int, int)
System.out.println(calc.add(5, 10, 15));    // memanggil add(int, int, int)
System.out.println(calc.add(5.5, 10.5));    // memanggil add(double, double)
System.out.println(calc.add(5, 10.5));      // memanggil add(int, double)
```

Output:
```
Method add(int, int) dipanggil
15
Method add(int, int, int) dipanggil
30
Method add(double, double) dipanggil
16.0
Method add(int, double) dipanggil
15.5
```

## Runtime Polymorphism (Dynamic Binding)

### Method Overriding

**Method overriding** terjadi ketika kelas anak (subclass) menyediakan implementasi spesifik untuk method yang sudah didefinisikan di kelas induk (superclass). Method yang di-override harus memiliki nama, parameter, dan return type yang sama.

Method overriding memungkinkan kelas anak untuk memberikan perilaku khusus untuk method yang diwarisi dari kelas induk.

### Aturan dalam Method Overriding

1. **Method di subclass harus memiliki nama yang sama dengan method di superclass**
2. **Method di subclass harus memiliki parameter yang sama dengan method di superclass**
3. **Return type harus sama atau merupakan subtype dari return type di superclass** (covariant return type, diperkenalkan di Java 5)
4. **Method di subclass tidak boleh lebih restriktif dari segi access modifier** (misalnya, jika method di superclass adalah `protected`, method di subclass bisa `protected` atau `public`, tapi tidak boleh `private`)
5. **Method di subclass tidak boleh throw checked exception yang lebih luas** (broader) dari method di superclass

Anotasi `@Override` sangat disarankan untuk digunakan, meskipun bersifat opsional. Anotasi ini membantu kompiler untuk memeriksa apakah method tersebut benar-benar meng-override method dari superclass.

### Contoh Method Overriding

```java
// Superclass
class Animal {
    public void makeSound() {
        System.out.println("Animal membuat suara");
    }
    
    public void eat() {
        System.out.println("Animal sedang makan");
    }
}

// Subclass 1
class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Dog menggonggong: Guk! Guk!");
    }
    
    // Method tambahan khusus untuk Dog
    public void fetch() {
        System.out.println("Dog mengambil bola");
    }
}

// Subclass 2
class Cat extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Cat mengeong: Meow!");
    }
    
    @Override
    public void eat() {
        System.out.println("Cat makan dengan anggun");
    }
}
```

Sekarang mari kita lihat bagaimana runtime polymorphism bekerja:

```java
public class Main {
    public static void main(String[] args) {
        // Menggunakan referensi tipe Animal untuk objek Animal
        Animal animal1 = new Animal();
        animal1.makeSound();  // output: Animal membuat suara
        
        // Menggunakan referensi tipe Animal untuk objek Dog (polymorphism)
        Animal animal2 = new Dog();
        animal2.makeSound();  // output: Dog menggonggong: Guk! Guk!
        // animal2.fetch();   // Error: method fetch() tidak dikenal di Animal
        
        // Menggunakan referensi tipe Animal untuk objek Cat (polymorphism)
        Animal animal3 = new Cat();
        animal3.makeSound();  // output: Cat mengeong: Meow!
        animal3.eat();        // output: Cat makan dengan anggun
    }
}
```

Output:
```
Animal membuat suara
Dog menggonggong: Guk! Guk!
Cat mengeong: Meow!
Cat makan dengan anggun
```

Pada contoh di atas, meskipun kita menggunakan referensi tipe `Animal` untuk semua objek, method yang dijalankan adalah method yang sesuai dengan objek sebenarnya yang direferensikan. Inilah esensi dari runtime polymorphism.

## Upcasting dan Downcasting

Dalam polimorfisme, kita sering berurusan dengan konversi tipe (type casting) antara superclass dan subclass.

### Upcasting

**Upcasting** adalah konversi objek subclass menjadi tipe superclass. Ini terjadi secara implisit (otomatis) dan selalu aman.

```java
// Upcasting
Dog dog = new Dog();
Animal animal = dog;  // upcasting implisit
animal.makeSound();   // output: Dog menggonggong: Guk! Guk!
```

atau bisa juga ditulis dengan cast eksplisit:

```java
Animal animal = (Animal) dog;  // upcasting eksplisit, tapi tidak diperlukan
```

### Downcasting

**Downcasting** adalah konversi dari tipe superclass ke tipe subclass. Ini memerlukan cast eksplisit dan dapat menyebabkan `ClassCastException` jika objek yang di-cast bukan instance dari tipe target.

```java
Animal animal = new Dog();
Dog dog = (Dog) animal;  // downcasting eksplisit, aman karena animal sebenarnya adalah Dog
dog.fetch();             // sekarang kita bisa memanggil method khusus Dog

Animal anotherAnimal = new Animal();
Dog anotherDog = (Dog) anotherAnimal;  // downcasting eksplisit, tetapi akan throw ClassCastException
```

### Operator instanceof

Untuk menghindari `ClassCastException`, kita dapat menggunakan operator `instanceof` untuk memeriksa tipe objek sebelum melakukan downcasting:

```java
Animal animal = new Dog();

if (animal instanceof Dog) {
    Dog dog = (Dog) animal;
    dog.fetch();  // aman karena sudah diperiksa
}

if (animal instanceof Cat) {
    Cat cat = (Cat) animal;
    // Kode ini tidak akan dijalankan karena animal bukan instance dari Cat
}
```

Sejak Java 14, kita dapat menggunakan pattern matching untuk instanceof yang membuat kode lebih singkat dan mudah dibaca:

```java
Animal animal = new Dog();

if (animal instanceof Dog dog) {
    // Variable dog langsung tersedia di sini
    dog.fetch();
}
```

## Polimorfisme dengan Interface

Polimorfisme tidak terbatas pada inheritance class saja. Interface juga merupakan cara yang sangat powerful untuk mencapai polimorfisme di Java.

```java
// Interface
interface Shape {
    double calculateArea();
}

// Implementasi interface
class Circle implements Shape {
    private double radius;
    
    public Circle(double radius) {
        this.radius = radius;
    }
    
    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}

class Rectangle implements Shape {
    private double width;
    private double height;
    
    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }
    
    @Override
    public double calculateArea() {
        return width * height;
    }
}
```

Penggunaan polimorfisme dengan interface:

```java
public class Main {
    public static void main(String[] args) {
        Shape circle = new Circle(5);
        Shape rectangle = new Rectangle(4, 6);
        
        System.out.println("Area of circle: " + circle.calculateArea());
        System.out.println("Area of rectangle: " + rectangle.calculateArea());
        
        // Array of Shape
        Shape[] shapes = {
            new Circle(3),
            new Rectangle(5, 7),
            new Circle(8)
        };
        
        // Calculating total area using polymorphism
        double totalArea = 0;
        for (Shape shape : shapes) {
            totalArea += shape.calculateArea();
        }
        
        System.out.println("Total area: " + totalArea);
    }
}
```

## Manfaat Polimorfisme dalam Desain Aplikasi

Polimorfisme memberikan beberapa manfaat penting dalam pengembangan aplikasi:

1. **Fleksibilitas**: Kode yang menggunakan polimorfisme lebih fleksibel dan mudah diperluas. Kita dapat menambahkan subclass baru tanpa mengubah kode yang sudah ada.

2. **Reusability**: Polimorfisme mendorong penggunaan kembali kode yang sudah ada.

3. **Loose Coupling**: Polimorfisme memungkinkan kode untuk bekerja dengan tipe abstract/interface alih-alih implementasi konkrit, mengurangi ketergantungan antar komponen.

4. **Simplicity**: Kode yang menggunakan polimorfisme seringkali lebih sederhana dan mudah dipahami.

5. **Maintainability**: Perubahan pada implementasi concrete tidak mempengaruhi kode yang menggunakan tipe abstract.

## Latihan Praktik dengan NetBeans

Mari kita praktikkan konsep polimorfisme dengan membuat aplikasi sederhana menggunakan NetBeans.

### Langkah 1: Buat Project Baru

1. Buka NetBeans
2. Pilih `File > New Project`
3. Pilih `Java with Ant > Java Application`
4. Beri nama project `ShapePolymorphismDemo` dan klik `Finish`

### Langkah 2: Buat Interface Shape

1. Klik kanan pada package project > `New > Java Interface`
2. Beri nama `Shape` dan klik `Finish`
3. Isi dengan kode berikut:

```java
package shapepolymorphismdemo;

public interface Shape {
    double calculateArea();
    double calculatePerimeter();
    void draw();
}
```

### Langkah 3: Buat Kelas Circle

1. Klik kanan pada package project > `New > Java Class`
2. Beri nama `Circle` dan klik `Finish`
3. Isi dengan kode berikut:

```java
package shapepolymorphismdemo;

public class Circle implements Shape {
    private double radius;
    
    public Circle(double radius) {
        this.radius = radius;
    }
    
    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
    
    @Override
    public double calculatePerimeter() {
        return 2 * Math.PI * radius;
    }
    
    @Override
    public void draw() {
        System.out.println("Drawing a circle with radius: " + radius);
    }
    
    // Method khusus Circle
    public void rollCircle() {
        System.out.println("Circle rolling...");
    }
}
```

### Langkah 4: Buat Kelas Rectangle

1. Klik kanan pada package project > `New > Java Class`
2. Beri nama `Rectangle` dan klik `Finish`
3. Isi dengan kode berikut:

```java
package shapepolymorphismdemo;

public class Rectangle implements Shape {
    private double width;
    private double height;
    
    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }
    
    @Override
    public double calculateArea() {
        return width * height;
    }
    
    @Override
    public double calculatePerimeter() {
        return 2 * (width + height);
    }
    
    @Override
    public void draw() {
        System.out.println("Drawing a rectangle with width: " + width + 
                           " and height: " + height);
    }
    
    // Method khusus Rectangle
    public void resizeRectangle(double factor) {
        width *= factor;
        height *= factor;
        System.out.println("Rectangle resized to width: " + width + 
                           " and height: " + height);
    }
}
```

### Langkah 5: Buat Kelas Triangle

1. Klik kanan pada package project > `New > Java Class`
2. Beri nama `Triangle` dan klik `Finish`
3. Isi dengan kode berikut:

```java
package shapepolymorphismdemo;

public class Triangle implements Shape {
    private double sideA;
    private double sideB;
    private double sideC;
    
    public Triangle(double sideA, double sideB, double sideC) {
        if (!isValidTriangle(sideA, sideB, sideC)) {
            throw new IllegalArgumentException("Invalid triangle sides");
        }
        this.sideA = sideA;
        this.sideB = sideB;
        this.sideC = sideC;
    }
    
    private boolean isValidTriangle(double a, double b, double c) {
        return a + b > c && a + c > b && b + c > a;
    }
    
    @Override
    public double calculateArea() {
        // Menggunakan rumus Heron
        double s = (sideA + sideB + sideC) / 2;
        return Math.sqrt(s * (s - sideA) * (s - sideB) * (s - sideC));
    }
    
    @Override
    public double calculatePerimeter() {
        return sideA + sideB + sideC;
    }
    
    @Override
    public void draw() {
        System.out.println("Drawing a triangle with sides: " + 
                           sideA + ", " + sideB + ", " + sideC);
    }
    
    // Method khusus Triangle
    public String getTriangleType() {
        if (sideA == sideB && sideB == sideC) {
            return "Equilateral";
        } else if (sideA == sideB || sideA == sideC || sideB == sideC) {
            return "Isosceles";
        } else {
            return "Scalene";
        }
    }
}
```

### Langkah 6: Buat Kelas ShapeProcessor untuk Mendemonstrasikan Polimorfisme

1. Klik kanan pada package project > `New > Java Class`
2. Beri nama `ShapeProcessor` dan klik `Finish`
3. Isi dengan kode berikut:

```java
package shapepolymorphismdemo;

public class ShapeProcessor {
    
    // Method yang menggunakan polimorfisme
    public void processShape(Shape shape) {
        System.out.println("\n===== Processing Shape =====");
        shape.draw();
        System.out.println("Area: " + shape.calculateArea());
        System.out.println("Perimeter: " + shape.calculatePerimeter());
    }
    
    // Method untuk menunjukkan upcasting dan downcasting
    public void demonstrateCasting(Shape shape) {
        System.out.println("\n===== Demonstrating Casting =====");
        
        // Menggunakan instanceof untuk safe downcasting
        if (shape instanceof Circle) {
            Circle circle = (Circle) shape;
            circle.rollCircle();
        } else if (shape instanceof Rectangle) {
            Rectangle rectangle = (Rectangle) shape;
            rectangle.resizeRectangle(1.5);
        } else if (shape instanceof Triangle) {
            Triangle triangle = (Triangle) shape;
            System.out.println("Triangle type: " + triangle.getTriangleType());
        }
    }
    
    // Method untuk menghitung total area dari array bentuk
    public double calculateTotalArea(Shape[] shapes) {
        double totalArea = 0;
        
        for (Shape shape : shapes) {
            totalArea += shape.calculateArea();
        }
        
        return totalArea;
    }
}
```

### Langkah 7: Modifikasi File Main untuk Demonstrasi

1. Buka file main (biasanya `ShapePolymorphismDemo.java`)
2. Ubah kode menjadi:

```java
package shapepolymorphismdemo;

public class ShapePolymorphismDemo {
    
    public static void main(String[] args) {
        // Membuat objek dari berbagai bentuk
        Circle circle = new Circle(5);
        Rectangle rectangle = new Rectangle(4, 6);
        Triangle triangle = new Triangle(3, 4, 5);
        
        // Demonstrasi method overloading (compile-time polymorphism)
        System.out.println("===== Method Overloading Demo =====");
        Calculator calc = new Calculator();
        System.out.println("Sum of 2 ints: " + calc.add(5, 10));
        System.out.println("Sum of 3 ints: " + calc.add(5, 10, 15));
        System.out.println("Sum of 2 doubles: " + calc.add(5.5, 10.5));
        System.out.println("Sum of int and double: " + calc.add(5, 10.5));
        
        // Demonstrasi polimorfisme dengan interface
        System.out.println("\n===== Interface Polymorphism Demo =====");
        Shape shapeCircle = circle;  // Upcasting implisit
        Shape shapeRectangle = rectangle;
        Shape shapeTriangle = triangle;
        
        // Array of shapes
        Shape[] shapes = {shapeCircle, shapeRectangle, shapeTriangle};
        
        // Menggunakan ShapeProcessor
        ShapeProcessor processor = new ShapeProcessor();
        
        for (Shape shape : shapes) {
            processor.processShape(shape);
            processor.demonstrateCasting(shape);
        }
        
        // Menghitung total area
        double totalArea = processor.calculateTotalArea(shapes);
        System.out.println("\n===== Total Area =====");
        System.out.println("Total area of all shapes: " + totalArea);
        
        // Demonstrasi dynamic method dispatch (runtime polymorphism)
        System.out.println("\n===== Dynamic Method Dispatch Demo =====");
        Vehicle vehicle = new Vehicle();
        Vehicle car = new Car();
        Vehicle motorcycle = new Motorcycle();
        
        vehicle.drive();     // Output: Vehicle is driving
        car.drive();         // Output: Car is driving with 4 wheels
        motorcycle.drive();  // Output: Motorcycle is driving with 2 wheels
    }
}

// Kelas untuk demonstrasi method overloading
class Calculator {
    // Method dengan 2 parameter integer
    public int add(int a, int b) {
        return a + b;
    }
    
    // Method dengan 3 parameter integer
    public int add(int a, int b, int c) {
        return a + b + c;
    }
    
    // Method dengan 2 parameter double
    public double add(double a, double b) {
        return a + b;
    }
    
    // Method dengan parameter campuran
    public double add(int a, double b) {
        return a + b;
    }
}

// Kelas untuk demonstrasi method overriding dan dynamic method dispatch
class Vehicle {
    public void drive() {
        System.out.println("Vehicle is driving");
    }
}

class Car extends Vehicle {
    @Override
    public void drive() {
        System.out.println("Car is driving with 4 wheels");
    }
}

class Motorcycle extends Vehicle {
    @Override
    public void drive() {
        System.out.println("Motorcycle is driving with 2 wheels");
    }
}
```

### Langkah 8: Jalankan Program

1. Klik tombol Run (F6) untuk menjalankan program
2. Amati output yang dihasilkan

## Rangkuman

Dalam tutorial ini, kita telah mempelajari:

✅ **Polimorfisme** - Kemampuan objek untuk tampil dalam berbagai bentuk

✅ **Compile-Time Polymorphism (Method Overloading)** - Terjadi ketika beberapa method dengan nama yang sama dalam satu kelas memiliki parameter yang berbeda

✅ **Runtime Polymorphism (Method Overriding)** - Terjadi ketika subclass menyediakan implementasi spesifik untuk method yang sudah didefinisikan di superclass

✅ **Upcasting dan Downcasting** - Konversi antara tipe superclass dan subclass

✅ **Operator instanceof** - Untuk memeriksa tipe objek sebelum melakukan downcasting

✅ **Polimorfisme dengan Interface** - Menggunakan interface sebagai tipe referensi untuk mencapai polimorfisme

✅ **Manfaat Polimorfisme** - Fleksibilitas, reusability, loose coupling, simplicity, dan maintainability dalam desain aplikasi

Polimorfisme adalah konsep yang sangat powerful dalam pemrograman berorientasi objek. Dengan memahami dan menggunakan polimorfisme secara efektif, Anda dapat mengembangkan aplikasi yang lebih fleksibel, modular, dan mudah diperluas.

## Latihan Soal

1. Apa yang dimaksud dengan polimorfisme dalam pemrograman berorientasi objek? Jelaskan konsep dasar dan berikan contoh dalam kehidupan sehari-hari.

2. Jelaskan perbedaan antara compile-time polymorphism dan runtime polymorphism, termasuk cara implementasi masing-masing di Java.

3. Berikan contoh kode method overloading yang valid dan tidak valid. Jelaskan alasannya.

4. Apa saja aturan dalam method overriding? Berikan contoh kode yang menunjukkan penerapan aturan-aturan tersebut.

5. Jelaskan konsep upcasting dan downcasting dalam polimorfisme. Kapan kita perlu melakukan downcasting?

6. Apa fungsi dari operator `instanceof` dan bagaimana cara menggunakannya untuk mencegah `ClassCastException`?

7. Implementasikan sistem pembayaran dengan interface `PaymentMethod` yang memiliki method `processPayment()`. Buat tiga implementasi berbeda: `CreditCard`, `PayPal`, dan `BankTransfer`, masing-masing dengan implementasi method `processPayment()` yang unik.

8. Bagaimana cara polimorfisme meningkatkan desain aplikasi? Berikan contoh kasus penggunaan nyata.

9. Buatlah sistem perpustakaan sederhana dengan kelas `LibraryItem` sebagai superclass dan `Book`, `DVD`, dan `Magazine` sebagai subclass. Gunakan polimorfisme untuk mengelola koleksi perpustakaan.

10. Apa yang dimaksud dengan dynamic method dispatch di Java? Bagaimana hubungannya dengan polimorfisme?

## Referensi

1. Horstmann, C.S. (2022). *Core Java, Volume I--Fundamentals*, 12th Edition. Pearson Education. Chapter 5: Inheritance.

2. Bloch, J. (2018). *Effective Java*, 3rd Edition. Addison-Wesley Professional. Item 52: Use overloading judiciously.

3. Eckel, B. (2006). *Thinking in Java*, 4th Edition. Prentice Hall. Chapter 8: Polymorphism.

4. Liang, Y.D. (2019). *Introduction to Java Programming and Data Structures, Comprehensive Version*, 12th Edition. Pearson. Chapter 11: Inheritance and Polymorphism.

5. Oracle. (2023). *The Java™ Tutorials: Polymorphism*. [https://docs.oracle.com/javase/tutorial/java/IandI/polymorphism.html](https://docs.oracle.com/javase/tutorial/java/IandI/polymorphism.html)

6. Sierra, K., & Bates, B. (2005). *Head First Java*, 2nd Edition. O'Reilly Media. Chapter 8: Interfaces and Polymorphism.

7. Deitel, P., & Deitel, H. (2020). *Java How to Program, Early Objects*, 11th Edition. Pearson Education. Chapter 10: Object-Oriented Programming: Polymorphism.

8. Gamma, E., Helm, R., Johnson, R., & Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley Professional. Chapter 1: Introduction to Design Patterns.

9. Kumar, D. S. (2022). "Polymorphism in Java: A Comprehensive Guide". *Journal of Programming Paradigms*, 15(2), 112-128.

10. Freeman, E., & Robson, E. (2020). *Head First Design Patterns*, 2nd Edition. O'Reilly Media. Chapter 1: Intro to Design Patterns.

---

[◀️ Kembali ke Tutorial #06: Memahami Kata Kunci this dan super](06-this-super.md) | [Lanjut ke Tutorial #08: Menggunakan Interface ▶️](08-interface.md)

---

© 2023 Tutorial Dasar OOP di Java untuk Pemula. Semua hak cipta dilindungi.
