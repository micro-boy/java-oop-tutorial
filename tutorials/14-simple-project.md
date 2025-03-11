
# 📘 Tutorial Java OOP #14: Implementasi Proyek Sederhana

> *"Pemahaman sejati datang dari penerapan. Sekarang saatnya menggabungkan semua konsep OOP yang telah kita pelajari untuk membangun sebuah aplikasi yang utuh, fungsional, dan terstruktur dengan baik."*

## 🎯 Tujuan Pembelajaran

Setelah mempelajari materi ini, Anda diharapkan dapat:
- Merancang dan mengimplementasikan aplikasi Java yang mengintegrasikan berbagai konsep OOP
- Menerapkan prinsip desain software yang baik dalam pengembangan aplikasi
- Mengelola dependensi antar komponen dalam aplikasi berorientasi objek
- Mengimplementasikan fitur aplikasi menggunakan inheritance, polymorphism, dan encapsulation
- Mengelola data menggunakan collections framework
- Menangani error dan kasus pengecualian dengan tepat
- Membangun user interface berbasis konsol yang user-friendly
- Menguji dan memvalidasi aplikasi secara menyeluruh
- Mendokumentasikan kode dengan baik
- Mengembangkan kemampuan problem solving dalam konteks OOP

## 📋 Daftar Isi

1. [Pendahuluan](#pendahuluan)
2. [Gambaran Umum Proyek](#gambaran-umum-proyek)
   - [Deskripsi Sistem Manajemen Inventory](#deskripsi-sistem-manajemen-inventory)
   - [Fitur Utama](#fitur-utama)
   - [Struktur Proyek](#struktur-proyek)
3. [Perancangan Sistem](#perancangan-sistem)
   - [Identifikasi Class dan Interface](#identifikasi-class-dan-interface)
   - [Diagram Hubungan Class](#diagram-hubungan-class)
   - [Desain Database Sederhana](#desain-database-sederhana)
4. [Implementasi dengan NetBeans](#implementasi-dengan-netbeans)
   - [Membuat Project Baru](#membuat-project-baru)
   - [Mengimplementasikan Model](#mengimplementasikan-model)
   - [Mengimplementasikan Service Layer](#mengimplementasikan-service-layer)
   - [Mengimplementasikan Data Access Layer](#mengimplementasikan-data-access-layer)
   - [Mengimplementasikan User Interface](#mengimplementasikan-user-interface)
   - [Menghubungkan Komponen](#menghubungkan-komponen)
5. [Penerapan Konsep OOP](#penerapan-konsep-oop)
   - [Inheritance dan Polymorphism](#inheritance-dan-polymorphism)
   - [Interface dan Abstract Class](#interface-dan-abstract-class)
   - [Encapsulation dan Information Hiding](#encapsulation-dan-information-hiding)
   - [Collections Framework](#collections-framework)
   - [Exception Handling](#exception-handling)
   - [Lambda Expressions](#lambda-expressions)
6. [Pembahasan Pola Desain](#pembahasan-pola-desain)
   - [DAO Pattern](#dao-pattern)
   - [Service Pattern](#service-pattern)
   - [Singleton Pattern](#singleton-pattern)
   - [Factory Pattern](#factory-pattern)
7. [Testing dan Debugging](#testing-dan-debugging)
   - [Manual Testing](#manual-testing)
   - [Debugging Common Issues](#debugging-common-issues)
8. [Peningkatan dan Pengembangan Lebih Lanjut](#peningkatan-dan-pengembangan-lebih-lanjut)
   - [Ide Peningkatan](#ide-peningkatan)
   - [Refactoring Opportunities](#refactoring-opportunities)
9. [Rangkuman](#rangkuman)
10. [Latihan Soal](#latihan-soal)
11. [Referensi](#referensi)

## Pendahuluan

Selamat datang di Tutorial #14 dari seri Pemrograman Berorientasi Objek dengan Java! Setelah mempelajari berbagai konsep dan komponen OOP dalam tutorial-tutorial sebelumnya, kini saatnya untuk menggabungkan semua pengetahuan tersebut ke dalam sebuah proyek yang utuh dan fungsional.

Proyek ini akan memungkinkan Anda melihat bagaimana berbagai konsep OOP—seperti class, inheritance, interface, polymorphism, exception handling, dan collections—bekerja sama dalam konteks aplikasi dunia nyata. Melalui proses pengembangan proyek ini, Anda akan mendapat pemahaman yang lebih dalam tentang bagaimana mendesain, mengimplementasikan, dan menguji aplikasi berorientasi objek.

Kita akan membangun sebuah Sistem Manajemen Inventory sederhana, yang menggabungkan berbagai aspek pemrograman berorientasi objek. Proyek ini akan mencakup pengelolaan produk, kategori, supplier, dan transaksi dengan operasi CRUD (Create, Read, Update, Delete) dasar.

Mari kita mulai perjalanan pengembangan aplikasi ini!

## Gambaran Umum Proyek

### Deskripsi Sistem Manajemen Inventory

Sistem Manajemen Inventory adalah aplikasi yang memungkinkan pengguna untuk melacak dan mengelola stok barang dalam suatu bisnis. Dalam proyek ini, kita akan membuat versi sederhana dari sistem tersebut yang berjalan di konsol (command-line interface).

Sistem ini dirancang untuk toko retail kecil yang perlu mengelola inventory produk mereka, mencatat supplier, dan memantau transaksi dasar seperti penambahan dan pengambilan stok.

### Fitur Utama

Aplikasi Sistem Manajemen Inventory kita akan memiliki fitur-fitur berikut:

1. **Manajemen Produk**:
   - Tambah, lihat, perbarui, dan hapus produk
   - Cari produk berdasarkan nama, kategori, atau kode
   - Lacak stok produk

2. **Manajemen Kategori**:
   - Tambah, lihat, perbarui, dan hapus kategori produk
   - Lihat semua produk dalam kategori tertentu

3. **Manajemen Supplier**:
   - Tambah, lihat, perbarui, dan hapus informasi supplier
   - Lihat semua produk dari supplier tertentu

4. **Manajemen Transaksi**:
   - Catat transaksi masuk (menambah stok)
   - Catat transaksi keluar (mengurangi stok)
   - Lihat riwayat transaksi

5. **Reporting**:
   - Lihat produk dengan stok rendah
   - Lihat statistik inventory

6. **Fitur User**:
   - Autentikasi pengguna sederhana
   - Level akses berbeda (admin dan staff regular)

### Struktur Proyek

Proyek ini akan mengikuti struktur multi-layer yang umum digunakan dalam aplikasi enterprise:

1. **Presentation Layer** (User Interface):
   - Menangani interaksi dengan pengguna melalui konsol
   - Menampilkan menu dan output
   - Memvalidasi input pengguna

2. **Business Layer** (Service Layer):
   - Mengimplementasikan logika bisnis
   - Menerapkan aturan validasi
   - Mengoordinasikan operasi

3. **Data Access Layer**:
   - Menangani penyimpanan dan pengambilan data
   - Dalam proyek sederhana ini, kita akan menggunakan penyimpanan in-memory dengan collections

4. **Domain Layer** (Model):
   - Mendefinisikan entity/model yang mewakili objek bisnis
   - Mengimplementasikan behavior spesifik domain

Kita akan menggunakan pendekatan yang terstruktur namun sederhana, dengan fokus pada prinsip OOP dan aplikabilitas praktis.

## Perancangan Sistem

### Identifikasi Class dan Interface

Berdasarkan deskripsi sistem, kita dapat mengidentifikasi beberapa class dan interface utama:

**Model/Entity Classes**:
- `User`: Mewakili pengguna sistem
- `Product`: Mewakili produk dalam inventory
- `Category`: Mewakili kategori produk
- `Supplier`: Mewakili pemasok produk
- `Transaction`: Mewakili transaksi inventory (abstrak)
  - `InboundTransaction`: Transaksi penambahan stok
  - `OutboundTransaction`: Transaksi pengurangan stok

**Service Interfaces**:
- `UserService`: Mengelola operasi terkait pengguna
- `ProductService`: Mengelola operasi terkait produk
- `CategoryService`: Mengelola operasi terkait kategori
- `SupplierService`: Mengelola operasi terkait supplier
- `TransactionService`: Mengelola operasi terkait transaksi
- `ReportService`: Menyediakan laporan dan statistik

**DAO (Data Access Object) Interfaces**:
- `UserDAO`: Akses data untuk User
- `ProductDAO`: Akses data untuk Product
- `CategoryDAO`: Akses data untuk Category
- `SupplierDAO`: Akses data untuk Supplier
- `TransactionDAO`: Akses data untuk Transaction

**UI Classes**:
- `InventoryApp`: Class utama yang berisi method main
- `UIManager`: Mengelola user interface dan navigasi
- `InputHandler`: Menangani dan memvalidasi input pengguna
- Menu handler untuk berbagai komponen (produk, kategori, dll.)

**Utility Classes**:
- `PasswordUtils`: Untuk mengelola password (enkripsi sederhana)
- `DateUtils`: Untuk operasi terkait tanggal dan waktu

### Diagram Hubungan Class

Berikut adalah representasi sederhana dari hubungan antar class dalam sistem kita:

```
[User] --> [Role]
    
[Product] --> [Category]
[Product] <--> [Supplier]
    
[Transaction] <|-- [InboundTransaction]
[Transaction] <|-- [OutboundTransaction]
[Transaction] --> [Product]
[Transaction] --> [User]
    
[*Service] --> [*DAO]
[*Service] --> [Model Classes]
    
[UI Classes] --> [*Service]
```

### Desain Database Sederhana

Untuk proyek ini, kita akan menggunakan penyimpanan in-memory dengan Java Collections, tetapi dengan struktur yang menyerupai database relasional. Berikut adalah struktur "tabel" yang akan kita implementasikan:

```
Users(userId, username, password, fullName, role)
Categories(categoryId, name, description)
Suppliers(supplierId, name, contactPerson, phone, email, address)
Products(productId, name, description, categoryId, price, stockQuantity, supplierId)
Transactions(transactionId, type, productId, quantity, date, userId, notes)
```

## Implementasi dengan NetBeans

### Membuat Project Baru

Mari kita mulai dengan membuat project baru di NetBeans:

1. Buka NetBeans IDE
2. Pilih **File > New Project**
3. Pilih **Java with Ant > Java Application**
4. Beri nama project `InventoryManagementSystem` dan klik **Finish**

### Mengimplementasikan Model

Mari mulai dengan mengimplementasikan class-class model dasar.

#### 1. Buat Enum Role

```java
package inventorymanagementsystem.model;

public enum Role {
    ADMIN,
    STAFF
}
```

#### 2. Buat Class User

```java
package inventorymanagementsystem.model;

import java.util.Objects;

public class User {
    private String userId;
    private String username;
    private String password;
    private String fullName;
    private Role role;
    
    public User(String userId, String username, String password, String fullName, Role role) {
        this.userId = userId;
        this.username = username;
        this.password = password;
        this.fullName = fullName;
        this.role = role;
    }
    
    // Getters and Setters
    public String getUserId() {
        return userId;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public String getFullName() {
        return fullName;
    }

    public void setFullName(String fullName) {
        this.fullName = fullName;
    }

    public Role getRole() {
        return role;
    }

    public void setRole(Role role) {
        this.role = role;
    }
    
    // Object methods
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        User user = (User) o;
        return Objects.equals(userId, user.userId);
    }

    @Override
    public int hashCode() {
        return Objects.hash(userId);
    }

    @Override
    public String toString() {
        return "User{" +
                "userId='" + userId + '\'' +
                ", username='" + username + '\'' +
                ", fullName='" + fullName + '\'' +
                ", role=" + role +
                '}';
    }
}
```

#### 3. Buat Class Category

```java
package inventorymanagementsystem.model;

import java.util.Objects;

public class Category {
    private String categoryId;
    private String name;
    private String description;
    
    public Category(String categoryId, String name, String description) {
        this.categoryId = categoryId;
        this.name = name;
        this.description = description;
    }
    
    // Getters and Setters
    public String getCategoryId() {
        return categoryId;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getDescription() {
        return description;
    }

    public void setDescription(String description) {
        this.description = description;
    }
    
    // Object methods
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Category category = (Category) o;
        return Objects.equals(categoryId, category.categoryId);
    }

    @Override
    public int hashCode() {
        return Objects.hash(categoryId);
    }

    @Override
    public String toString() {
        return "Category{" +
                "categoryId='" + categoryId + '\'' +
                ", name='" + name + '\'' +
                ", description='" + description + '\'' +
                '}';
    }
}
```

#### 4. Buat Class Supplier

```java
package inventorymanagementsystem.model;

import java.util.Objects;

public class Supplier {
    private String supplierId;
    private String name;
    private String contactPerson;
    private String phone;
    private String email;
    private String address;
    
    public Supplier(String supplierId, String name, String contactPerson, String phone, String email, String address) {
        this.supplierId = supplierId;
        this.name = name;
        this.contactPerson = contactPerson;
        this.phone = phone;
        this.email = email;
        this.address = address;
    }
    
    // Getters and Setters
    public String getSupplierId() {
        return supplierId;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getContactPerson() {
        return contactPerson;
    }

    public void setContactPerson(String contactPerson) {
        this.contactPerson = contactPerson;
    }

    public String getPhone() {
        return phone;
    }

    public void setPhone(String phone) {
        this.phone = phone;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }
    
    // Object methods
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Supplier supplier = (Supplier) o;
        return Objects.equals(supplierId, supplier.supplierId);
    }

    @Override
    public int hashCode() {
        return Objects.hash(supplierId);
    }

    @Override
    public String toString() {
        return "Supplier{" +
                "supplierId='" + supplierId + '\'' +
                ", name='" + name + '\'' +
                ", contactPerson='" + contactPerson + '\'' +
                ", phone='" + phone + '\'' +
                '}';
    }
}
```

#### 5. Buat Class Product

```java
package inventorymanagementsystem.model;

import java.util.Objects;

public class Product {
    private String productId;
    private String name;
    private String description;
    private String categoryId;
    private double price;
    private int stockQuantity;
    private String supplierId;
    
    public Product(String productId, String name, String description, String categoryId, 
                   double price, int stockQuantity, String supplierId) {
        this.productId = productId;
        this.name = name;
        this.description = description;
        this.categoryId = categoryId;
        this.price = price;
        this.stockQuantity = stockQuantity;
        this.supplierId = supplierId;
    }
    
    // Getters and Setters
    public String getProductId() {
        return productId;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getDescription() {
        return description;
    }

    public void setDescription(String description) {
        this.description = description;
    }

    public String getCategoryId() {
        return categoryId;
    }

    public void setCategoryId(String categoryId) {
        this.categoryId = categoryId;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    public int getStockQuantity() {
        return stockQuantity;
    }

    public void setStockQuantity(int stockQuantity) {
        this.stockQuantity = stockQuantity;
    }

    public String getSupplierId() {
        return supplierId;
    }

    public void setSupplierId(String supplierId) {
        this.supplierId = supplierId;
    }
    
    // Business methods
    public void increaseStock(int quantity) {
        if (quantity <= 0) {
            throw new IllegalArgumentException("Quantity must be positive");
        }
        this.stockQuantity += quantity;
    }
    
    public void decreaseStock(int quantity) {
        if (quantity <= 0) {
            throw new IllegalArgumentException("Quantity must be positive");
        }
        if (quantity > this.stockQuantity) {
            throw new IllegalStateException("Not enough stock available");
        }
        this.stockQuantity -= quantity;
    }
    
    public boolean isLowStock(int threshold) {
        return this.stockQuantity <= threshold;
    }
    
    // Object methods
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Product product = (Product) o;
        return Objects.equals(productId, product.productId);
    }

    @Override
    public int hashCode() {
        return Objects.hash(productId);
    }

    @Override
    public String toString() {
        return "Product{" +
                "productId='" + productId + '\'' +
                ", name='" + name + '\'' +
                ", price=" + price +
                ", stockQuantity=" + stockQuantity +
                '}';
    }
}
```

#### 6. Buat Class Transaction hierarki

```java
package inventorymanagementsystem.model;

import java.time.LocalDateTime;
import java.util.Objects;

public abstract class Transaction {
    private String transactionId;
    private String productId;
    private int quantity;
    private LocalDateTime timestamp;
    private String userId;
    private String notes;
    
    public Transaction(String transactionId, String productId, int quantity, 
                      LocalDateTime timestamp, String userId, String notes) {
        this.transactionId = transactionId;
        this.productId = productId;
        this.quantity = quantity;
        this.timestamp = timestamp;
        this.userId = userId;
        this.notes = notes;
    }
    
    // Getters and Setters
    public String getTransactionId() {
        return transactionId;
    }

    public String getProductId() {
        return productId;
    }

    public int getQuantity() {
        return quantity;
    }

    public LocalDateTime getTimestamp() {
        return timestamp;
    }

    public String getUserId() {
        return userId;
    }

    public String getNotes() {
        return notes;
    }

    public void setNotes(String notes) {
        this.notes = notes;
    }
    
    // Abstract method to be implemented by subclasses
    public abstract String getTransactionType();
    
    // Common object methods
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Transaction that = (Transaction) o;
        return Objects.equals(transactionId, that.transactionId);
    }

    @Override
    public int hashCode() {
        return Objects.hash(transactionId);
    }

    @Override
    public String toString() {
        return "Transaction{" +
                "transactionId='" + transactionId + '\'' +
                ", productId='" + productId + '\'' +
                ", quantity=" + quantity +
                ", timestamp=" + timestamp +
                ", type='" + getTransactionType() + '\'' +
                '}';
    }
}
```

```java
package inventorymanagementsystem.model;

import java.time.LocalDateTime;

public class InboundTransaction extends Transaction {
    
    public InboundTransaction(String transactionId, String productId, int quantity,
                             LocalDateTime timestamp, String userId, String notes) {
        super(transactionId, productId, quantity, timestamp, userId, notes);
    }
    
    @Override
    public String getTransactionType() {
        return "INBOUND";
    }
}
```

```java
package inventorymanagementsystem.model;

import java.time.LocalDateTime;

public class OutboundTransaction extends Transaction {
    
    public OutboundTransaction(String transactionId, String productId, int quantity,
                              LocalDateTime timestamp, String userId, String notes) {
        super(transactionId, productId, quantity, timestamp, userId, notes);
    }
    
    @Override
    public String getTransactionType() {
        return "OUTBOUND";
    }
}
```

### Mengimplementasikan Data Access Layer

Sekarang, mari implementasikan Data Access Layer dengan interface DAO dan implementasi in-memory.

#### 1. Interface UserDAO

```java
package inventorymanagementsystem.dao;

import inventorymanagementsystem.model.User;
import java.util.List;
import java.util.Optional;

public interface UserDAO {
    boolean add(User user);
    Optional<User> findById(String userId);
    Optional<User> findByUsername(String username);
    List<User> findAll();
    boolean update(User user);
    boolean delete(String userId);
}
```

#### 2. Interface ProductDAO

```java
package inventorymanagementsystem.dao;

import inventorymanagementsystem.model.Product;
import java.util.List;
import java.util.Optional;

public interface ProductDAO {
    boolean add(Product product);
    Optional<Product> findById(String productId);
    List<Product> findByName(String name);
    List<Product> findByCategory(String categoryId);
    List<Product> findBySupplier(String supplierId);
    List<Product> findAll();
    boolean update(Product product);
    boolean delete(String productId);
    List<Product> findLowStock(int threshold);
}
```

#### 3. Interface CategoryDAO

```java
package inventorymanagementsystem.dao;

import inventorymanagementsystem.model.Category;
import java.util.List;
import java.util.Optional;

public interface CategoryDAO {
    boolean add(Category category);
    Optional<Category> findById(String categoryId);
    Optional<Category> findByName(String name);
    List<Category> findAll();
    boolean update(Category category);
    boolean delete(String categoryId);
}
```

#### 4. Interface SupplierDAO

```java
package inventorymanagementsystem.dao;

import inventorymanagementsystem.model.Supplier;
import java.util.List;
import java.util.Optional;

public interface SupplierDAO {
    boolean add(Supplier supplier);
    Optional<Supplier> findById(String supplierId);
    List<Supplier> findByName(String name);
    List<Supplier> findAll();
    boolean update(Supplier supplier);
    boolean delete(String supplierId);
}
```

#### 5. Interface TransactionDAO

```java
package inventorymanagementsystem.dao;

import inventorymanagementsystem.model.Transaction;
import java.time.LocalDateTime;
import java.util.List;
import java.util.Optional;

public interface TransactionDAO {
    boolean add(Transaction transaction);
    Optional<Transaction> findById(String transactionId);
    List<Transaction> findByProduct(String productId);
    List<Transaction> findByUser(String userId);
    List<Transaction> findByDateRange(LocalDateTime start, LocalDateTime end);
    List<Transaction> findAll();
    boolean update(Transaction transaction);
    boolean delete(String transactionId);
}
```

#### 6. Implementasi In-Memory UserDAO

```java
package inventorymanagementsystem.dao.impl;

import inventorymanagementsystem.dao.UserDAO;
import inventorymanagementsystem.model.User;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Optional;

public class InMemoryUserDAO implements UserDAO {
    private final Map<String, User> users = new HashMap<>();
    
    @Override
    public boolean add(User user) {
        if (users.containsKey(user.getUserId())) {
            return false;
        }
        users.put(user.getUserId(), user);
        return true;
    }

    @Override
    public Optional<User> findById(String userId) {
        return Optional.ofNullable(users.get(userId));
    }

    @Override
    public Optional<User> findByUsername(String username) {
        return users.values().stream()
                .filter(user -> user.getUsername().equals(username))
                .findFirst();
    }

    @Override
    public List<User> findAll() {
        return new ArrayList<>(users.values());
    }

    @Override
    public boolean update(User user) {
        if (!users.containsKey(user.getUserId())) {
            return false;
        }
        users.put(user.getUserId(), user);
        return true;
    }

    @Override
    public boolean delete(String userId) {
        if (!users.containsKey(userId)) {
            return false;
        }
        users.remove(userId);
        return true;
    }
}
```

#### 7. Implementasi Lainnya

Implementasikan rest of the DAO classes in a similar way. For brevity, we'll skip showing all implementations, but they follow the same pattern as the `InMemoryUserDAO`.

### Mengimplementasikan Service Layer

Selanjutnya, mari implementasikan Service Layer, yang berisi logika bisnis kita.

#### 1. Interface UserService

```java
package inventorymanagementsystem.service;

import inventorymanagementsystem.model.User;
import java.util.List;
import java.util.Optional;

public interface UserService {
    boolean registerUser(User user);
    boolean authenticateUser(String username, String password);
    Optional<User> getCurrentUser();
    void logout();
    List<User> getAllUsers();
    Optional<User> getUserById(String userId);
    boolean updateUser(User user);
    boolean deleteUser(String userId);
    boolean isAdmin();
}
```

#### 2. Interface ProductService

```java
package inventorymanagementsystem.service;

import inventorymanagementsystem.model.Product;
import java.util.List;
import java.util.Optional;

public interface ProductService {
    boolean addProduct(Product product);
    Optional<Product> getProductById(String productId);
    List<Product> searchProductsByName(String name);
    List<Product> getProductsByCategory(String categoryId);
    List<Product> getProductsBySupplier(String supplierId);
    List<Product> getAllProducts();
    boolean updateProduct(Product product);
    boolean deleteProduct(String productId);
    boolean increaseStock(String productId, int quantity);
    boolean decreaseStock(String productId, int quantity);
    List<Product> getLowStockProducts(int threshold);
}
```

#### 3. Implementasi UserServiceImpl

```java
package inventorymanagementsystem.service.impl;

import inventorymanagementsystem.dao.UserDAO;
import inventorymanagementsystem.model.Role;
import inventorymanagementsystem.model.User;
import inventorymanagementsystem.service.UserService;
import inventorymanagementsystem.util.PasswordUtils;
import java.util.List;
import java.util.Optional;

public class UserServiceImpl implements UserService {
    private final UserDAO userDAO;
    private User currentUser;
    
    public UserServiceImpl(UserDAO userDAO) {
        this.userDAO = userDAO;
    }
    
    @Override
    public boolean registerUser(User user) {
        // Check if username is already taken
        if (userDAO.findByUsername(user.getUsername()).isPresent()) {
            return false;
        }
        
        // Hash the password before storing it
        String hashedPassword = PasswordUtils.hashPassword(user.getPassword());
        User userWithHashedPassword = new User(
            user.getUserId(),
            user.getUsername(),
            hashedPassword,
            user.getFullName(),
            user.getRole()
        );
        
        return userDAO.add(userWithHashedPassword);
    }

    @Override
    public boolean authenticateUser(String username, String password) {
        Optional<User> userOpt = userDAO.findByUsername(username);
        
        if (!userOpt.isPresent()) {
            return false;
        }
        
        User user = userOpt.get();
        boolean authenticated = PasswordUtils.verifyPassword(password, user.getPassword());
        
        if (authenticated) {
            currentUser = user;
        }
        
        return authenticated;
    }

    @Override
    public Optional<User> getCurrentUser() {
        return Optional.ofNullable(currentUser);
    }

    @Override
    public void logout() {
        currentUser = null;
    }

    @Override
    public List<User> getAllUsers() {
        return userDAO.findAll();
    }

    @Override
    public Optional<User> getUserById(String userId) {
        return userDAO.findById(userId);
    }

    @Override
    public boolean updateUser(User user) {
        // Only admins can update other users
        if (!isAdmin() && (currentUser == null || !currentUser.getUserId().equals(user.getUserId()))) {
            return false;
        }
        
        return userDAO.update(user);
    }

    @Override
    public boolean deleteUser(String userId) {
        // Only admins can delete users
        if (!isAdmin()) {
            return false;
        }
        
        // Prevent deleting yourself
        if (currentUser != null && currentUser.getUserId().equals(userId)) {
            return false;
        }
        
        return userDAO.delete(userId);
    }

    @Override
    public boolean isAdmin() {
        return currentUser != null && currentUser.getRole() == Role.ADMIN;
    }
}
```

#### 4. Implementasi ProductServiceImpl

```java
package inventorymanagementsystem.service.impl;

import inventorymanagementsystem.dao.ProductDAO;
import inventorymanagementsystem.model.Product;
import inventorymanagementsystem.service.ProductService;
import java.util.List;
import java.util.Optional;

public class ProductServiceImpl implements ProductService {
    private final ProductDAO productDAO;
    
    public ProductServiceImpl(ProductDAO productDAO) {
        this.productDAO = productDAO;
    }
    
    @Override
    public boolean addProduct(Product product) {
        return productDAO.add(product);
    }

    @Override
    public Optional<Product> getProductById(String productId) {
        return productDAO.findById(productId);
    }

    @Override
    public List<Product> searchProductsByName(String name) {
        return productDAO.findByName(name);
    }

    @Override
    public List<Product> getProductsByCategory(String categoryId) {
        return productDAO.findByCategory(categoryId);
    }

    @Override
    public List<Product> getProductsBySupplier(String supplierId) {
        return productDAO.findBySupplier(supplierId);
    }

    @Override
    public List<Product> getAllProducts() {
        return productDAO.findAll();
    }

    @Override
    public boolean updateProduct(Product product) {
        return productDAO.update(product);
    }

    @Override
    public boolean deleteProduct(String productId) {
        return productDAO.delete(productId);
    }

    @Override
    public boolean increaseStock(String productId, int quantity) {
        if (quantity <= 0) {
            return false;
        }
        
        Optional<Product> productOpt = productDAO.findById(productId);
        if (!productOpt.isPresent()) {
            return false;
        }
        
        Product product = productOpt.get();
        try {
            product.increaseStock(quantity);
            return productDAO.update(product);
        } catch (IllegalArgumentException e) {
            return false;
        }
    }

    @Override
    public boolean decreaseStock(String productId, int quantity) {
        if (quantity <= 0) {
            return false;
        }
        
        Optional<Product> productOpt = productDAO.findById(productId);
        if (!productOpt.isPresent()) {
            return false;
        }
        
        Product product = productOpt.get();
        try {
            product.decreaseStock(quantity);
            return productDAO.update(product);
        } catch (IllegalArgumentException | IllegalStateException e) {
            return false;
        }
    }

    @Override
    public List<Product> getLowStockProducts(int threshold) {
        return productDAO.findLowStock(threshold);
    }
}
```

### Mengimplementasikan User Interface

Terakhir, mari implementasikan lapisan user interface untuk berinteraksi dengan pengguna.

#### 1. Utility Class InputHandler

```java
package inventorymanagementsystem.ui.util;

import java.util.Scanner;

public class InputHandler {
    private static final Scanner scanner = new Scanner(System.in);
    
    public static String readString(String prompt) {
        System.out.print(prompt + ": ");
        return scanner.nextLine();
    }
    
    public static int readInt(String prompt) {
        while (true) {
            try {
                System.out.print(prompt + ": ");
                return Integer.parseInt(scanner.nextLine());
            } catch (NumberFormatException e) {
                System.out.println("Please enter a valid number");
            }
        }
    }
    
    public static double readDouble(String prompt) {
        while (true) {
            try {
                System.out.print(prompt + ": ");
                return Double.parseDouble(scanner.nextLine());
            } catch (NumberFormatException e) {
                System.out.println("Please enter a valid number");
            }
        }
    }
    
    public static boolean readBoolean(String prompt) {
        while (true) {
            System.out.print(prompt + " (y/n): ");
            String input = scanner.nextLine().trim().toLowerCase();
            if (input.equals("y") || input.equals("yes")) {
                return true;
            } else if (input.equals("n") || input.equals("no")) {
                return false;
            } else {
                System.out.println("Please enter 'y' or 'n'");
            }
        }
    }
    
    public static void pressEnterToContinue() {
        System.out.println("\nPress Enter to continue...");
        scanner.nextLine();
    }
    
    public static void clearScreen() {
        // This doesn't actually clear the screen in all environments,
        // but it prints many newlines to simulate clearing
        for (int i = 0; i < 50; i++) {
            System.out.println();
        }
    }
}
```

#### 2. Main Menu UI Class

```java
package inventorymanagementsystem.ui;

import inventorymanagementsystem.model.User;
import inventorymanagementsystem.service.UserService;
import inventorymanagementsystem.ui.util.InputHandler;
import java.util.Optional;

public class MainMenuUI {
    private final UserService userService;
    private final ProductMenuUI productMenu;
    private final CategoryMenuUI categoryMenu;
    private final SupplierMenuUI supplierMenu;
    private final TransactionMenuUI transactionMenu;
    private final ReportMenuUI reportMenu;
    private final UserMenuUI userMenu;
    
    public MainMenuUI(UserService userService, ProductMenuUI productMenu, 
                     CategoryMenuUI categoryMenu, SupplierMenuUI supplierMenu,
                     TransactionMenuUI transactionMenu, ReportMenuUI reportMenu,
                     UserMenuUI userMenu) {
        this.userService = userService;
        this.productMenu = productMenu;
        this.categoryMenu = categoryMenu;
        this.supplierMenu = supplierMenu;
        this.transactionMenu = transactionMenu;
        this.reportMenu = reportMenu;
        this.userMenu = userMenu;
    }
    
    public void displayMainMenu() {
        while (true) {
            InputHandler.clearScreen();
            System.out.println("===== INVENTORY MANAGEMENT SYSTEM =====");
            
            Optional<User> currentUserOpt = userService.getCurrentUser();
            if (currentUserOpt.isPresent()) {
                User currentUser = currentUserOpt.get();
                System.out.println("Logged in as: " + currentUser.getFullName() + 
                                 " (" + currentUser.getRole() + ")");
            }
            
            System.out.println("\nMain Menu:");
            System.out.println("1. Product Management");
            System.out.println("2. Category Management");
            System.out.println("3. Supplier Management");
            System.out.println("4. Transaction Management");
            System.out.println("5. Reports");
            
            if (currentUserOpt.isPresent()) {
                if (userService.isAdmin()) {
                    System.out.println("6. User Management");
                }
                System.out.println("7. Logout");
            } else {
                System.out.println("6. Login");
                System.out.println("7. Register");
            }
            
            System.out.println("0. Exit");
            
            int choice = InputHandler.readInt("Enter your choice");
            
            if (!currentUserOpt.isPresent() && (choice >= 1 && choice <= 5)) {
                System.out.println("You must be logged in to access this feature.");
                InputHandler.pressEnterToContinue();
                continue;
            }
            
            switch (choice) {
                case 1:
                    productMenu.displayMenu();
                    break;
                case 2:
                    categoryMenu.displayMenu();
                    break;
                case 3:
                    supplierMenu.displayMenu();
                    break;
                case 4:
                    transactionMenu.displayMenu();
                    break;
                case 5:
                    reportMenu.displayMenu();
                    break;
                case 6:
                    if (currentUserOpt.isPresent() && userService.isAdmin()) {
                        userMenu.displayMenu();
                    } else {
                        displayLoginScreen();
                    }
                    break;
                case 7:
                    if (currentUserOpt.isPresent()) {
                        userService.logout();
                        System.out.println("Logged out successfully.");
                    } else {
                        displayRegistrationScreen();
                    }
                    InputHandler.pressEnterToContinue();
                    break;
                case 0:
                    System.out.println("Thank you for using the Inventory Management System!");
                    return;
                default:
                    System.out.println("Invalid choice. Please try again.");
                    InputHandler.pressEnterToContinue();
            }
        }
    }
    
    private void displayLoginScreen() {
        InputHandler.clearScreen();
        System.out.println("===== LOGIN =====");
        
        String username = InputHandler.readString("Username");
        String password = InputHandler.readString("Password");
        
        boolean authenticated = userService.authenticateUser(username, password);
        
        if (authenticated) {
            System.out.println("Login successful!");
        } else {
            System.out.println("Invalid username or password");
        }
        
        InputHandler.pressEnterToContinue();
    }
    
    private void displayRegistrationScreen() {
        InputHandler.clearScreen();
        System.out.println("===== REGISTER NEW USER =====");
        
        String userId = "U" + System.currentTimeMillis() % 10000;
        String username = InputHandler.readString("Username");
        
        // Check if username is available
        if (userService.getAllUsers().stream().anyMatch(u -> u.getUsername().equals(username))) {
            System.out.println("Username already taken");
            InputHandler.pressEnterToContinue();
            return;
        }
        
        String password = InputHandler.readString("Password");
        String fullName = InputHandler.readString("Full Name");
        
        // In a real app, you'd want better user validation
        User newUser = new User(userId, username, password, fullName, Role.STAFF);
        
        boolean registered = userService.registerUser(newUser);
        
        if (registered) {
            System.out.println("Registration successful! You can now log in.");
        } else {
            System.out.println("Registration failed");
        }
    }
}
```

#### 3. Main Application Class

```java
package inventorymanagementsystem;

import inventorymanagementsystem.dao.*;
import inventorymanagementsystem.dao.impl.*;
import inventorymanagementsystem.model.*;
import inventorymanagementsystem.service.*;
import inventorymanagementsystem.service.impl.*;
import inventorymanagementsystem.ui.*;

public class InventoryApp {
    
    public static void main(String[] args) {
        // Initialize DAOs
        UserDAO userDAO = new InMemoryUserDAO();
        ProductDAO productDAO = new InMemoryProductDAO();
        CategoryDAO categoryDAO = new InMemoryCategoryDAO();
        SupplierDAO supplierDAO = new InMemorySupplierDAO();
        TransactionDAO transactionDAO = new InMemoryTransactionDAO();
        
        // Initialize Services
        UserService userService = new UserServiceImpl(userDAO);
        ProductService productService = new ProductServiceImpl(productDAO);
        CategoryService categoryService = new CategoryServiceImpl(categoryDAO);
        SupplierService supplierService = new SupplierServiceImpl(supplierDAO);
        TransactionService transactionService = new TransactionServiceImpl(transactionDAO, productService, userService);
        ReportService reportService = new ReportServiceImpl(productService, transactionService);
        
        // Initialize UI components
        ProductMenuUI productMenu = new ProductMenuUI(productService, categoryService, supplierService);
        CategoryMenuUI categoryMenu = new CategoryMenuUI(categoryService, productService);
        SupplierMenuUI supplierMenu = new SupplierMenuUI(supplierService, productService);
        TransactionMenuUI transactionMenu = new TransactionMenuUI(transactionService, productService);
        ReportMenuUI reportMenu = new ReportMenuUI(reportService);
        UserMenuUI userMenu = new UserMenuUI(userService);
        
        // Initialize Main Menu
        MainMenuUI mainMenu = new MainMenuUI(userService, productMenu, categoryMenu, 
                                           supplierMenu, transactionMenu, reportMenu, userMenu);
        
        // Initialize demo data
        initDemoData(userService, categoryService, supplierService, productService);
        
        // Start the application
        mainMenu.displayMainMenu();
    }
    
    private static void initDemoData(UserService userService, CategoryService categoryService,
                                    SupplierService supplierService, ProductService productService) {
        // Create admin user
        User admin = new User("U1000", "admin", "admin123", "System Administrator", Role.ADMIN);
        userService.registerUser(admin);
        
        // Create categories
        Category electronics = new Category("C1001", "Electronics", "Electronic devices and accessories");
        Category clothing = new Category("C1002", "Clothing", "Clothing items for all ages");
        Category food = new Category("C1003", "Food", "Food and beverages");
        
        categoryService.addCategory(electronics);
        categoryService.addCategory(clothing);
        categoryService.addCategory(food);
        
        // Create suppliers
        Supplier techSupplier = new Supplier("S1001", "TechWorld", "John Tech", 
                                         "555-1234", "john@techworld.com", "123 Tech St");
        Supplier fashionSupplier = new Supplier("S1002", "Fashion House", "Mary Style", 
                                           "555-5678", "mary@fashionhouse.com", "456 Style Ave");
        Supplier foodSupplier = new Supplier("S1003", "Food Distributors", "Bob Eats", 
                                         "555-9012", "bob@fooddist.com", "789 Food Blvd");
        
        supplierService.addSupplier(techSupplier);
        supplierService.addSupplier(fashionSupplier);
        supplierService.addSupplier(foodSupplier);
        
        // Create products
        Product laptop = new Product("P1001", "Laptop", "15-inch laptop computer", 
                                   electronics.getCategoryId(), 999.99, 10, techSupplier.getSupplierId());
        Product smartphone = new Product("P1002", "Smartphone", "Latest model smartphone", 
                                      electronics.getCategoryId(), 599.99, 15, techSupplier.getSupplierId());
        Product tshirt = new Product("P1003", "T-Shirt", "Cotton t-shirt", 
                                   clothing.getCategoryId(), 19.99, 50, fashionSupplier.getSupplierId());
        Product jeans = new Product("P1004", "Jeans", "Denim jeans", 
                                  clothing.getCategoryId(), 39.99, 30, fashionSupplier.getSupplierId());
        Product chocolate = new Product("P1005", "Chocolate", "Dark chocolate bar", 
                                     food.getCategoryId(), 3.99, 100, foodSupplier.getSupplierId());
        
        productService.addProduct(laptop);
        productService.addProduct(smartphone);
        productService.addProduct(tshirt);
        productService.addProduct(jeans);
        productService.addProduct(chocolate);
    }
}
```

### Menghubungkan Komponen

Untuk menyelesaikan aplikasi, kita perlu membuat implementasi untuk semua class UI dan service yang belum diimplementasikan. Karena pembahasan kode lengkap akan terlalu panjang, kita telah menunjukkan komponen utama dan pattern yang digunakan.

Beberapa implementasi kunci lainnya yang perlu Anda buat:

1. Implementasi DAO untuk:
   - `InMemoryCategoryDAO`
   - `InMemoryProductDAO`
   - `InMemorySupplierDAO`
   - `InMemoryTransactionDAO`

2. Implementasi Service untuk:
   - `CategoryServiceImpl`
   - `SupplierServiceImpl`
   - `TransactionServiceImpl`
   - `ReportServiceImpl`

3. Implementasi UI untuk:
   - `ProductMenuUI`
   - `CategoryMenuUI`
   - `SupplierMenuUI`
   - `TransactionMenuUI`
   - `ReportMenuUI`
   - `UserMenuUI`

4. Implementasi utility:
   - `PasswordUtils` (untuk hashing password)
   - `DateUtils` (untuk format tanggal)

## Penerapan Konsep OOP

Dalam proyek ini, kita telah menerapkan berbagai konsep OOP. Mari kita bahas beberapa penerapan kunci.

### Inheritance dan Polymorphism

Contoh inheritance dan polymorphism dapat dilihat dalam hierarki Transaction:

```java
// Base abstract class
public abstract class Transaction { ... }

// Subclasses
public class InboundTransaction extends Transaction { ... }
public class OutboundTransaction extends Transaction { ... }
```

Kita menggunakan polymorphism saat bekerja dengan transactions tanpa perlu tahu tipe spesifiknya:

```java
// Example of polymorphism
List<Transaction> transactions = transactionDAO.findAll();
for (Transaction transaction : transactions) {
    // getTransactionType() calls the appropriate implementation
    System.out.println("Transaction type: " + transaction.getTransactionType());
}
```

### Interface dan Abstract Class

Kita telah menggunakan interface untuk mendefinisikan kontrak untuk services dan DAOs:

```java
public interface ProductDAO { ... }
public interface ProductService { ... }
```

Dan abstract class untuk Transaction, yang menyediakan implementasi dasar dan memaksa subclass untuk mengimplementasikan method tertentu:

```java
public abstract class Transaction {
    // Common implementation
    ...
    
    // To be implemented by subclasses
    public abstract String getTransactionType();
}
```

### Encapsulation dan Information Hiding

Kita telah menerapkan encapsulation dengan:
- Membuat fields private
- Menyediakan getters dan setters yang sesuai
- Menyembunyikan detail implementasi di balik interface

```java
public class Product {
    private String productId;
    private String name;
    private double price;
    // other fields...
    
    // Getters and setters
    // Business methods that enforce rules
}
```

### Collections Framework

Kita menggunakan collections untuk menyimpan dan mengelola data dalam implementasi in-memory:

```java
// Example from InMemoryUserDAO
private final Map<String, User> users = new HashMap<>();

@Override
public List<User> findAll() {
    return new ArrayList<>(users.values());
}
```

### Exception Handling

Kita menangani exceptions pada level aplikasi, seperti yang terlihat dalam ProductServiceImpl:

```java
@Override
public boolean decreaseStock(String productId, int quantity) {
    // ...
    try {
        product.decreaseStock(quantity);
        return productDAO.update(product);
    } catch (IllegalArgumentException | IllegalStateException e) {
        return false;
    }
}
```

Dan dalam Product class untuk business rules:

```java
public void decreaseStock(int quantity) {
    if (quantity <= 0) {
        throw new IllegalArgumentException("Quantity must be positive");
    }
    if (quantity > this.stockQuantity) {
        throw new IllegalStateException("Not enough stock available");
    }
    this.stockQuantity -= quantity;
}
```

### Lambda Expressions

Kita menggunakan lambda expressions dan method references di beberapa tempat, seperti dalam filter dan stream operations:

```java
// Example from UserServiceImpl
boolean usernameTaken = userDAO.findByUsername(user.getUsername()).isPresent();

// Example with lambda
List<Product> lowStockProducts = productDAO.findAll().stream()
    .filter(p -> p.getStockQuantity() < threshold)
    .collect(Collectors.toList());
```

## Pembahasan Pola Desain

Dalam proyek ini, kita telah menerapkan beberapa pola desain umum dalam pengembangan aplikasi.

### DAO Pattern

Data Access Object (DAO) pattern memisahkan logika akses data dari logika bisnis. Kita telah menerapkan ini dengan interface DAO dan implementasi konkritnya:

```java
// Interface
public interface ProductDAO { ... }

// Implementation
public class InMemoryProductDAO implements ProductDAO { ... }
```

Keuntungan:
- Memisahkan logika akses data, sehingga mudah untuk mengganti implementasi (misalnya dari in-memory menjadi database)
- Memudahkan testing karena kita dapat mock DAO
- Code organization yang lebih baik

### Service Pattern

Service pattern menyediakan layer abstraksi yang berisi logika bisnis:

```java
// Interface
public interface ProductService { ... }

// Implementation
public class ProductServiceImpl implements ProductService { ... }
```

Keuntungan:
- Pemisahan concern yang jelas
- Loose coupling antara UI dan akses data
- Reusability dan testability yang lebih baik

### Singleton Pattern

Meskipun tidak diimplementasikan secara eksplisit, services kita berperilaku seperti singleton dalam aplikasi ini. Dalam aplikasi yang lebih besar, kita bisa mengimplementasikan singleton pattern secara eksplisit:

```java
public class UserServiceSingleton {
    private static UserService instance;
    
    private UserServiceSingleton() {}
    
    public static synchronized UserService getInstance(UserDAO userDAO) {
        if (instance == null) {
            instance = new UserServiceImpl(userDAO);
        }
        return instance;
    }
}
```

### Factory Pattern

Kita dapat meningkatkan aplikasi dengan menambahkan factory pattern untuk membuat transaksi:

```java
public class TransactionFactory {
    public static Transaction createTransaction(String type, String transactionId, 
                                              String productId, int quantity,
                                              LocalDateTime timestamp, String userId, 
                                              String notes) {
        if ("INBOUND".equals(type)) {
            return new InboundTransaction(transactionId, productId, quantity, 
                                        timestamp, userId, notes);
        } else if ("OUTBOUND".equals(type)) {
            return new OutboundTransaction(transactionId, productId, quantity, 
                                         timestamp, userId, notes);
        } else {
            throw new IllegalArgumentException("Unknown transaction type: " + type);
        }
    }
}
```

## Testing dan Debugging

### Manual Testing

Untuk aplikasi konsol sederhana ini, kita dapat melakukan testing manual dengan menjalankan aplikasi dan mencoba fitur-fiturnya:

1. **Login Testing**:
   - Login dengan kredensial yang valid dan invalid
   - Verifikasi pembatasan akses berdasarkan role

2. **CRUD Testing untuk setiap Entity**:
   - Buat, baca, perbarui, dan hapus
   - Validasi bahwa data disimpan dan diambil dengan benar

3. **Business Logic Testing**:
   - Tambah/kurangi stok produk
   - Pastikan aturan bisnis dipatuhi (misalnya tidak bisa mengurangi stok jika tidak cukup)

4. **Exception Testing**:
   - Uji bagaimana aplikasi menangani input yang tidak valid
   - Pastikan error messages informatif

### Debugging Common Issues

Beberapa masalah umum yang mungkin Anda temui:

1. **NullPointerException**:
   - Pastikan semua dependencies diinjeksi dengan benar
   - Periksa nilai null sebelum dereference

2. **ConcurrentModificationException**:
   - Hindari memodifikasi collection saat iterasi
   - Gunakan copy of collection atau iterator.remove()

3. **Incorrect Business Logic**:
   - Tambahkan logging untuk melihat nilai variabel
   - Gunakan debugger IDE

4. **Authentication Issues**:
   - Periksa bahwa password hashing/verification bekerja dengan benar
   - Pastikan bahwa currentUser disimpan dan dihapus saat login/logout

## Peningkatan dan Pengembangan Lebih Lanjut

### Ide Peningkatan

Berikut beberapa ide untuk mengembangkan aplikasi ini lebih lanjut:

1. **Persistent Storage**:
   - Implementasikan DAO yang menggunakan database seperti SQLite, MySQL, atau PostgreSQL
   - Gunakan JPA/Hibernate untuk ORM

2. **GUI Interface**:
   - Konversi console app menjadi aplikasi desktop dengan JavaFX
   - Tambahkan form validasi dan user-friendly UI

3. **Fitur Tambahan**:
   - Fitur search dan filter yang lebih kompleks
   - Sistem notifikasi untuk stok rendah
   - Ekspor data ke CSV/Excel
   - Fitur backup/restore

4. **Security Enhancements**:
   - Implementasikan autentikasi yang lebih aman (misalnya bcrypt)
   - Tambahkan logging untuk audit trail
   - Authorization yang lebih granular

5. **Architecture Improvements**:
   - Dependency injection framework (seperti Spring)
   - Event-driven design untuk loose coupling yang lebih baik
   - Caching untuk performa

### Refactoring Opportunities

Beberapa area yang bisa direfactor dalam aplikasi ini:

1. **Error Handling**:
   - Buat custom exception hierarchy
   - Centralized error handling

2. **Input Validation**:
   - Implementasikan validation framework
   - Standardize validation logic

3. **Code Duplication**:
   - Refactor method yang berulang di DAO implementations
   - Buat BaseDAO abstract class

4. **Layering**:
   - Lebih jelas memisahkan concerns
   - Tambahkan DTOs (Data Transfer Objects) untuk transfer data antar layer

## Rangkuman

Dalam tutorial ini, kita telah mengimplementasikan sebuah aplikasi Inventory Management System sederhana yang menerapkan berbagai konsep OOP:

✅ **Class Structure** - Mendefinisikan domain models dan hubungan antar class

✅ **Inheritance dan Polymorphism** - Membuat hierarki class dan menggunakan interface

✅ **Encapsulation** - Menyembunyikan implementasi detail dan menyediakan API yang bersih

✅ **Interface dan Abstract Class** - Mendefinisikan kontrak dan behavior umum

✅ **Exception Handling** - Menangani error dan kasus pengecualian

✅ **Collections Framework** - Menggunakan data structures untuk menyimpan dan mengelola data

✅ **Design Patterns** - Menerapkan DAO, Service, Factory, dan Singleton patterns

Proyek ini menggabungkan konsep-konsep OOP yang telah kita pelajari di tutorial sebelumnya dan menunjukkan bagaimana mereka bekerja bersama dalam aplikasi dunia nyata. Aplikasi ini memiliki arsitektur multi-layer yang terorganisir dengan baik, menyediakan basis yang solid untuk pengembangan lebih lanjut dan peningkatan.

## Latihan Soal

1. Jelaskan bagaimana inheritance dan polymorphism diterapkan dalam proyek Inventory Management System. Berikan contoh spesifik dari kode.

2. Apa perbedaan antara DAO layer dan Service layer dalam aplikasi ini? Mengapa kita memisahkan keduanya?

3. Bagaimana encapsulation diterapkan dalam class Product? Apa manfaat dari pendekatan ini?

4. Jelaskan bagaimana exception handling diimplementasikan dalam method decreaseStock. Apa keuntungan dari pendekatan ini dibandingkan dengan membiarkan exception dipropagasi?

5. Implementasikan kelas ReportServiceImpl yang dapat menghasilkan berbagai laporan tentang inventory, seperti produk dengan stok rendah, nilai total inventory, dan produk yang paling banyak bertransaksi.

6. Modifikasi aplikasi untuk mendukung batch processing, seperti mengimpor banyak produk sekaligus dari file CSV.

7. Implementasikan nested transactions (misalnya, transaksi yang terdiri dari beberapa produk) dan pastikan integritas data terjaga (misalnya jika satu produk gagal, seluruh transaksi dibatalkan).

8. Tambahkan logging comprehensif ke aplikasi untuk membantu debugging dan audit. Gunakan framework logging seperti Log4j atau implementasikan solusi Anda sendiri.

9. Bagaimana Anda akan memodifikasi aplikasi ini untuk mendukung concurrent access oleh multiple users? Apa saja tantangan dan solusinya?

10. Desain dan implementasikan modul reporting yang menggunakan strategy pattern untuk mendukung berbagai format output (console, CSV, JSON).

## Referensi

1. Bloch, J. (2018). *Effective Java* (3rd ed.). Addison-Wesley Professional.

2. Martin, R. C. (2008). *Clean Code: A Handbook of Agile Software Craftsmanship*. Prentice Hall.

3. Gamma, E., Helm, R., Johnson, R., & Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley Professional.

4. Freeman, E., & Robson, E. (2020). *Head First Design Patterns* (2nd ed.). O'Reilly Media.

5. Fowler, M. (2002). *Patterns of Enterprise Application Architecture*. Addison-Wesley Professional.

6. Evans, E. (2003). *Domain-Driven Design: Tackling Complexity in the Heart of Software*. Addison-Wesley Professional.

7. Horstmann, C. S. (2019). *Core Java Volume I—Fundamentals* (11th ed.). Prentice Hall.

8. Walls, C. (2019). *Spring in Action* (5th ed.). Manning Publications.

9. Ottinger, J., & Lombardi, A. (2019). *Beginning Hibernate* (3rd ed.). Apress.

10. Laddad, R. (2009). *AspectJ in Action* (2nd ed.). Manning Publications.

---

[◀️ Kembali ke Tutorial #13: Collections Framework](13-collections.md) | [Lanjut ke Tutorial #15: Unit Testing untuk Kode OOP ▶️](15-unit-testing.md)

---

© 2023 Tutorial Dasar OOP di Java untuk Pemula. Semua hak cipta dilindungi.
