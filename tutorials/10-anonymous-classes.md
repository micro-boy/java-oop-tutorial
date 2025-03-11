# 📘 Tutorial Java OOP #10: Apa itu Anonymous Class?

> *"Anonymous class adalah ekspresi ketika kode perlu bicara dengan singkat; seperti pesan dalam botol yang berlayar hanya sekali—berisi implementasi tanpa nama yang melakukan tugasnya lalu menghilang."*

## 🎯 Tujuan Pembelajaran

Setelah mempelajari materi ini, Anda diharapkan dapat:
- Memahami konsep dan tujuan anonymous class dalam Java
- Membuat dan mengimplementasikan anonymous class untuk interface dan abstract class
- Mengetahui kapan sebaiknya menggunakan atau tidak menggunakan anonymous class
- Memahami perbedaan antara anonymous class dan class biasa
- Membedakan kasus penggunaan anonymous class vs lambda expressions
- Menerapkan anonymous class dalam pengembangan aplikasi

## 📋 Daftar Isi

1. [Pendahuluan](#pendahuluan)
2. [Apa itu Anonymous Class?](#apa-itu-anonymous-class)
   - [Definisi dan Konsep Dasar](#definisi-dan-konsep-dasar)
   - [Anonymous Class vs Class Biasa](#anonymous-class-vs-class-biasa)
3. [Membuat Anonymous Class](#membuat-anonymous-class)
   - [Sintaks Dasar](#sintaks-dasar)
   - [Anonymous Class untuk Interface](#anonymous-class-untuk-interface)
   - [Anonymous Class untuk Abstract Class](#anonymous-class-untuk-abstract-class)
   - [Anonymous Class untuk Class Konkrit](#anonymous-class-untuk-class-konkrit)
4. [Penggunaan Anonymous Class](#penggunaan-anonymous-class)
   - [Event Handling](#event-handling)
   - [Callback Functions](#callback-functions)
   - [Strategy Pattern](#strategy-pattern)
   - [Thread dan Runnable](#thread-dan-runnable)
5. [Keterbatasan Anonymous Class](#keterbatasan-anonymous-class)
   - [Batasan Struktural](#batasan-struktural)
   - [Akses Variabel Lokal](#akses-variabel-lokal)
   - [Visibilitas dan Reusability](#visibilitas-dan-reusability)
6. [Anonymous Class vs Lambda Expressions](#anonymous-class-vs-lambda-expressions)
   - [Perbandingan Sintaks](#perbandingan-sintaks)
   - [Kapan Menggunakan Lambda vs Anonymous Class](#kapan-menggunakan-lambda-vs-anonymous-class)
7. [Latihan Praktik dengan NetBeans](#latihan-praktik-dengan-netbeans)
8. [Best Practices](#best-practices)
9. [Rangkuman](#rangkuman)
10. [Latihan Soal](#latihan-soal)
11. [Referensi](#referensi)

## Pendahuluan

Pada tutorial sebelumnya, kita telah mempelajari konsep polimorfisme, interface, dan abstract class. Ketiga konsep tersebut memberikan dasar yang kuat untuk membuat aplikasi yang fleksibel dan modular. Dalam tutorial ini, kita akan mempelajari konsep yang sedikit berbeda namun sangat berguna dalam pemrograman Java—**Anonymous Class**.

Anonymous class adalah salah satu fitur yang powerful dalam Java yang memungkinkan kita untuk mendefinisikan dan menginstansiasi class secara bersamaan, tanpa perlu memberikan nama pada class tersebut. Fitur ini sangat berguna untuk membuat implementasi cepat dari interface atau abstract class, terutama ketika implementasi tersebut hanya digunakan sekali.

## Apa itu Anonymous Class?

### Definisi dan Konsep Dasar

**Anonymous class** adalah class tanpa nama yang didefinisikan dan diinstansiasi dalam satu ekspresi. Anonymous class selalu dibuat sebagai turunan dari class lain (baik class biasa maupun abstract class) atau sebagai implementasi dari interface.

Anonymous class mendefinisikan dan menciptakan instance dari class sekaligus pada titik di mana Anda membutuhkannya. Mereka tidak memiliki deklarasi eksplisit seperti class biasa—tidak ada nama, tidak ada file terpisah—hanya implementasi "on-the-fly" yang disisipkan langsung di kode Anda.

Analogi sederhana: Anonymous class seperti pesan dalam botol—Anda menulis pesan (implementasi), memasukkannya ke botol (membuat instance), dan melemparkannya ke laut (menggunakannya di program). Pesan itu tidak memiliki nama pengirim (anonymous), tetapi tetap berisi informasi yang diperlukan.

### Anonymous Class vs Class Biasa

| Aspek | Anonymous Class | Class Biasa |
|-------|----------------|-------------|
| Nama | Tidak memiliki nama | Memiliki nama |
| Definisi | Didefinisikan dan diinstansiasi dalam satu ekspresi | Didefinisikan terpisah dari instantiasi |
| Reusability | Tidak dapat digunakan kembali (single use) | Dapat digunakan kembali di banyak tempat |
| Visibilitas | Hanya visible di scope di mana ia didefinisikan | Dapat diakses dari mana saja sesuai access modifier |
| Inheritance | Harus meng-extend class atau mengimplementasikan interface | Dapat berdiri sendiri tanpa inheritance |
| Constructor | Tidak dapat memiliki constructor eksplisit | Dapat memiliki constructor |
| Static Member | Tidak dapat memiliki static initializers atau member | Dapat memiliki static initializers dan member |

## Membuat Anonymous Class

### Sintaks Dasar

Sintaks umum untuk anonymous class adalah:

```java
new SuperType(constructorArguments) {
    // Body of anonymous class
};
```

di mana `SuperType` adalah class (abstract atau konkrit) atau interface yang diwarisi/diimplementasikan, dan `constructorArguments` adalah argumen untuk konstruktor superclass (jika diperlukan).

### Anonymous Class untuk Interface

Implementasi anonymous class untuk interface sangat umum digunakan, terutama untuk interface dengan satu atau beberapa method. Contoh:

```java
interface Greeting {
    void greet();
    void greetWithName(String name);
}

public class Main {
    public static void main(String[] args) {
        // Anonymous class implementing Greeting interface
        Greeting anonymousGreeting = new Greeting() {
            @Override
            public void greet() {
                System.out.println("Hello from anonymous class!");
            }
            
            @Override
            public void greetWithName(String name) {
                System.out.println("Hello, " + name + " from anonymous class!");
            }
        };
        
        anonymousGreeting.greet();
        anonymousGreeting.greetWithName("Alice");
    }
}
```

### Anonymous Class untuk Abstract Class

Anonymous class juga dapat digunakan untuk mengimplementasikan abstract class:

```java
abstract class Animal {
    protected String name;
    
    public Animal(String name) {
        this.name = name;
    }
    
    public abstract void makeSound();
    
    public void eat() {
        System.out.println(name + " is eating.");
    }
}

public class Main {
    public static void main(String[] args) {
        // Anonymous class extending Animal abstract class
        Animal anonymousDog = new Animal("Rex") {
            @Override
            public void makeSound() {
                System.out.println(name + " says: Woof! Woof!");
            }
            
            // We can also add additional methods or override non-abstract methods
            @Override
            public void eat() {
                System.out.println(name + " is eating dog food.");
            }
            
            // Additional method only available within the anonymous class
            private void wag() {
                System.out.println(name + " is wagging its tail.");
            }
        };
        
        anonymousDog.makeSound();
        anonymousDog.eat();
        // anonymousDog.wag(); // Error: method not defined in Animal
    }
}
```

### Anonymous Class untuk Class Konkrit

Anonymous class dapat juga meng-extend class konkrit (non-abstract):

```java
class Button {
    private String label;
    
    public Button(String label) {
        this.label = label;
    }
    
    public void click() {
        System.out.println("Button " + label + " clicked!");
    }
    
    public String getLabel() {
        return label;
    }
}

public class Main {
    public static void main(String[] args) {
        // Anonymous class extending Button class
        Button specialButton = new Button("Submit") {
            @Override
            public void click() {
                System.out.println("Special handling for " + getLabel() + " button!");
                super.click(); // Calling the parent method
            }
            
            // Additional method
            public void hover() {
                System.out.println("Mouse hovering over " + getLabel() + " button!");
            }
        };
        
        specialButton.click();
        // specialButton.hover(); // Error: method not defined in Button
    }
}
```

## Penggunaan Anonymous Class

### Event Handling

Salah satu penggunaan paling umum dari anonymous class adalah untuk event handling, terutama dalam GUI programming:

```java
import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class SimpleGUI {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Simple GUI");
        JButton button = new JButton("Click Me");
        
        // Using anonymous class for event handling
        button.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                JOptionPane.showMessageDialog(frame, "Button clicked!");
            }
        });
        
        frame.getContentPane().add(button);
        frame.setSize(300, 200);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
    }
}
```

### Callback Functions

Anonymous class sering digunakan untuk implementasi callback functions:

```java
interface Callback {
    void onComplete(String result);
    void onError(String error);
}

class DataLoader {
    public void loadData(String url, Callback callback) {
        // Simulate loading data
        try {
            // Assuming data loading is successful
            callback.onComplete("Data loaded successfully");
        } catch (Exception e) {
            callback.onError("Failed to load data: " + e.getMessage());
        }
    }
}

public class Main {
    public static void main(String[] args) {
        DataLoader loader = new DataLoader();
        
        // Using anonymous class for callback
        loader.loadData("https://example.com/data", new Callback() {
            @Override
            public void onComplete(String result) {
                System.out.println("Success: " + result);
            }
            
            @Override
            public void onError(String error) {
                System.err.println("Error: " + error);
            }
        });
    }
}
```

### Strategy Pattern

Anonymous class berguna untuk mengimplementasikan Strategy Pattern, di mana berbagai algoritma dapat dipertukarkan:

```java
interface SortingStrategy {
    void sort(int[] array);
}

class Sorter {
    private SortingStrategy strategy;
    
    public Sorter(SortingStrategy strategy) {
        this.strategy = strategy;
    }
    
    public void sort(int[] array) {
        strategy.sort(array);
    }
}

public class Main {
    public static void main(String[] args) {
        int[] numbers = {5, 2, 8, 1, 9};
        
        // Using anonymous class to implement bubble sort strategy
        Sorter bubbleSorter = new Sorter(new SortingStrategy() {
            @Override
            public void sort(int[] array) {
                System.out.println("Bubble sort implementation");
                // Bubble sort algorithm...
            }
        });
        
        // Using anonymous class to implement quick sort strategy
        Sorter quickSorter = new Sorter(new SortingStrategy() {
            @Override
            public void sort(int[] array) {
                System.out.println("Quick sort implementation");
                // Quick sort algorithm...
            }
        });
        
        bubbleSorter.sort(numbers);
        quickSorter.sort(numbers);
    }
}
```

### Thread dan Runnable

Anonymous class sering digunakan untuk implementasi thread sederhana:

```java
public class Main {
    public static void main(String[] args) {
        // Using anonymous class to implement Runnable
        Thread thread = new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 5; i++) {
                    System.out.println("Thread running: " + i);
                    try {
                        Thread.sleep(1000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            }
        });
        
        thread.start();
        System.out.println("Main thread continues...");
    }
}
```

## Keterbatasan Anonymous Class

### Batasan Struktural

1. **Tidak Dapat Memiliki Konstruktor Eksplisit**:
   
   Anonymous class tidak dapat memiliki konstruktor eksplisit karena tidak memiliki nama. Inisialisasi dilakukan melalui instance initializer blocks:

   ```java
   Runnable r = new Runnable() {
       private int count;
       
       // Instance initializer block instead of constructor
       {
           count = 10;
           System.out.println("Anonymous class initialized");
       }
       
       @Override
       public void run() {
           System.out.println("Count: " + count);
       }
   };
   ```

2. **Tidak Dapat Memiliki Static Members**:

   Anonymous class tidak dapat memiliki static initializers atau static members:

   ```java
   Runnable r = new Runnable() {
       // This would cause a compile error
       // static int staticVar = 10;
       
       // This would also cause a compile error
       // static {
       //     System.out.println("Static initializer");
       // }
       
       @Override
       public void run() {
           System.out.println("Running");
       }
   };
   ```

3. **Batasan Extends dan Implements**:

   Anonymous class dapat meng-extend satu class ATAU mengimplementasikan satu interface, tetapi tidak keduanya secara bersamaan:

   ```java
   // Valid: extending a class
   Object obj = new Object() {
       @Override
       public String toString() {
           return "Anonymous Object";
       }
   };
   
   // Valid: implementing an interface
   Runnable r = new Runnable() {
       @Override
       public void run() {
           System.out.println("Running");
       }
   };
   
   // Not possible: extending a class and implementing an interface simultaneously
   ```

### Akses Variabel Lokal

Anonymous class dapat mengakses variabel lokal dari metode di mana mereka didefinisikan, tetapi variabel tersebut harus bersifat `final` atau "effectively final" (tidak diubah nilainya setelah inisialisasi):

```java
public void someMethod() {
    final int finalVar = 10;
    int effectivelyFinalVar = 20;  // Not declared final but never modified
    int nonFinalVar = 30;
    
    Runnable r = new Runnable() {
        @Override
        public void run() {
            System.out.println("Final var: " + finalVar);
            System.out.println("Effectively final var: " + effectivelyFinalVar);
            // System.out.println(nonFinalVar++);  // Error: Cannot modify variable
        }
    };
    
    // nonFinalVar = 40;  // If uncommented, would make effectivelyFinalVar not effectively final
    
    r.run();
}
```

### Visibilitas dan Reusability

Anonymous class tidak dapat digunakan kembali di tempat lain karena mereka tidak memiliki nama. Jika implementasi yang sama dibutuhkan di beberapa tempat, lebih baik membuat named class:

```java
// If you need this implementation in multiple places, use a named class
class SpecialRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Special running logic");
    }
}

// Usage in multiple places
Runnable r1 = new SpecialRunnable();
Runnable r2 = new SpecialRunnable();
```

## Anonymous Class vs Lambda Expressions

Sejak Java 8, lambda expressions menyediakan cara yang lebih ringkas untuk mengimplementasikan functional interfaces (interface dengan satu abstract method).

### Perbandingan Sintaks

Untuk implementasi `Runnable` (yang hanya memiliki satu method `run()`):

```java
// Using anonymous class
Runnable anonymousRunnable = new Runnable() {
    @Override
    public void run() {
        System.out.println("Anonymous class implementation");
    }
};

// Using lambda expression (Java 8+)
Runnable lambdaRunnable = () -> System.out.println("Lambda implementation");
```

Untuk implementasi `Comparator` (yang memiliki satu method `compare()`):

```java
// Using anonymous class
Comparator<String> anonymousComparator = new Comparator<String>() {
    @Override
    public int compare(String s1, String s2) {
        return s1.length() - s2.length();
    }
};

// Using lambda expression
Comparator<String> lambdaComparator = (s1, s2) -> s1.length() - s2.length();
```

### Kapan Menggunakan Lambda vs Anonymous Class

**Gunakan Lambda Expressions ketika**:
- Anda mengimplementasikan functional interface (interface dengan satu abstract method)
- Implementasinya sederhana dan ringkas
- Tidak perlu mengakses `this` atau `super` dari class enclosing
- Tidak perlu menambahkan fields atau methods tambahan

**Gunakan Anonymous Class ketika**:
- Anda perlu mengimplementasikan interface dengan banyak methods
- Anda perlu mengimplementasikan atau meng-extend abstract class
- Anda perlu menambahkan fields atau methods tambahan
- Anda perlu mengakses `this` atau `super` dari class enclosing

## Latihan Praktik dengan NetBeans

Mari kita praktikkan konsep anonymous class dengan membuat aplikasi sederhana di NetBeans.

### Langkah 1: Buat Project Baru

1. Buka NetBeans
2. Pilih `File > New Project`
3. Pilih `Java with Ant > Java Application`
4. Beri nama project `AnonymousClassDemo` dan klik `Finish`

### Langkah 2: Buat Interface Validator

1. Klik kanan pada package project > `New > Java Interface`
2. Beri nama `Validator` dan klik `Finish`
3. Isi dengan kode berikut:

```java
package anonymousclassdemo;

public interface Validator {
    boolean validate(String input);
    String getErrorMessage();
}
```

### Langkah 3: Buat Abstract Class Filter

1. Klik kanan pada package project > `New > Java Class`
2. Beri nama `Filter` dan klik `Finish`
3. Ubah kode menjadi:

```java
package anonymousclassdemo;

public abstract class Filter {
    protected String name;
    
    public Filter(String name) {
        this.name = name;
    }
    
    public abstract String filter(String input);
    
    public String getName() {
        return name;
    }
}
```

### Langkah 4: Buat Class Button

1. Klik kanan pada package project > `New > Java Class`
2. Beri nama `Button` dan klik `Finish`
3. Isi dengan kode berikut:

```java
package anonymousclassdemo;

public class Button {
    private String label;
    private ClickListener clickListener;
    
    public Button(String label) {
        this.label = label;
    }
    
    public void setClickListener(ClickListener listener) {
        this.clickListener = listener;
    }
    
    public void click() {
        if (clickListener != null) {
            clickListener.onClick(this);
        }
    }
    
    public String getLabel() {
        return label;
    }
    
    // Nested interface
    public interface ClickListener {
        void onClick(Button button);
    }
}
```

### Langkah 5: Buat Class Task

1. Klik kanan pada package project > `New > Java Class`
2. Beri nama `Task` dan klik `Finish`
3. Isi dengan kode berikut:

```java
package anonymousclassdemo;

public class Task {
    private String name;
    private Callback callback;
    
    public Task(String name) {
        this.name = name;
    }
    
    public void setCallback(Callback callback) {
        this.callback = callback;
    }
    
    public void execute() {
        System.out.println("Executing task: " + name);
        
        // Simulate task execution
        try {
            Thread.sleep(1000); // Simulate work
            
            if (Math.random() < 0.8) {
                // 80% chance of success
                if (callback != null) {
                    callback.onSuccess("Task " + name + " completed successfully!");
                }
            } else {
                // 20% chance of failure
                if (callback != null) {
                    callback.onFailure("Task " + name + " failed!");
                }
            }
        } catch (InterruptedException e) {
            if (callback != null) {
                callback.onFailure("Task interrupted: " + e.getMessage());
            }
        }
    }
    
    public interface Callback {
        void onSuccess(String result);
        void onFailure(String error);
    }
}
```

### Langkah 6: Buat Class Sorter dengan Generic Type

1. Klik kanan pada package project > `New > Java Class`
2. Beri nama `Sorter` dan klik `Finish`
3. Isi dengan kode berikut:

```java
package anonymousclassdemo;

import java.util.Arrays;
import java.util.Comparator;

public class Sorter<T> {
    private T[] items;
    
    public Sorter(T[] items) {
        this.items = items.clone();
    }
    
    public T[] sort(Comparator<T> comparator) {
        T[] result = items.clone();
        Arrays.sort(result, comparator);
        return result;
    }
}
```

### Langkah 7: Buat Kelas Main untuk Demonstrasi

1. Buka file main (biasanya `AnonymousClassDemo.java`)
2. Ubah kode menjadi:

```java
package anonymousclassdemo;

import java.util.Arrays;
import java.util.Comparator;

public class AnonymousClassDemo {
    public static void main(String[] args) {
        System.out.println("===== ANONYMOUS CLASS DEMO =====\n");
        
        // Anonymous class implementing Validator interface
        System.out.println("--- Validator Demo ---");
        Validator emailValidator = new Validator() {
            private boolean isValid;
            private String email;
            
            @Override
            public boolean validate(String input) {
                email = input;
                isValid = input != null && 
                         input.contains("@") && 
                         input.contains(".");
                return isValid;
            }
            
            @Override
            public String getErrorMessage() {
                if (isValid) {
                    return "Email is valid";
                } else {
                    return "Invalid email: " + email + 
                           " (must contain '@' and '.')";
                }
            }
        };
        
        String[] emails = {"user@example.com", "invalid-email", "another@user.co"};
        for (String email : emails) {
            boolean valid = emailValidator.validate(email);
            System.out.println(email + ": " + (valid ? "Valid" : "Invalid"));
            System.out.println("  " + emailValidator.getErrorMessage());
        }
        
        // Anonymous class extending Filter abstract class
        System.out.println("\n--- Filter Demo ---");
        Filter uppercaseFilter = new Filter("Uppercase Filter") {
            @Override
            public String filter(String input) {
                return input != null ? input.toUpperCase() : "";
            }
        };
        
        Filter vowelRemover = new Filter("Vowel Remover") {
            @Override
            public String filter(String input) {
                return input != null ? input.replaceAll("[aeiouAEIOU]", "") : "";
            }
            
            // Additional method (only available within this anonymous class)
            private boolean isVowel(char c) {
                return "aeiouAEIOU".indexOf(c) != -1;
            }
        };
        
        String testString = "Hello World";
        System.out.println("Original: " + testString);
        System.out.println(uppercaseFilter.getName() + ": " + 
                          uppercaseFilter.filter(testString));
        System.out.println(vowelRemover.getName() + ": " + 
                          vowelRemover.filter(testString));
        
        // Anonymous class implementing Button.ClickListener interface
        System.out.println("\n--- Button Click Demo ---");
        Button loginButton = new Button("Login");
        Button cancelButton = new Button("Cancel");
        
        loginButton.setClickListener(new Button.ClickListener() {
            @Override
            public void onClick(Button button) {
                System.out.println("Login button clicked! Performing login...");
            }
        });
        
        cancelButton.setClickListener(new Button.ClickListener() {
            @Override
            public void onClick(Button button) {
                System.out.println("Cancel button clicked! Cancelling operation...");
            }
        });
        
        loginButton.click();
        cancelButton.click();
        
        // Anonymous class for callback implementation
        System.out.println("\n--- Task Callback Demo ---");
        Task uploadTask = new Task("File Upload");
        
        uploadTask.setCallback(new Task.Callback() {
            @Override
            public void onSuccess(String result) {
                System.out.println("Success: " + result);
                System.out.println("Proceeding to next step...");
            }
            
            @Override
            public void onFailure(String error) {
                System.out.println("Error: " + error);
                System.out.println("Retrying...");
            }
        });
        
        uploadTask.execute();
        
        // Anonymous class implementing Comparator for custom sorting
        System.out.println("\n--- Comparator Demo ---");
        String[] names = {"Alice", "Bob", "Charlie", "David", "Eva"};
        
        Sorter<String> nameSorter = new Sorter<>(names);
        
        // Sort by length using anonymous class
        String[] sortedByLength = nameSorter.sort(new Comparator<String>() {
            @Override
            public int compare(String s1, String s2) {
                return s1.length() - s2.length();
            }
        });
        
        // Sort alphabetically in reverse using anonymous class
        String[] sortedByAlphabet = nameSorter.sort(new Comparator<String>() {
            @Override
            public int compare(String s1, String s2) {
                return s2.compareTo(s1); // Reverse order
            }
        });
        
        System.out.println("Original names: " + Arrays.toString(names));
        System.out.println("Sorted by length: " + Arrays.toString(sortedByLength));
        System.out.println("Sorted alphabetically (reverse): " + Arrays.toString(sortedByAlphabet));
        
        // Thread creation using anonymous class
        System.out.println("\n--- Thread Demo ---");
        Thread counterThread = new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 1; i <= 5; i++) {
                    System.out.println("Count: " + i);
                    try {
                        Thread.sleep(500);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            }
        });
        
        counterThread.start();
        
        // Compare with lambda expression (Java 8+)
        System.out.println("\n--- Lambda vs Anonymous Class ---");
        
        // Anonymous class implementation
        Runnable anonymousRunnable = new Runnable() {
            @Override
            public void run() {
                System.out.println("This is from anonymous class");
            }
        };
        
        // Lambda implementation
        Runnable lambdaRunnable = () -> System.out.println("This is from lambda expression");
        
        anonymousRunnable.run();
        lambdaRunnable.run();
        
        try {
            // Wait for counter thread to finish
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

### Langkah 8: Jalankan Program

1. Klik tombol Run (F6) untuk menjalankan program
2. Amati output yang dihasilkan

## Best Practices

1. **Gunakan Anonymous Class untuk Implementasi Sederhana**:
   - Jika implementasi sangat sederhana dan hanya digunakan di satu tempat, anonymous class dapat membuat kode lebih ringkas.

2. **Pertimbangkan Lambda Expressions untuk Functional Interfaces**:
   - Untuk interface dengan satu method, lambda expressions (Java 8+) lebih ringkas dan ekspresif.

3. **Pertimbangkan Class Bernama untuk Kompleksitas Tinggi**:
   - Jika implementasi kompleks atau digunakan di beberapa tempat, membuat named class lebih baik.

4. **Hindari Anonymous Class yang Terlalu Besar**:
   - Anonymous class dengan banyak method atau logika kompleks membuat kode sulit dibaca.

5. **Jaga Konteks Penggunaan**:
   - Gunakan anonymous class dekat dengan tempat penggunaannya untuk meningkatkan readability.

6. **Minimalkan Akses ke Variabel Luar**:
   - Meminimalkan penggunaan variabel dari enclosing scope membuat anonymous class lebih mudah dipahami.

## Rangkuman

Dalam tutorial ini, kita telah mempelajari:

✅ **Anonymous Class** - Class tanpa nama yang didefinisikan dan diinstansiasi dalam satu ekspresi

✅ **Cara Membuat Anonymous Class** - Untuk interface, abstract class, dan class konkrit

✅ **Penggunaan Umum Anonymous Class** - Event handling, callbacks, strategy pattern, dan thread

✅ **Keterbatasan Anonymous Class** - Tidak bisa memiliki konstruktor eksplisit, static members, dan lainnya

✅ **Anonymous Class vs Lambda Expressions** - Pilihan penggunaan tergantung kebutuhan spesifik

✅ **Best Practices** - Pedoman penggunaan anonymous class secara efektif

Anonymous class adalah alat yang powerful dalam pemrograman Java yang memungkinkan implementasi cepat dan efisien dari interface dan abstract class, terutama ketika implementasi tersebut hanya digunakan sekali. Meskipun lambda expressions (Java 8+) memberikan alternatif yang lebih ringkas untuk functional interfaces, anonymous class tetap memiliki peran penting dalam berbagai skenario pemrograman Java.

## Latihan Soal

1. Apa yang dimaksud dengan anonymous class dalam Java? Jelaskan karakteristik utamanya.

2. Apa perbedaan antara anonymous class dan class biasa? Berikan contoh kasus penggunaan yang tepat untuk masing-masing.

3. Bagaimana cara membuat anonymous class yang mengimplementasikan interface? Berikan contoh kode.

4. Apakah anonymous class dapat memiliki konstruktor? Jika tidak, bagaimana cara menginisialisasi fields dalam anonymous class?

5. Sebutkan minimal 3 keterbatasan anonymous class dan jelaskan alasannya.

6. Jelaskan perbedaan antara anonymous class dan lambda expressions. Kapan sebaiknya menggunakan anonymous class daripada lambda?

7. Buatlah contoh anonymous class yang mengimplementasikan interface `Comparator<Student>` untuk mengurutkan objek `Student` berdasarkan nilai (`grade`).

8. Apa yang dimaksud dengan "effectively final" dalam konteks variabel lokal yang diakses oleh anonymous class?

9. Buatlah contoh anonymous class yang mengextend class `Thread` dan override method `run()` untuk menampilkan angka 1 sampai 10 dengan jeda 1 detik.

10. Implementasikan sebuah simple event system dengan menggunakan anonymous class. Buatlah interface `EventListener` dengan method `onEvent(String eventName, Object data)`, dan class `EventManager` yang dapat menambahkan listener dan memicu event.

## Referensi

1. Bloch, J. (2018). *Effective Java* (3rd ed.). Addison-Wesley Professional. Chapter 7: Lambda and Streams, Item 42: Prefer lambdas to anonymous classes.

2. Deitel, P., & Deitel, H. (2020). *Java How to Program, Early Objects* (11th ed.). Pearson. Chapter 9: Classes and Objects: A Deeper Look.

3. Eckel, B. (2006). *Thinking in Java* (4th ed.). Prentice Hall. Chapter 10: Inner Classes.

4. Horstmann, C. S. (2019). *Core Java Volume I—Fundamentals* (11th ed.). Prentice Hall. Chapter 6: Interfaces, Lambda Expressions, and Inner Classes.

5. Oracle. (2023). *Java Language Specification: Anonymous Classes*. [https://docs.oracle.com/javase/specs/jls/se17/html/jls-15.html#jls-15.9.5](https://docs.oracle.com/javase/specs/jls/se17/html/jls-15.html#jls-15.9.5)

6. Oracle. (2023). *Java Tutorial: Anonymous Classes*. [https://docs.oracle.com/javase/tutorial/java/javaOO/anonymousclasses.html](https://docs.oracle.com/javase/tutorial/java/javaOO/anonymousclasses.html)

7. Schildt, H. (2018). *Java: The Complete Reference* (11th ed.). McGraw-Hill Education. Chapter 24: Using Inner Classes.

8. Sierra, K., & Bates, B. (2005). *Head First Java* (2nd ed.). O'Reilly Media. Chapter 11: Inner Classes.

9. Urma, R.-G., Fusco, M., & Mycroft, A. (2014). *Java 8 in Action: Lambdas, Streams, and Functional-Style Programming*. Manning Publications. Chapter 3: Lambda Expressions.

10. Naftalin, M., & Wadler, P. (2006). *Java Generics and Collections*. O'Reilly Media. Chapter 4: Comparison and Bounds.

---

[◀️ Kembali ke Tutorial #09: Mengenal Class Abstract](09-abstract-classes.md) | [Lanjut ke Tutorial #11: Menggunakan Lambda Expression ▶️](11-lambda-expressions.md)

---

© 2023 Tutorial Dasar OOP di Java untuk Pemula. Semua hak cipta dilindungi.
