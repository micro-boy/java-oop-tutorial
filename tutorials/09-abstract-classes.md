# 📘 Tutorial Java OOP #09: Mengenal Class Abstract

> *"Abstract class adalah jembatan antara interface dan class konkrit, memberikan template implementasi sekaligus kebebasan abstraksi—memungkinkan kita menggabungkan yang terbaik dari kedua dunia."*

## 🎯 Tujuan Pembelajaran

Setelah mempelajari materi ini, Anda diharapkan dapat:
- Memahami konsep dan tujuan abstract class dalam pemrograman berorientasi objek
- Mendefinisikan abstract class dan abstract method di Java
- Membedakan abstract class dengan class konkrit dan interface
- Mengimplementasikan abstract class dalam hirarki inheritance
- Memahami kapan sebaiknya menggunakan abstract class dibanding interface
- Menerapkan abstract class dalam pengembangan aplikasi Java

## 📋 Daftar Isi

1. [Pendahuluan](#pendahuluan)
2. [Apa itu Abstract Class?](#apa-itu-abstract-class)
   - [Definisi dan Konsep Dasar](#definisi-dan-konsep-dasar)
   - [Abstract Class vs Class Konkrit](#abstract-class-vs-class-konkrit)
   - [Abstract Class vs Interface](#abstract-class-vs-interface)
3. [Mendefinisikan Abstract Class](#mendefinisikan-abstract-class)
   - [Sintaks dan Struktur](#sintaks-dan-struktur)
   - [Abstract Methods](#abstract-methods)
   - [Concrete Methods](#concrete-methods)
   - [Konstruktor dalam Abstract Class](#konstruktor-dalam-abstract-class)
4. [Mengimplementasikan Abstract Class](#mengimplementasikan-abstract-class)
   - [Mewarisi Abstract Class](#mewarisi-abstract-class)
   - [Mengimplementasikan Abstract Methods](#mengimplementasikan-abstract-methods)
   - [Hirarki Abstract Class](#hirarki-abstract-class)
5. [Kapan Menggunakan Abstract Class?](#kapan-menggunakan-abstract-class)
   - [Keuntungan Abstract Class](#keuntungan-abstract-class)
   - [Kasus Penggunaan yang Tepat](#kasus-penggunaan-yang-tepat)
   - [Abstract Class vs Interface: Pilihan Desain](#abstract-class-vs-interface-pilihan-desain)
6. [Best Practices](#best-practices)
7. [Latihan Praktik dengan NetBeans](#latihan-praktik-dengan-netbeans)
8. [Rangkuman](#rangkuman)
9. [Latihan Soal](#latihan-soal)
10. [Referensi](#referensi)

## Pendahuluan

Pada tutorial sebelumnya, kita telah mempelajari konsep polimorfisme dan interface dalam Java. Kedua konsep tersebut sangat penting untuk membuat aplikasi yang modular dan fleksibel. Dalam tutorial ini, kita akan mengeksplorasi konsep lain yang tidak kalah penting dalam pemrograman berorientasi objek, yaitu **abstract class**.

Abstract class menempati posisi unik dalam desain berorientasi objek, berada di antara class konkrit dan interface. Abstract class memberikan kombinasi antara implementasi konkrit dengan abstraksi, memungkinkan kita untuk mendefinisikan template dan perilaku umum, sambil tetap memberi fleksibilitas kepada class turunan untuk mengimplementasikan detail spesifik.

## Apa itu Abstract Class?

### Definisi dan Konsep Dasar

**Abstract class** adalah class yang tidak dapat di-instantiasi (tidak dapat dibuat objeknya secara langsung) dan dapat berisi abstract methods (method tanpa implementasi, mirip dengan method pada interface) maupun concrete methods (method dengan implementasi lengkap).

Abstract class dirancang untuk menjadi superclass (class dasar) yang memberikan kerangka kerja umum dan implementasi parsial bagi class-class turunannya. Class turunan harus mengimplementasikan semua abstract methods yang dideklarasikan dalam abstract class, kecuali jika class turunan itu sendiri adalah abstract class.

Analogi sederhana: 
Abstract class seperti blueprint untuk rumah yang memberikan desain dasar, seperti jumlah kamar dan struktur, tapi tidak menentukan bagaimana detail-detail seperti warna cat atau material lantai. Blueprint tersebut tidak bisa langsung digunakan untuk membangun rumah (tidak dapat di-instantiasi), tapi memberikan panduan dasar yang harus diikuti oleh desainer ketika membuat rencana pembangunan yang lebih spesifik.

### Abstract Class vs Class Konkrit

| Aspek | Abstract Class | Class Konkrit |
|-------|---------------|--------------|
| Instantiasi | Tidak dapat di-instantiasi langsung | Dapat di-instantiasi langsung |
| Method | Dapat berisi abstract methods dan concrete methods | Hanya berisi concrete methods |
| Tujuan | Mendefinisikan template dan perilaku umum | Mendefinisikan implementasi lengkap |
| Kata kunci | Menggunakan keyword `abstract` | Tidak menggunakan keyword `abstract` |
| Konstruktor | Memiliki konstruktor, tetapi tidak dapat dipanggil langsung | Memiliki konstruktor yang dapat dipanggil langsung |

### Abstract Class vs Interface

| Aspek | Abstract Class | Interface |
|-------|---------------|-----------|
| Inheritance | Single inheritance (hanya dapat mewarisi satu class) | Multiple inheritance (dapat mengimplementasikan banyak interface) |
| Method Implementation | Dapat memiliki method dengan implementasi | Secara tradisional hanya berisi abstract methods (Java 8+ mendukung default dan static methods) |
| Fields | Dapat memiliki instance variables | Hanya dapat memiliki konstanta (public static final) |
| Konstruktor | Dapat memiliki konstruktor | Tidak dapat memiliki konstruktor |
| Access Modifiers | Dapat menggunakan semua access modifiers | Method secara implisit public, fields secara implisit public static final |
| Tujuan | Template dengan implementasi parsial | Kontrak fungsionalitas tanpa implementasi |
| Keyword | `extends` | `implements` |

## Mendefinisikan Abstract Class

### Sintaks dan Struktur

Untuk mendefinisikan abstract class di Java, kita menggunakan keyword `abstract` sebelum keyword `class`:

```java
public abstract class AbstractClassName {
    // Fields
    // Constructors
    // Methods (abstract and concrete)
}
```

### Abstract Methods

Abstract methods adalah methods yang dideklarasikan tanpa implementasi (tidak memiliki body). Abstract methods hanya menentukan signature method (nama, parameter, return type, dan exception) tanpa memberikan implementasi. Class yang berisi abstract method harus dideklarasikan sebagai abstract class.

Sintaks abstract method:

```java
public abstract class Shape {
    // Abstract method
    public abstract double calculateArea();
    
    // Another abstract method
    public abstract double calculatePerimeter();
}
```

### Concrete Methods

Abstract class juga dapat berisi concrete methods (methods dengan implementasi lengkap). Ini adalah salah satu keunggulan abstract class dibandingkan interface tradisional (sebelum Java 8). Concrete methods dapat memberikan implementasi umum yang dapat digunakan oleh semua subclass tanpa perlu mendefinisikan ulang.

```java
public abstract class Shape {
    // Fields
    protected String color;
    
    // Constructor
    public Shape(String color) {
        this.color = color;
    }
    
    // Abstract methods
    public abstract double calculateArea();
    public abstract double calculatePerimeter();
    
    // Concrete method
    public void setColor(String color) {
        this.color = color;
    }
    
    // Concrete method
    public String getColor() {
        return color;
    }
    
    // Concrete method with default implementation
    public void displayDetails() {
        System.out.println("This is a " + color + " shape.");
        System.out.println("Area: " + calculateArea());
        System.out.println("Perimeter: " + calculatePerimeter());
    }
}
```

### Konstruktor dalam Abstract Class

Meskipun abstract class tidak dapat di-instantiasi secara langsung, abstract class tetap dapat dan seharusnya memiliki konstruktor. Konstruktor ini dapat dipanggil oleh konstruktor subclass menggunakan keyword `super()`.

```java
public abstract class Animal {
    private String name;
    private int age;
    
    // Constructor
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    // Getters
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
    
    // Abstract method
    public abstract void makeSound();
}

public class Dog extends Animal {
    private String breed;
    
    // Constructor calling superclass constructor
    public Dog(String name, int age, String breed) {
        super(name, age);  // Calling constructor of abstract class
        this.breed = breed;
    }
    
    @Override
    public void makeSound() {
        System.out.println("Woof! Woof!");
    }
    
    public String getBreed() {
        return breed;
    }
}
```

## Mengimplementasikan Abstract Class

### Mewarisi Abstract Class

Untuk menggunakan abstract class, kita perlu membuat subclass yang mewarisi abstract class tersebut menggunakan keyword `extends`. Subclass harus mengimplementasikan semua abstract methods dari superclass, kecuali jika subclass itu sendiri adalah abstract class.

```java
public class Circle extends Shape {
    private double radius;
    
    public Circle(String color, double radius) {
        super(color);  // Calling constructor of abstract class
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
}
```

### Mengimplementasikan Abstract Methods

Ketika mewarisi abstract class, subclass harus memberikan implementasi untuk semua abstract methods yang dideklarasikan di abstract class. Implementasi ini harus sesuai dengan signature method yang dideklarasikan di abstract class.

```java
public abstract class Vehicle {
    protected String brand;
    
    public Vehicle(String brand) {
        this.brand = brand;
    }
    
    public abstract void start();
    public abstract void stop();
    
    public void displayBrand() {
        System.out.println("Brand: " + brand);
    }
}

public class Car extends Vehicle {
    public Car(String brand) {
        super(brand);
    }
    
    @Override
    public void start() {
        System.out.println("Car starting... Turn ignition key");
    }
    
    @Override
    public void stop() {
        System.out.println("Car stopping... Apply brakes and turn off engine");
    }
}

public class Motorcycle extends Vehicle {
    public Motorcycle(String brand) {
        super(brand);
    }
    
    @Override
    public void start() {
        System.out.println("Motorcycle starting... Kick start or push button");
    }
    
    @Override
    public void stop() {
        System.out.println("Motorcycle stopping... Apply brakes and turn off engine");
    }
}
```

### Hirarki Abstract Class

Abstract class dapat membentuk hirarki dengan class lain. Sebuah abstract class dapat mewarisi class lain (konkrit atau abstract) dan dapat diwarisi oleh abstract class lain. Ini memberikan fleksibilitas dalam desain OOP.

```java
// Base abstract class
public abstract class Animal {
    public abstract void eat();
    public abstract void sleep();
}

// Intermediate abstract class
public abstract class Mammal extends Animal {
    @Override
    public void sleep() {
        System.out.println("Mammal sleeping...");
    }
    
    public abstract void giveBirth();
}

// Concrete class
public class Dog extends Mammal {
    @Override
    public void eat() {
        System.out.println("Dog eating dog food");
    }
    
    @Override
    public void giveBirth() {
        System.out.println("Dog giving birth to puppies");
    }
}
```

Dalam contoh di atas, `Mammal` adalah abstract class yang mewarisi abstract class `Animal`. `Mammal` mengimplementasikan method `sleep()` dari `Animal` tetapi menambahkan abstract method baru `giveBirth()`. `Dog` adalah class konkrit yang mewarisi `Mammal` dan harus mengimplementasikan semua abstract methods yang belum diimplementasikan: `eat()` dari `Animal` dan `giveBirth()` dari `Mammal`.

## Kapan Menggunakan Abstract Class?

### Keuntungan Abstract Class

1. **Implementasi Parsial**: Abstract class memungkinkan kita untuk memberikan implementasi parsial, menyediakan metode umum yang dapat digunakan oleh semua subclass.

2. **Code Reusability**: Dengan mendefinisikan metode umum di abstract class, kita menghindari duplikasi kode di subclass.

3. **Template Method Pattern**: Abstract class sangat cocok untuk mengimplementasikan Template Method Pattern, di mana kita mendefinisikan "skeleton" dari algoritma di superclass dan membiarkan subclass mengimplementasikan detail spesifik.

4. **Evolusi API**: Abstract class memudahkan evolusi API dengan tetap menjaga backward compatibility.

### Kasus Penggunaan yang Tepat

Abstract class sangat cocok digunakan ketika:

1. **Ada Implementasi yang Dibagikan**: Ketika ada perilaku umum yang dapat dibagikan di antara beberapa subclass.

2. **Ada State yang Perlu Dikelola**: Ketika state (variabel instance) perlu dikelola di level superclass.

3. **Memerlukan Access Modifiers Selain Public**: Ketika perlu membatasi akses ke metode/field dengan access modifiers seperti protected atau private.

4. **Template untuk Class Terkait**: Ketika ingin menyediakan template umum untuk sekelompok class yang terkait erat.

5. **Ada Default Implementation**: Ketika ada implementasi default yang masuk akal untuk beberapa metode.

### Abstract Class vs Interface: Pilihan Desain

Kapan sebaiknya menggunakan abstract class dan kapan sebaiknya menggunakan interface?

**Gunakan abstract class ketika**:
- Anda ingin berbagi kode di antara beberapa class terkait erat
- Anda ingin mengelola state yang dibutuhkan oleh semua subclass
- Anda memerlukan access modifiers selain public
- Anda perlu mendefinisikan fields non-static atau non-final
- Anda ingin menyediakan implementasi default untuk beberapa metode

**Gunakan interface ketika**:
- Anda ingin mendefinisikan kontrak yang dapat diimplementasikan oleh class yang tidak terkait erat
- Anda ingin memanfaatkan multiple inheritance
- Anda ingin fokus pada apa yang bisa dilakukan, bukan bagaimana melakukannya

## Best Practices

1. **Pilih Nama yang Jelas**: Nama abstract class sebaiknya menggambarkan konsep umum atau template yang disediakan.

2. **Dokumentasi yang Baik**: Berikan dokumentasi yang jelas untuk abstract methods, menjelaskan apa yang diharapkan dari implementasi subclass.

3. **Hindari Terlalu Banyak Abstract Methods**: Jika hampir semua metode adalah abstract, mungkin interface lebih cocok untuk kasus ini.

4. **Implementasikan Template Method Pattern**: Gunakan abstract class untuk mendefinisikan skeleton dari algoritma, dengan langkah-langkah spesifik yang diimplementasikan oleh subclass.

5. **Pertimbangkan Protected Methods**: Gunakan protected methods untuk menyediakan helper methods bagi subclass tanpa mengeksposnya ke luar.

## Latihan Praktik dengan NetBeans

Mari kita praktikkan konsep abstract class dengan membuat simulasi struktur karyawan dalam perusahaan menggunakan NetBeans.

### Langkah 1: Buat Project Baru

1. Buka NetBeans
2. Pilih `File > New Project`
3. Pilih `Java with Ant > Java Application`
4. Beri nama project `EmployeeAbstractDemo` dan klik `Finish`

### Langkah 2: Buat Abstract Class Employee

1. Klik kanan pada package project > `New > Java Class`
2. Beri nama `Employee` dan klik `Finish`
3. Ubah kode menjadi:

```java
package employeeabstractdemo;

public abstract class Employee {
    // Fields
    private String id;
    private String name;
    private double baseSalary;
    
    // Constructor
    public Employee(String id, String name, double baseSalary) {
        this.id = id;
        this.name = name;
        this.baseSalary = baseSalary;
    }
    
    // Concrete methods (getters and setters)
    public String getId() {
        return id;
    }
    
    public String getName() {
        return name;
    }
    
    public double getBaseSalary() {
        return baseSalary;
    }
    
    // Abstract method
    public abstract double calculateSalary();
    
    // Template method pattern: final method that uses abstract method
    public final void printPaySlip() {
        System.out.println("======= PAYSLIP =======");
        System.out.println("ID: " + id);
        System.out.println("Name: " + name);
        System.out.println("Base Salary: $" + baseSalary);
        System.out.println("Total Salary: $" + calculateSalary());
        printAdditionalInfo();
        System.out.println("=======================");
    }
    
    // Method to be overridden by subclasses (optional)
    protected void printAdditionalInfo() {
        // Default implementation does nothing
    }
    
    // Common behavior for all employees
    public void clockIn() {
        System.out.println(name + " has clocked in.");
    }
    
    public void clockOut() {
        System.out.println(name + " has clocked out.");
    }
}
```

### Langkah 3: Buat Class Manager yang Mewarisi Employee

1. Klik kanan pada package project > `New > Java Class`
2. Beri nama `Manager` dan klik `Finish`
3. Ubah kode menjadi:

```java
package employeeabstractdemo;

public class Manager extends Employee {
    // Additional fields
    private double managementBonus;
    private int teamSize;
    
    // Constructor
    public Manager(String id, String name, double baseSalary, double managementBonus, int teamSize) {
        super(id, name, baseSalary);
        this.managementBonus = managementBonus;
        this.teamSize = teamSize;
    }
    
    // Implementing abstract method
    @Override
    public double calculateSalary() {
        return getBaseSalary() + managementBonus + (teamSize * 100);
    }
    
    // Overriding optional method
    @Override
    protected void printAdditionalInfo() {
        System.out.println("Role: Manager");
        System.out.println("Team Size: " + teamSize);
        System.out.println("Management Bonus: $" + managementBonus);
    }
    
    // Additional behavior specific to managers
    public void callMeeting() {
        System.out.println("Manager " + getName() + " has called a meeting.");
    }
}
```

### Langkah 4: Buat Class Developer yang Mewarisi Employee

1. Klik kanan pada package project > `New > Java Class`
2. Beri nama `Developer` dan klik `Finish`
3. Ubah kode menjadi:

```java
package employeeabstractdemo;

public class Developer extends Employee {
    // Additional fields
    private String programmingLanguage;
    private int experienceYears;
    private boolean hasBonus;
    
    // Constructor
    public Developer(String id, String name, double baseSalary, 
                   String programmingLanguage, int experienceYears, boolean hasBonus) {
        super(id, name, baseSalary);
        this.programmingLanguage = programmingLanguage;
        this.experienceYears = experienceYears;
        this.hasBonus = hasBonus;
    }
    
    // Implementing abstract method
    @Override
    public double calculateSalary() {
        double salary = getBaseSalary() + (experienceYears * 500);
        if (hasBonus) {
            salary += 1000;
        }
        return salary;
    }
    
    // Overriding optional method
    @Override
    protected void printAdditionalInfo() {
        System.out.println("Role: Developer");
        System.out.println("Programming Language: " + programmingLanguage);
        System.out.println("Experience: " + experienceYears + " years");
        System.out.println("Performance Bonus: " + (hasBonus ? "Yes" : "No"));
    }
    
    // Additional behavior specific to developers
    public void writeCode() {
        System.out.println("Developer " + getName() + " is writing code in " + programmingLanguage);
    }
    
    public void debug() {
        System.out.println("Developer " + getName() + " is debugging code.");
    }
}
```

### Langkah 5: Buat Class SalesRepresentative yang Mewarisi Employee

1. Klik kanan pada package project > `New > Java Class`
2. Beri nama `SalesRepresentative` dan klik `Finish`
3. Ubah kode menjadi:

```java
package employeeabstractdemo;

public class SalesRepresentative extends Employee {
    // Additional fields
    private double salesAmount;
    private double commissionRate;
    
    // Constructor
    public SalesRepresentative(String id, String name, double baseSalary, 
                             double salesAmount, double commissionRate) {
        super(id, name, baseSalary);
        this.salesAmount = salesAmount;
        this.commissionRate = commissionRate;
    }
    
    // Implementing abstract method
    @Override
    public double calculateSalary() {
        return getBaseSalary() + (salesAmount * commissionRate);
    }
    
    // Overriding optional method
    @Override
    protected void printAdditionalInfo() {
        System.out.println("Role: Sales Representative");
        System.out.println("Sales Amount: $" + salesAmount);
        System.out.println("Commission Rate: " + (commissionRate * 100) + "%");
        System.out.println("Commission: $" + (salesAmount * commissionRate));
    }
    
    // Additional behavior specific to sales representatives
    public void makeSale(double amount) {
        salesAmount += amount;
        System.out.println("Sales Representative " + getName() + " made a sale of $" + amount);
        System.out.println("Total sales now: $" + salesAmount);
    }
}
```

### Langkah 6: Buat Abstract Class TemporaryEmployee yang Mewarisi Employee

1. Klik kanan pada package project > `New > Java Class`
2. Beri nama `TemporaryEmployee` dan klik `Finish`
3. Ubah kode menjadi:

```java
package employeeabstractdemo;

// Intermediate abstract class
public abstract class TemporaryEmployee extends Employee {
    // Additional fields
    private int contractDurationMonths;
    private String contractEndDate;
    
    // Constructor
    public TemporaryEmployee(String id, String name, double baseSalary, 
                           int contractDurationMonths, String contractEndDate) {
        super(id, name, baseSalary);
        this.contractDurationMonths = contractDurationMonths;
        this.contractEndDate = contractEndDate;
    }
    
    // Getters
    public int getContractDurationMonths() {
        return contractDurationMonths;
    }
    
    public String getContractEndDate() {
        return contractEndDate;
    }
    
    // Abstract method specific to temporary employees
    public abstract double calculateContractBonus();
    
    // Overriding method from Employee
    @Override
    protected void printAdditionalInfo() {
        System.out.println("Contract Duration: " + contractDurationMonths + " months");
        System.out.println("Contract End Date: " + contractEndDate);
    }
}
```

### Langkah 7: Buat Class Intern yang Mewarisi TemporaryEmployee

1. Klik kanan pada package project > `New > Java Class`
2. Beri nama `Intern` dan klik `Finish`
3. Ubah kode menjadi:

```java
package employeeabstractdemo;

public class Intern extends TemporaryEmployee {
    // Additional fields
    private String university;
    private boolean isPerformanceGood;
    
    // Constructor
    public Intern(String id, String name, double baseSalary, 
                int contractDurationMonths, String contractEndDate,
                String university, boolean isPerformanceGood) {
        super(id, name, baseSalary, contractDurationMonths, contractEndDate);
        this.university = university;
        this.isPerformanceGood = isPerformanceGood;
    }
    
    // Implementing abstract method from Employee
    @Override
    public double calculateSalary() {
        double salary = getBaseSalary();
        if (isPerformanceGood) {
            salary += 200;
        }
        return salary;
    }
    
    // Implementing abstract method from TemporaryEmployee
    @Override
    public double calculateContractBonus() {
        return isPerformanceGood ? getContractDurationMonths() * 50 : 0;
    }
    
    // Overriding method from TemporaryEmployee
    @Override
    protected void printAdditionalInfo() {
        super.printAdditionalInfo();
        System.out.println("Role: Intern");
        System.out.println("University: " + university);
        System.out.println("Performance: " + (isPerformanceGood ? "Good" : "Needs Improvement"));
        System.out.println("Contract Bonus: $" + calculateContractBonus());
    }
    
    // Additional behavior specific to interns
    public void attendTraining() {
        System.out.println("Intern " + getName() + " is attending training.");
    }
}
```

### Langkah 8: Buat Kelas Main

1. Buka file main (biasanya `EmployeeAbstractDemo.java`)
2. Ubah kode menjadi:

```java
package employeeabstractdemo;

public class EmployeeAbstractDemo {
    public static void main(String[] args) {
        System.out.println("===== EMPLOYEE ABSTRACT CLASS DEMO =====\n");
        
        // Tidak bisa membuat instance dari abstract class Employee
        // Employee employee = new Employee("E001", "John Doe", 5000);  // Error
        
        // Membuat objects dari concrete classes
        Manager manager = new Manager("M001", "Alice Smith", 8000, 2000, 5);
        Developer developer = new Developer("D001", "Bob Johnson", 7000, "Java", 5, true);
        SalesRepresentative salesRep = new SalesRepresentative("S001", "Charlie Brown", 4000, 50000, 0.05);
        Intern intern = new Intern("I001", "Diana Prince", 2000, 6, "2023-12-31", "MIT", true);
        
        // Demonstrasi polimorfisme dengan abstract class
        Employee[] employees = {manager, developer, salesRep, intern};
        
        // Memanggil method untuk setiap employee
        for (Employee emp : employees) {
            System.out.println("\n--- Employee Information ---");
            emp.clockIn();
            
            // Memanggil template method
            emp.printPaySlip();
            
            // Demonstrasi method khusus untuk masing-masing jenis employee
            if (emp instanceof Manager) {
                Manager mgr = (Manager) emp;
                mgr.callMeeting();
            } else if (emp instanceof Developer) {
                Developer dev = (Developer) emp;
                dev.writeCode();
                dev.debug();
            } else if (emp instanceof SalesRepresentative) {
                SalesRepresentative sales = (SalesRepresentative) emp;
                sales.makeSale(10000);
            } else if (emp instanceof Intern) {
                Intern int1 = (Intern) emp;
                int1.attendTraining();
                System.out.println("Contract bonus: $" + int1.calculateContractBonus());
            }
            
            emp.clockOut();
            System.out.println("-------------------------");
        }
        
        // Demonstrasi hirarki abstract class
        System.out.println("\n===== ABSTRACT CLASS HIERARCHY DEMO =====");
        System.out.println("\nIntern is a TemporaryEmployee: " + (intern instanceof TemporaryEmployee));
        System.out.println("Intern is an Employee: " + (intern instanceof Employee));
        System.out.println("Developer is a TemporaryEmployee: " + (developer instanceof TemporaryEmployee));
    }
}
```

### Langkah 9: Jalankan Program

1. Klik tombol Run (F6) untuk menjalankan program
2. Amati output yang dihasilkan

## Rangkuman

Dalam tutorial ini, kita telah mempelajari:

✅ **Abstract Class** - Kelas yang tidak dapat di-instantiasi dan dapat berisi abstract methods dan concrete methods

✅ **Abstract Methods** - Methods yang dideklarasikan tanpa implementasi dan harus diimplementasikan oleh subclass

✅ **Perbedaan antara Abstract Class, Class Konkrit, dan Interface** - Karakteristik dan use cases untuk masing-masing

✅ **Konstruktor dalam Abstract Class** - Digunakan oleh subclass melalui keyword `super()`

✅ **Template Method Pattern** - Mendefinisikan kerangka algoritma di abstract class dan membiarkan subclass mengimplementasikan langkah-langkah spesifik

✅ **Hierarki Abstract Class** - Abstract class dapat mewarisi dan diwarisi oleh abstract class lain

✅ **Kapan Menggunakan Abstract Class** - Situasi di mana abstract class lebih cocok daripada interface

Abstract class adalah alat powerful dalam pemrograman berorientasi objek yang memungkinkan kita untuk menyeimbangkan antara reusability dan fleksibilitas. Dengan memahami kapan dan bagaimana menggunakan abstract class, Anda dapat mendesain aplikasi yang lebih modular, maintainable, dan extensible.

## Latihan Soal

1. Apa perbedaan utama antara abstract class dan interface di Java? Dalam situasi apa Anda akan memilih menggunakan abstract class daripada interface?

2. Sebutkan karakteristik dari abstract method. Bagaimana cara mendefinisikan abstract method dalam abstract class?

3. Apakah abstract class dapat di-instantiasi secara langsung? Jelaskan alasannya.

4. Mengapa abstract class memiliki konstruktor meskipun tidak dapat di-instantiasi secara langsung?

5. Apa yang dimaksud dengan Template Method Pattern? Berikan contoh implementasi pattern ini menggunakan abstract class.

6. Buatlah abstract class `Shape` dengan abstract methods `calculateArea()` dan `calculatePerimeter()`. Kemudian buat tiga subclass: `Circle`, `Rectangle`, dan `Triangle` yang mengimplementasikan abstract methods tersebut.

7. Apakah subclass dari abstract class harus mengimplementasikan semua abstract methods? Bagaimana jika subclass tidak ingin mengimplementasikan beberapa abstract methods?

8. Jelaskan konsep hirarki abstract class. Berikan contoh kasus di mana hirarki abstract class berguna dalam pengembangan aplikasi.

9. Apakah abstract class dapat mengimplementasikan interface? Jika ya, berikan contoh kasus penggunaan.

10. Buatlah sistem bank sederhana dengan abstract class `Account` yang memiliki abstract method `calculateInterest()`. Implementasikan subclass `SavingsAccount` dan `CheckingAccount` dengan perhitungan bunga yang berbeda.

## Referensi

1. Bloch, J. (2018). *Effective Java* (3rd ed.). Addison-Wesley Professional. Chapter 4: Classes and Interfaces.

2. Deitel, P., & Deitel, H. (2020). *Java How to Program, Early Objects* (11th ed.). Pearson. Chapter 10: Object-Oriented Programming: Polymorphism and Interfaces.

3. Eckel, B. (2006). *Thinking in Java* (4th ed.). Prentice Hall. Chapter 7: Polymorphism.

4. Gamma, E., Helm, R., Johnson, R., & Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley Professional. Chapter 3: Template Method Pattern.

5. Horstmann, C. S. (2019). *Core Java Volume I—Fundamentals* (11th ed.). Prentice Hall. Chapter 5: Inheritance.

6. McLaughlin, B. D., Pollice, G., & West, D. (2006). *Head First Object-Oriented Analysis and Design*. O'Reilly Media. Chapter 6: Solving Really Big Problems.

7. Oracle. (2023). *Java Language Specification: Abstract Classes*. [https://docs.oracle.com/javase/specs/jls/se17/html/jls-8.html#jls-8.1.1.1](https://docs.oracle.com/javase/specs/jls/se17/html/jls-8.html#jls-8.1.1.1)

8. Oracle. (2023). *Java Tutorial: Abstract Methods and Classes*. [https://docs.oracle.com/javase/tutorial/java/IandI/abstract.html](https://docs.oracle.com/javase/tutorial/java/IandI/abstract.html)

9. Schildt, H. (2018). *Java: The Complete Reference* (11th ed.). McGraw-Hill Education. Chapter 8: Inheritance.

10. Sierra, K., & Bates, B. (2005). *Head First Java* (2nd ed.). O'Reilly Media. Chapter 8: Interfaces and Abstract Classes.

---

[◀️ Kembali ke Tutorial #08: Menggunakan Interface](08-interface.md) | [Lanjut ke Tutorial #10: Apa itu Anonymous Class? ▶️](10-anonymous-classes.md)

---

© 2023 Tutorial Dasar OOP di Java untuk Pemula. Semua hak cipta dilindungi.
