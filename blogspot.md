# Rencana Project PHP Native Web Blog
## Fundamental PHP & Object-Oriented Programming

---

## 📋 **Informasi Project**

### **Tujuan Pembelajaran**
- Memahami fundamental PHP lebih mendalam
- Menguasai konsep Object-Oriented Programming (OOP) di PHP
- Membangun aplikasi blog sederhana dengan arsitektur yang terstruktur
- Transisi dari coding prosedural ke OOP

### **Prerequisites Siswa**
- Sudah bisa CRUD manual PHP (1 file HTML + 1 file action)
- Familiar dengan XAMPP/Laragon
- Memahami dasar-dasar HTML, CSS, dan MySQL

### **Environment Setup**
- **Siswa:** XAMPP atau Laragon
- **Pengajar:** Docker (PHP + MySQL + Nginx/Apache)
- **Compatibility:** Code yang dibuat akan compatible untuk kedua environment

### **Durasi Project**
8 Minggu (dapat disesuaikan dengan intensitas pertemuan)

---

## 📁 **Struktur Folder Final**

```
blog-project/
├── config/
│   └── Database.php           # Class koneksi database
├── models/
│   ├── Post.php               # Model untuk posts
│   ├── Category.php           # Model untuk categories
│   └── User.php               # Model untuk users (opsional)
├── controllers/
│   ├── PostController.php     # Controller untuk logic posts
│   └── CategoryController.php
├── views/
│   ├── layouts/
│   │   ├── header.php         # Template header
│   │   └── footer.php         # Template footer
│   ├── posts/
│   │   ├── index.php          # List semua posts
│   │   ├── show.php           # Detail post
│   │   ├── create.php         # Form create post
│   │   └── edit.php           # Form edit post
│   └── categories/
│       ├── index.php
│       └── create.php
├── public/
│   ├── css/
│   │   └── style.css
│   ├── js/
│   │   └── script.js
│   └── images/
├── helpers/
│   └── functions.php          # Helper functions
├── index.php                  # Entry point
└── .htaccess                  # URL routing (opsional)
```

---

## 🗓️ **Timeline & Fase Pembelajaran**

### **FASE 1: Foundation & Refactoring (Minggu 1-2)**

#### **Minggu 1: Review & Setup**

**Tujuan:**
- Review kemampuan CRUD siswa
- Identifikasi masalah pendekatan 1-file
- Perkenalan konsep separation of concerns

**Aktivitas:**

1. **Review CRUD Existing**
   - Siswa demo CRUD mereka (1 file HTML + 1 file action)
   - Diskusi: Apa masalahnya jika project berkembang besar?
   - Identifikasi code repetition

2. **Setup Project Baru**
   - Buat folder structure dasar
   - Setup database baru: `blog_db`
   - Create table `posts`:
     ```sql
     CREATE TABLE posts (
         id INT PRIMARY KEY AUTO_INCREMENT,
         title VARCHAR(200) NOT NULL,
         content TEXT NOT NULL,
         author VARCHAR(100),
         created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
         updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
     );
     ```

3. **Langkah Pertama: Pisahkan Database Connection**
   - Buat file `config/database.php`
   - Pindahkan koneksi database ke file terpisah
   - Gunakan `require_once` untuk include file

**Deliverable:**
- Project structure sudah dibuat
- Database connection terpisah dalam file `config/database.php`
- CRUD masih menggunakan cara lama tapi dengan koneksi terpisah

---

#### **Minggu 2: Separation of Concerns**

**Tujuan:**
- Memisahkan HTML dari PHP logic
- Memisahkan database operations
- Mengenal konsep MVC (pengenalan awal)

**Aktivitas:**

1. **Pisahkan Views dari Logic**
   - Buat folder `views/posts/`
   - Pindahkan HTML ke file views
   - File logic hanya handle data, lalu include view

2. **Struktur Sementara (Transisi):**
   ```
   ├── config/
   │   └── database.php
   ├── views/
   │   └── posts/
   │       ├── index.php      (HTML untuk list)
   │       ├── create.php     (HTML untuk form create)
   │       └── edit.php       (HTML untuk form edit)
   ├── actions/
   │   ├── post_create.php    (Logic untuk create)
   │   ├── post_update.php    (Logic untuk update)
   │   └── post_delete.php    (Logic untuk delete)
   └── index.php              (Entry point)
   ```

3. **Refactoring CRUD:**
   - Create: form di `views/posts/create.php`, action di `actions/post_create.php`
   - Read: tampilan di `views/posts/index.php`
   - Update: form di `views/posts/edit.php`, action di `actions/post_update.php`
   - Delete: action di `actions/post_delete.php`

**Deliverable:**
- CRUD dengan views dan logic terpisah
- Code lebih mudah dibaca dan di-maintain
- Siswa mulai memahami separation of concerns

---

### **FASE 2: Functions & Code Reusability (Minggu 3)**

#### **Minggu 3: Introduction to Functions**

**Tujuan:**
- Mengurangi code repetition dengan functions
- Memahami parameter dan return values
- Membangun library fungsi reusable

**Aktivitas:**

1. **Identifikasi Code Repetition**
   - Cari code yang diulang-ulang (query database, validation, dll)
   - Diskusi: Bagaimana cara menghindarinya?

2. **Buat Helper Functions**
   - File `helpers/functions.php`
   - Functions untuk:
     ```php
     // Database operations
     function getAllPosts($conn) { }
     function getPostById($conn, $id) { }
     function createPost($conn, $data) { }
     function updatePost($conn, $id, $data) { }
     function deletePost($conn, $id) { }
     
     // Utility functions
     function sanitizeInput($data) { }
     function redirect($url) { }
     function showMessage($message, $type) { }
     ```

3. **Refactoring dengan Functions**
   - Ganti semua query manual dengan function calls
   - Code jadi lebih bersih dan mudah dipahami

**Praktik:**
- Buat 1 function bersama-sama (live coding)
- Siswa refactor CRUD mereka menggunakan functions
- Code review bersama

**Deliverable:**
- File `helpers/functions.php` dengan minimal 5-7 functions
- CRUD refactored menggunakan functions
- Code lebih DRY (Don't Repeat Yourself)

---

### **FASE 3: Object-Oriented Programming Basics (Minggu 4-5)**

#### **Minggu 4: Pengenalan OOP - Class & Object**

**Tujuan:**
- Memahami konsep Class dan Object
- Membuat class pertama
- Properties dan Methods
- Constructor

**Konsep yang Diajarkan:**

1. **Apa itu OOP?**
   - Perbandingan dengan prosedural
   - Keuntungan OOP: reusability, scalability, maintainability
   - Real-world analogy (mobil, hewan, dll)

2. **Class & Object - Teori**
   - Class = Blueprint
   - Object = Instance dari class
   - Analogi: Class Mobil → Object: mobil Toyota, Honda, dll

3. **Praktik Sederhana (Non-Database Dulu)**
   ```php
   class Post {
       // Properties
       public $title;
       public $content;
       public $author;
       
       // Constructor
       public function __construct($title, $content, $author) {
           $this->title = $title;
           $this->content = $content;
           $this->author = $author;
       }
       
       // Methods
       public function getExcerpt($length = 100) {
           return substr($this->content, 0, $length) . '...';
       }
       
       public function display() {
           echo "<h2>{$this->title}</h2>";
           echo "<p>By {$this->author}</p>";
           echo "<p>{$this->getExcerpt()}</p>";
       }
   }
   ```

4. **Latihan:**
   - Buat object dari class Post
   - Akses properties dan methods
   - Buat beberapa instance berbeda

**Aktivitas:**
- Live coding: buat class sederhana bersama
- Siswa buat class `Category` dengan properties dan methods sendiri
- Diskusi: Kapan menggunakan OOP vs functions?

**Deliverable:**
- Class `Post` dasar (belum connect ke database)
- Pemahaman tentang class, object, properties, methods, constructor
- Latihan membuat minimal 1 class sendiri

---

#### **Minggu 5: OOP Lanjutan - Encapsulation & Database Integration**

**Tujuan:**
- Memahami encapsulation (visibility: public, private, protected)
- Getter & Setter methods
- Mengintegrasikan OOP dengan database
- Membuat Model class yang proper

**Konsep yang Diajarkan:**

1. **Encapsulation**
   - Mengapa perlu private properties?
   - Access modifiers: public, private, protected
   - Getter & Setter

   ```php
   class Post {
       private $id;
       private $title;
       private $content;
       
       // Getter
       public function getTitle() {
           return $this->title;
       }
       
       // Setter with validation
       public function setTitle($title) {
           if (strlen($title) < 5) {
               throw new Exception("Title too short");
           }
           $this->title = $title;
       }
   }
   ```

2. **Database Class**
   ```php
   class Database {
       private $host = "localhost";
       private $username = "root";
       private $password = "";
       private $database = "blog_db";
       private $connection;
       
       public function __construct() {
           $this->connection = new mysqli(
               $this->host,
               $this->username,
               $this->password,
               $this->database
           );
           
           if ($this->connection->connect_error) {
               die("Connection failed: " . $this->connection->connect_error);
           }
       }
       
       public function getConnection() {
           return $this->connection;
       }
       
       public function close() {
           $this->connection->close();
       }
   }
   ```

3. **Post Model dengan Database**
   ```php
   class Post {
       private $conn;
       private $id;
       private $title;
       private $content;
       private $author;
       
       public function __construct($db) {
           $this->conn = $db;
       }
       
       // Getters & Setters
       public function setId($id) { $this->id = $id; }
       public function setTitle($title) { $this->title = $title; }
       public function setContent($content) { $this->content = $content; }
       public function setAuthor($author) { $this->author = $author; }
       
       public function getId() { return $this->id; }
       public function getTitle() { return $this->title; }
       public function getContent() { return $this->content; }
       public function getAuthor() { return $this->author; }
       
       // CRUD Methods
       public function create() {
           $query = "INSERT INTO posts (title, content, author) VALUES (?, ?, ?)";
           $stmt = $this->conn->prepare($query);
           $stmt->bind_param("sss", $this->title, $this->content, $this->author);
           return $stmt->execute();
       }
       
       public function read() {
           $query = "SELECT * FROM posts ORDER BY created_at DESC";
           $result = $this->conn->query($query);
           return $result->fetch_all(MYSQLI_ASSOC);
       }
       
       public function readOne() {
           $query = "SELECT * FROM posts WHERE id = ?";
           $stmt = $this->conn->prepare($query);
           $stmt->bind_param("i", $this->id);
           $stmt->execute();
           return $stmt->get_result()->fetch_assoc();
       }
       
       public function update() {
           $query = "UPDATE posts SET title = ?, content = ?, author = ? WHERE id = ?";
           $stmt = $this->conn->prepare($query);
           $stmt->bind_param("sssi", $this->title, $this->content, $this->author, $this->id);
           return $stmt->execute();
       }
       
       public function delete() {
           $query = "DELETE FROM posts WHERE id = ?";
           $stmt = $this->conn->prepare($query);
           $stmt->bind_param("i", $this->id);
           return $stmt->execute();
       }
   }
   ```

**Aktivitas:**
- Refactoring: ubah functions menjadi methods dalam class
- Implementasi Database class
- Implementasi Post model dengan CRUD methods
- Testing setiap method

**Deliverable:**
- `config/Database.php` - class untuk database connection
- `models/Post.php` - model lengkap dengan CRUD
- CRUD berfungsi menggunakan OOP approach
- Pemahaman tentang encapsulation dan prepared statements

---

### **FASE 4: MVC Pattern & Advanced Features (Minggu 6-7)**

#### **Minggu 6: MVC Pattern Introduction**

**Tujuan:**
- Memahami konsep MVC (Model-View-Controller)
- Implementasi Controller layer
- Membuat aplikasi lebih terstruktur

**Konsep MVC:**
- **Model:** Data dan business logic (sudah ada)
- **View:** Presentasi/tampilan (sudah ada)
- **Controller:** Penghubung Model dan View (baru)

**Implementasi Controller:**

```php
// controllers/PostController.php
class PostController {
    private $db;
    private $post;
    
    public function __construct() {
        $database = new Database();
        $this->db = $database->getConnection();
        $this->post = new Post($this->db);
    }
    
    public function index() {
        $posts = $this->post->read();
        require_once 'views/posts/index.php';
    }
    
    public function show($id) {
        $this->post->setId($id);
        $post = $this->post->readOne();
        require_once 'views/posts/show.php';
    }
    
    public function create() {
        require_once 'views/posts/create.php';
    }
    
    public function store() {
        $this->post->setTitle($_POST['title']);
        $this->post->setContent($_POST['content']);
        $this->post->setAuthor($_POST['author']);
        
        if ($this->post->create()) {
            header("Location: index.php?success=1");
        } else {
            header("Location: index.php?error=1");
        }
    }
    
    public function edit($id) {
        $this->post->setId($id);
        $post = $this->post->readOne();
        require_once 'views/posts/edit.php';
    }
    
    public function update($id) {
        $this->post->setId($id);
        $this->post->setTitle($_POST['title']);
        $this->post->setContent($_POST['content']);
        $this->post->setAuthor($_POST['author']);
        
        if ($this->post->update()) {
            header("Location: index.php?success=1");
        } else {
            header("Location: index.php?error=1");
        }
    }
    
    public function destroy($id) {
        $this->post->setId($id);
        
        if ($this->post->delete()) {
            header("Location: index.php?success=1");
        } else {
            header("Location: index.php?error=1");
        }
    }
}
```

**Simple Router (index.php):**
```php
<?php
require_once 'config/Database.php';
require_once 'models/Post.php';
require_once 'controllers/PostController.php';

$controller = new PostController();

$action = $_GET['action'] ?? 'index';
$id = $_GET['id'] ?? null;

switch ($action) {
    case 'index':
        $controller->index();
        break;
    case 'show':
        $controller->show($id);
        break;
    case 'create':
        $controller->create();
        break;
    case 'store':
        $controller->store();
        break;
    case 'edit':
        $controller->edit($id);
        break;
    case 'update':
        $controller->update($id);
        break;
    case 'delete':
        $controller->destroy($id);
        break;
    default:
        $controller->index();
}
```

**Aktivitas:**
- Jelaskan flow MVC dengan diagram
- Implementasi PostController bersama-sama
- Refactor existing code ke pattern MVC
- Testing routing

**Deliverable:**
- `controllers/PostController.php` - controller lengkap
- `index.php` - simple router
- Aplikasi berfungsi dengan MVC pattern
- Pemahaman flow: User → Controller → Model → Database → Model → Controller → View

---

#### **Minggu 7: Additional Features & Relationships**

**Tujuan:**
- Implementasi fitur tambahan
- Memahami relasi one-to-many
- Pagination
- Search functionality

**Fitur yang Ditambahkan:**

1. **Categories (One-to-Many Relationship)**
   
   **Database:**
   ```sql
   CREATE TABLE categories (
       id INT PRIMARY KEY AUTO_INCREMENT,
       name VARCHAR(100) NOT NULL,
       slug VARCHAR(100) NOT NULL UNIQUE,
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );
   
   -- Tambah column di posts
   ALTER TABLE posts ADD COLUMN category_id INT;
   ALTER TABLE posts ADD FOREIGN KEY (category_id) REFERENCES categories(id);
   ```
   
   **Model Category:**
   ```php
   class Category {
       private $conn;
       private $id;
       private $name;
       private $slug;
       
       public function __construct($db) {
           $this->conn = $db;
       }
       
       // CRUD methods untuk Category
       public function create() { }
       public function read() { }
       public function readOne() { }
       public function update() { }
       public function delete() { }
       
       // Get posts by category
       public function getPosts() {
           $query = "SELECT * FROM posts WHERE category_id = ?";
           $stmt = $this->conn->prepare($query);
           $stmt->bind_param("i", $this->id);
           $stmt->execute();
           return $stmt->get_result()->fetch_all(MYSQLI_ASSOC);
       }
   }
   ```
   
   **Update Post Model:**
   ```php
   // Tambah method di Post class
   public function getCategory() {
       $query = "SELECT c.* FROM categories c 
                 INNER JOIN posts p ON p.category_id = c.id 
                 WHERE p.id = ?";
       $stmt = $this->conn->prepare($query);
       $stmt->bind_param("i", $this->id);
       $stmt->execute();
       return $stmt->get_result()->fetch_assoc();
   }
   ```

2. **Search Functionality**
   ```php
   // Tambah method di Post model
   public function search($keyword) {
       $keyword = "%{$keyword}%";
       $query = "SELECT * FROM posts 
                 WHERE title LIKE ? OR content LIKE ? 
                 ORDER BY created_at DESC";
       $stmt = $this->conn->prepare($query);
       $stmt->bind_param("ss", $keyword, $keyword);
       $stmt->execute();
       return $stmt->get_result()->fetch_all(MYSQLI_ASSOC);
   }
   ```

3. **Pagination**
   ```php
   // Tambah method di Post model
   public function readPaginated($start = 0, $limit = 10) {
       $query = "SELECT * FROM posts 
                 ORDER BY created_at DESC 
                 LIMIT ?, ?";
       $stmt = $this->conn->prepare($query);
       $stmt->bind_param("ii", $start, $limit);
       $stmt->execute();
       return $stmt->get_result()->fetch_all(MYSQLI_ASSOC);
   }
   
   public function countAll() {
       $query = "SELECT COUNT(*) as total FROM posts";
       $result = $this->conn->query($query);
       $row = $result->fetch_assoc();
       return $row['total'];
   }
   ```

4. **Validation Helper**
   ```php
   // helpers/Validator.php
   class Validator {
       private $errors = [];
       
       public function validate($data, $rules) {
           foreach ($rules as $field => $rule) {
               if ($rule === 'required' && empty($data[$field])) {
                   $this->errors[$field] = ucfirst($field) . " is required";
               }
               
               if (strpos($rule, 'min:') === 0) {
                   $min = (int)substr($rule, 4);
                   if (strlen($data[$field]) < $min) {
                       $this->errors[$field] = ucfirst($field) . " must be at least {$min} characters";
                   }
               }
               
               if (strpos($rule, 'max:') === 0) {
                   $max = (int)substr($rule, 4);
                   if (strlen($data[$field]) > $max) {
                       $this->errors[$field] = ucfirst($field) . " must not exceed {$max} characters";
                   }
               }
           }
           
           return empty($this->errors);
       }
       
       public function getErrors() {
           return $this->errors;
       }
   }
   ```

**Aktivitas:**
- Implementasi Category model dan controller
- Tambah dropdown category di form post
- Implementasi search box
- Implementasi pagination
- Implementasi validation

**Deliverable:**
- Categories CRUD lengkap
- Relasi category-post berfungsi
- Search dan pagination working
- Form validation implemented

---

### **FASE 5: Security & Best Practices (Minggu 8)**

#### **Minggu 8: Security, Polish, & Documentation**

**Tujuan:**
- Implementasi security measures
- Code refactoring dan cleanup
- Documentation
- Final testing

**Security Implementations:**

1. **Input Sanitization & Validation**
   - Semua input sudah menggunakan prepared statements ✓
   - Tambah HTML escaping untuk output:
   ```php
   // helpers/functions.php
   function escape($data) {
       return htmlspecialchars($data, ENT_QUOTES, 'UTF-8');
   }
   
   // Di views
   <h1><?php echo escape($post['title']); ?></h1>
   ```

2. **CSRF Protection (Basic)**
   ```php
   // helpers/Security.php
   class Security {
       public static function generateToken() {
           if (!isset($_SESSION['csrf_token'])) {
               $_SESSION['csrf_token'] = bin2hex(random_bytes(32));
           }
           return $_SESSION['csrf_token'];
       }
       
       public static function verifyToken($token) {
           return isset($_SESSION['csrf_token']) && 
                  hash_equals($_SESSION['csrf_token'], $token);
       }
   }
   
   // Di form
   <input type="hidden" name="csrf_token" value="<?php echo Security::generateToken(); ?>">
   
   // Di controller sebelum process
   if (!Security::verifyToken($_POST['csrf_token'])) {
       die("CSRF token validation failed");
   }
   ```

3. **Session Management**
   ```php
   // config/session.php
   session_start();
   
   // Regenerate session ID untuk prevent session fixation
   if (!isset($_SESSION['initiated'])) {
       session_regenerate_id(true);
       $_SESSION['initiated'] = true;
   }
   ```

4. **Error Handling**
   ```php
   // config/error_handler.php
   // Jangan tampilkan error di production
   ini_set('display_errors', 0);
   ini_set('log_errors', 1);
   ini_set('error_log', __DIR__ . '/../logs/error.log');
   
   // Custom error handler
   function customErrorHandler($errno, $errstr, $errfile, $errline) {
       error_log("Error: [$errno] $errstr - $errfile:$errline");
       // Tampilkan user-friendly message
       echo "Something went wrong. Please try again later.";
   }
   
   set_error_handler("customErrorHandler");
   ```

**Best Practices Checklist:**

- [ ] Semua query menggunakan prepared statements
- [ ] Input validation di semua form
- [ ] Output escaping untuk prevent XSS
- [ ] CSRF protection di form
- [ ] Error logging (jangan display error ke user)
- [ ] Session security
- [ ] Naming convention konsisten
- [ ] Code comments untuk fungsi kompleks
- [ ] Separation of concerns terjaga
- [ ] No hardcoded credentials (gunakan config file)

**Code Refactoring:**
- Review semua code untuk consistency
- Hapus code yang tidak terpakai
- Improve readability
- Add comments dimana perlu

**UI/UX Polish:**
- Tambah Bootstrap atau CSS framework
- Success/error flash messages
- Loading states
- Responsive design
- User-friendly error messages

**Documentation:**

1. **README.md**
   ```markdown
   # Blog Application - PHP Native OOP
   
   ## Requirements
   - PHP 7.4+
   - MySQL 5.7+
   - XAMPP/Laragon
   
   ## Installation
   1. Clone/download project
   2. Import `database.sql` ke MySQL
   3. Update database credentials di `config/Database.php`
   4. Akses via browser: `http://localhost/blog-project`
   
   ## Features
   - CRUD Posts
   - Categories management
   - Search posts
   - Pagination
   - Input validation
   - CSRF protection
   
   ## Project Structure
   - `config/` - Database configuration
   - `models/` - Data models
   - `controllers/` - Application logic
   - `views/` - HTML templates
   - `helpers/` - Utility functions
   ```

2. **Code Documentation**
   - PHPDoc comments untuk class dan method penting
   ```php
   /**
    * Post Model
    * Handles all post-related database operations
    */
   class Post {
       /**
        * Create new post
        * @return bool Success status
        */
       public function create() {
           // ...
       }
   }
   ```

**Final Testing:**
- Test semua fitur CRUD
- Test validation (input invalid data)
- Test search dengan berbagai keyword
- Test pagination
- Test security (SQL injection attempts, XSS)
- Cross-browser testing (Chrome, Firefox)
- Responsive testing (mobile, tablet)

**Deliverable:**
- Aplikasi blog lengkap dan aman
- Code bersih dan terdokumentasi
- README.md lengkap
- Database export file
- Siap untuk deployment/presentation

---

## 📊 **Kriteria Evaluasi**

### **1. Pemahaman OOP (35%)**
- [ ] Membuat dan menggunakan class dengan benar
- [ ] Implementasi properties dan methods
- [ ] Penggunaan constructor
- [ ] Encapsulation (private/public)
- [ ] Getter dan Setter
- [ ] Pemahaman konsep MVC

### **2. Functionality (30%)**
- [ ] CRUD posts berfungsi sempurna
- [ ] CRUD categories berfungsi
- [ ] Search berfungsi
- [ ] Pagination berfungsi
- [ ] Relasi category-post bekerja
- [ ] Tidak ada critical bugs

### **3. Code Quality (20%)**
- [ ] Code terorganisir dengan baik (struktur folder)
- [ ] Naming convention konsisten
- [ ] Code readable dan maintainable
- [ ] Comments pada bagian penting
- [ ] Tidak ada code duplication
- [ ] Separation of concerns terjaga

### **4. Security & Best Practices (15%)**
- [ ] Prepared statements untuk semua query
- [ ] Input validation
- [ ] Output escaping (XSS prevention)
- [ ] CSRF protection
- [ ] Error handling yang baik
- [ ] Session management

---

## 🎯 **Milestones Checklist**

### **Week 1:**
- [ ] Project setup complete
- [ ] Database created
- [ ] Database connection separated

### **Week 2:**
- [ ] Views separated from logic
- [ ] CRUD with separated files working
- [ ] Understanding separation of concerns

### **Week 3:**
- [ ] Helper functions created
- [ ] CRUD refactored using functions
- [ ] Code DRY achieved

### **Week 4:**
- [ ] First OOP class created
- [ ] Understanding class, object, constructor
- [ ] Practice creating objects

### **Week 5:**
- [ ] Database class implemented
- [ ] Post model with CRUD methods
- [ ] Understanding encapsulation
- [ ] Prepared statements implemented

### **Week 6:**
- [ ] MVC pattern implemented
- [ ] Controller layer created
- [ ] Simple routing working
- [ ] Understanding MVC flow

### **Week 7:**
- [ ] Categories feature complete
- [ ] Search functionality working
- [ ] Pagination implemented
- [ ] Validation working

### **Week 8:**
- [ ] Security measures implemented
- [ ] Code polished and documented
- [ ] README complete
- [ ] Final testing done
- [ ] Project ready for presentation

---

## 💡 **Tips Pengajaran**

### **Untuk Pengajar:**

1. **Live Coding**
   - Coding bersama untuk setiap konsep baru
   - Biarkan siswa follow along
   - Jelaskan setiap baris code

2. **Code Review Sessions**
   - Review code siswa setiap minggu
   - Berikan feedback konstruktif
   - Diskusi best practices

3. **Debugging Together**
   - Ketika ada error, debug bersama
   - Ajarkan cara membaca error messages
   - Latih problem-solving skills

4. **Progressive Complexity**
   - Jangan skip steps
   - Pastikan siswa paham sebelum lanjut
   - Review konsep sebelumnya jika perlu

5. **Real-World Context**
   - Jelaskan kenapa konsep ini penting di industri
   - Berikan contoh penggunaan di aplikasi nyata
   - Relate dengan framework modern (Laravel, CodeIgniter)

6. **Encourage Questions**
   - Buat environment yang safe untuk bertanya
   - Tidak ada pertanyaan bodoh
   - Diskusi terbuka

7. **Pair Programming**
   - Sesekali buat siswa coding berpasangan
   - Peer learning sangat efektif
   - Code review antar siswa

### **Untuk Siswa:**

1. **Practice, Practice, Practice**
   - Jangan hanya copy-paste
   - Ketik ulang setiap code
   - Eksperimen dengan modifikasi

2. **Understand, Don't Memorize**
   - Pahami konsep, bukan hafal syntax
   - Tanya "kenapa" bukan hanya "bagaimana"
   - Relate dengan konsep yang sudah dipahami

3. **Debug Yourself First**
   - Coba solve error sendiri dulu
   - Baca error message dengan teliti
   - Google adalah teman terbaik

4. **Take Notes**
   - Catat konsep-konsep penting
   - Buat cheat sheet sendiri
   - Review notes sebelum pertemuan

5. **Build Portfolio**
   - Project ini bisa jadi portfolio
   - Document dengan baik
   - Upload ke GitHub

---

## 🛠️ **Tools & Resources**

### **Development Tools:**
- **Code Editor:** VS Code (recommended), Sublime Text, PHPStorm
- **Database Management:** phpMyAdmin (included in XAMPP/Laragon)
- **Version Control:** Git & GitHub (opsional tapi recommended)
- **Browser DevTools:** Chrome DevTools untuk debugging

### **Recommended VS Code Extensions:**
- PHP Intelephense
- PHP DocBlocker
- MySQL (untuk query langsung dari VS Code)
- Live Server (untuk auto-reload)
- Bracket Pair Colorizer

### **Learning Resources:**
- **PHP Manual:** https://www.php.net/manual/en/
- **W3Schools PHP:** https://www.w3schools.com/php/
- **PHP OOP Tutorial:** https://www.tutorialspoint.com/php/php_object_oriented.htm
- **Stack Overflow:** Untuk troubleshooting

### **Dokumentasi Referensi:**
- MySQL Documentation
- Bootstrap Documentation (untuk styling)
- MDN Web Docs (HTML/CSS/JavaScript)

---

## 📝 **Troubleshooting Guide**

### **Common Issues & Solutions:**

1. **Database Connection Failed**
   ```
   Error: Connection refused
   Solution: 
   - Pastikan MySQL service running
   - Check username/password di config/Database.php
   - Verify database name sudah dibuat
   ```

2. **Class Not Found**
   ```
   Error: Class 'Post' not found
   Solution:
   - Pastikan file sudah di-require_once
   - Check path file apakah benar
   - Verify nama class sama dengan nama file
   ```

3. **Undefined Variable**
   ```
   Error: Undefined variable: post
   Solution:
   - Variable belum di-assign value
   - Check typo nama variable
   - Pastikan data sudah di-pass dari controller ke view
   ```

4. **Headers Already Sent**
   ```
   Error: Cannot modify header information
   Solution:
   - Pastikan tidak ada output (echo, HTML) sebelum header()
   - Check whitespace di awal file PHP
   - Gunakan ob_start() jika perlu
   ```

5. **Call to Undefined Method**
   ```
   Error: Call to undefined method Post::readAll()
   Solution:
   - Method belum dibuat di class
   - Check typo nama method
   - Pastikan object sudah di-instantiate
   ```

---

## 🎓 **Learning Outcomes**

Setelah menyelesaikan project ini, siswa diharapkan:

### **Technical Skills:**
- ✅ Memahami fundamental PHP dengan baik
- ✅ Menguasai konsep OOP (Class, Object, Encapsulation, Inheritance)
- ✅ Mampu implementasi MVC pattern
- ✅ Bisa membuat CRUD dengan prepared statements
- ✅ Memahami database relationships
- ✅ Implementasi basic security measures
- ✅ Code organization dan best practices

### **Soft Skills:**
- ✅ Problem-solving mindset
- ✅ Debugging skills
- ✅ Code reading & review
- ✅ Documentation skills
- ✅ Collaborative coding

### **Career Readiness:**
- ✅ Portfolio project yang presentable
- ✅ Foundation untuk belajar framework (Laravel, CodeIgniter)
- ✅ Understanding web application architecture
- ✅ Ready untuk junior developer position

---

## 🚀 **Next Steps After Project**

### **Immediate Next Steps:**
1. **Refine the Project**
   - Add user authentication
   - Implement image upload for posts
   - Add comments system
   - Create admin panel

2. **Deploy the Project**
   - Learn about web hosting
   - Deploy to shared hosting atau VPS
   - Setup domain dan SSL

3. **Learn Version Control**
   - Git basics
   - GitHub untuk portfolio
   - Collaborative development

### **Advanced Learning Path:**

1. **Framework Transition**
   - Laravel (most popular)
   - CodeIgniter (lightweight)
   - Symfony (enterprise level)

2. **Frontend Enhancement**
   - JavaScript ES6+
   - Vue.js atau React
   - AJAX & Fetch API
   - REST API development

3. **Database Optimization**
   - Indexing
   - Query optimization
   - Database design patterns

4. **Security Deep Dive**
   - OWASP Top 10
   - Authentication & Authorization
   - JWT, OAuth
   - Penetration testing basics

5. **DevOps Basics**
   - Docker (containerization)
   - CI/CD pipelines
   - Server management
   - Cloud platforms (AWS, Digital Ocean)

---

## 📦 **Starter Files Template**

### **Database Schema (database.sql):**
```sql
-- Create Database
CREATE DATABASE IF NOT EXISTS blog_db;
USE blog_db;

-- Categories Table
CREATE TABLE categories (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    slug VARCHAR(100) NOT NULL UNIQUE,
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

-- Posts Table
CREATE TABLE posts (
    id INT PRIMARY KEY AUTO_INCREMENT,
    category_id INT,
    title VARCHAR(200) NOT NULL,
    slug VARCHAR(200) NOT NULL UNIQUE,
    content TEXT NOT NULL,
    excerpt VARCHAR(500),
    author VARCHAR(100),
    featured_image VARCHAR(255),
    status ENUM('draft', 'published') DEFAULT 'draft',
    views INT DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (category_id) REFERENCES categories(id) ON DELETE SET NULL
);

-- Insert Sample Categories
INSERT INTO categories (name, slug, description) VALUES
('Technology', 'technology', 'Tech news and tutorials'),
('Programming', 'programming', 'Coding tips and tricks'),
('Lifestyle', 'lifestyle', 'Life and wellness articles');

-- Insert Sample Posts
INSERT INTO posts (category_id, title, slug, content, excerpt, author, status) VALUES
(1, 'Getting Started with PHP', 'getting-started-with-php', 'PHP is a popular server-side scripting language...', 'Learn the basics of PHP programming', 'John Doe', 'published'),
(2, 'Introduction to OOP', 'introduction-to-oop', 'Object-Oriented Programming is a paradigm...', 'Understanding OOP concepts', 'Jane Smith', 'published');
```

### **.htaccess (untuk clean URLs - opsional):**
```apache
RewriteEngine On

# Redirect to index.php
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php?url=$1 [QSA,L]

# Prevent directory listing
Options -Indexes

# Protect config files
<FilesMatch "^(config|database)\.php$">
    Order allow,deny
    Deny from all
</FilesMatch>
```

### **config/config.php:**
```php
<?php
// Application Configuration
define('APP_NAME', 'My Blog');
define('APP_URL', 'http://localhost/blog-project');
define('APP_VERSION', '1.0.0');

// Database Configuration
define('DB_HOST', 'localhost');
define('DB_USER', 'root');
define('DB_PASS', '');
define('DB_NAME', 'blog_db');

// Pagination
define('POSTS_PER_PAGE', 10);

// Paths
define('BASE_PATH', __DIR__ . '/..');
define('VIEWS_PATH', BASE_PATH . '/views');
define('UPLOADS_PATH', BASE_PATH . '/public/uploads');

// Security
define('CSRF_TOKEN_NAME', 'csrf_token');

// Error Reporting
if ($_SERVER['SERVER_NAME'] === 'localhost') {
    // Development
    error_reporting(E_ALL);
    ini_set('display_errors', 1);
} else {
    // Production
    error_reporting(0);
    ini_set('display_errors', 0);
    ini_set('log_errors', 1);
    ini_set('error_log', BASE_PATH . '/logs/error.log');
}
```

---

## 📋 **Weekly Assignment Template**

### **Week 1 Assignment:**
**Goal:** Setup project dan pisahkan database connection

**Tasks:**
1. [ ] Install XAMPP/Laragon
2. [ ] Create project folder
3. [ ] Create database `blog_db`
4. [ ] Create `posts` table
5. [ ] Create `config/database.php`
6. [ ] Test connection with simple query
7. [ ] Screenshot hasil test connection

**Submission:**
- Folder structure screenshot
- Database screenshot
- Working connection proof

---

### **Week 2 Assignment:**
**Goal:** Refactor CRUD dengan separated files

**Tasks:**
1. [ ] Create `views/posts/` folder
2. [ ] Separate HTML to view files
3. [ ] Create `actions/` folder for logic
4. [ ] Refactor Create operation
5. [ ] Refactor Read operation
6. [ ] Refactor Update operation
7. [ ] Refactor Delete operation
8. [ ] Test all CRUD operations

**Submission:**
- Updated folder structure
- Working CRUD demonstration
- Code screenshots

---

### **Week 3 Assignment:**
**Goal:** Create reusable functions

**Tasks:**
1. [ ] Create `helpers/functions.php`
2. [ ] Create `getAllPosts()` function
3. [ ] Create `getPostById()` function
4. [ ] Create `createPost()` function
5. [ ] Create `updatePost()` function
6. [ ] Create `deletePost()` function
7. [ ] Refactor CRUD to use functions
8. [ ] Add input sanitization function

**Submission:**
- `functions.php` file
- Refactored action files
- Test results

---

### **Week 4 Assignment:**
**Goal:** Create first OOP class

**Tasks:**
1. [ ] Create `models/Post.php`
2. [ ] Define Post class with properties
3. [ ] Add constructor
4. [ ] Add getter methods
5. [ ] Add setter methods
6. [ ] Add `display()` method
7. [ ] Create test file to instantiate Post objects
8. [ ] Document class with comments

**Submission:**
- Post class file
- Test file with multiple objects
- Explanation of OOP concepts learned

---

### **Week 5 Assignment:**
**Goal:** Integrate OOP with database

**Tasks:**
1. [ ] Create `config/Database.php` class
2. [ ] Update Post model with database integration
3. [ ] Implement `create()` method
4. [ ] Implement `read()` method
5. [ ] Implement `readOne()` method
6. [ ] Implement `update()` method
7. [ ] Implement `delete()` method
8. [ ] Use prepared statements for all queries
9. [ ] Test all methods

**Submission:**
- Database class
- Complete Post model
- Test results for each method

---

### **Week 6 Assignment:**
**Goal:** Implement MVC pattern

**Tasks:**
1. [ ] Create `controllers/PostController.php`
2. [ ] Implement all controller methods
3. [ ] Update `index.php` with routing
4. [ ] Update views to work with controller
5. [ ] Test complete flow
6. [ ] Draw MVC flow diagram
7. [ ] Document understanding of MVC

**Submission:**
- PostController file
- Updated index.php
- MVC flow diagram
- Working application demonstration

---

### **Week 7 Assignment:**
**Goal:** Add advanced features

**Tasks:**
1. [ ] Create Category model
2. [ ] Create Category controller
3. [ ] Add category CRUD
4. [ ] Update posts to include category
5. [ ] Implement search functionality
6. [ ] Implement pagination
7. [ ] Add form validation
8. [ ] Test all new features

**Submission:**
- Category implementation files
- Search demonstration
- Pagination demonstration
- Validation demonstration

---

### **Week 8 Assignment:**
**Goal:** Security, polish, and documentation

**Tasks:**
1. [ ] Implement CSRF protection
2. [ ] Add output escaping
3. [ ] Implement error handling
4. [ ] Add success/error messages
5. [ ] Polish UI with CSS
6. [ ] Write README.md
7. [ ] Add code comments
8. [ ] Export database
9. [ ] Final testing
10. [ ] Prepare presentation

**Submission:**
- Complete project ZIP
- README.md
- Database export
- Presentation slides
- Video demo (optional)

---

## 🎯 **Final Project Presentation Guide**

### **Presentation Structure (10-15 minutes):**

1. **Introduction (2 min)**
   - Project overview
   - Technologies used
   - Development timeline

2. **Features Demo (5 min)**
   - CRUD operations
   - Category management
   - Search & pagination
   - Live demonstration

3. **Technical Highlights (5 min)**
   - OOP implementation
   - MVC architecture
   - Security measures
   - Code structure walkthrough

4. **Challenges & Solutions (2 min)**
   - Biggest challenges faced
   - How you solved them
   - Key learnings

5. **Q&A (3 min)**
   - Answer questions
   - Discuss improvements
   - Future enhancements

### **Presentation Tips:**
- Practice your demo beforehand
- Prepare for potential questions
- Have backup plan if demo fails
- Show your best code examples
- Be honest about challenges
- Show enthusiasm for learning

---

## 🌟 **Bonus Features (untuk siswa advanced)**

Jika siswa sudah menyelesaikan core features, bisa tambahkan:

1. **User Authentication**
   - Login/Register system
   - Password hashing
   - Session management
   - User roles (admin, author, reader)

2. **Comments System**
   - Users can comment on posts
   - Nested comments (replies)
   - Comment moderation

3. **Image Upload**
   - Featured image for posts
   - Image validation
   - Image resize
   - File management

4. **Rich Text Editor**
   - Integrate CKEditor atau TinyMCE
   - Better content formatting
   - Image insertion

5. **Tags System**
   - Many-to-many relationship
   - Tag management
   - Filter by tags

6. **Email Notifications**
   - Email on new post
   - Newsletter system
   - Contact form

7. **API Development**
   - RESTful API
   - JSON responses
   - API authentication

8. **Performance Optimization**
   - Caching
   - Query optimization
   - Lazy loading

---

## 📞 **Support & Communication**

### **Communication Channels:**
- **Kelas:** Diskusi langsung saat pertemuan
- **Group Chat:** WhatsApp/Telegram untuk pertanyaan cepat
- **Email:** Untuk submission assignment
- **GitHub Issues:** Untuk track bugs dan feature requests (jika menggunakan Git)

### **Office Hours:**
- Set jadwal untuk konsultasi
- Online/offline availability
- Response time expectations

### **Getting Help:**
1. Try to solve yourself (15-30 minutes)
2. Google the error message
3. Ask classmates
4. Ask instructor
5. Check documentation

---

## ✅ **Final Checklist**

Before considering project complete, check:

### **Functionality:**
- [ ] Create post works
- [ ] Read/list posts works
- [ ] Update post works
- [ ] Delete post works
- [ ] Category CRUD works
- [ ] Search works
- [ ] Pagination works
- [ ] Validation works
- [ ] No critical bugs

### **Code Quality:**
- [ ] OOP properly implemented
- [ ] MVC pattern followed
- [ ] Code is organized
- [ ] Naming conventions consistent
- [ ] Comments added where needed
- [ ] No unused code
- [ ] Prepared statements used

### **Security:**
- [ ] SQL injection prevented
- [ ] XSS prevented
- [ ] CSRF protection added
- [ ] Input validation
- [ ] Output escaping
- [ ] Error handling

### **Documentation:**
- [ ] README.md complete
- [ ] Code comments added
- [ ] Database schema documented
- [ ] Setup instructions clear
- [ ] Features documented

### **Presentation:**
- [ ] Clean UI
- [ ] Responsive design
- [ ] User-friendly messages
- [ ] Professional appearance

---

## 🎊 **Congratulations!**

Setelah menyelesaikan project ini, kamu telah:
- ✅ Membangun aplikasi web complete dari scratch
- ✅ Menguasai fundamental PHP dan OOP
- ✅ Memahami arsitektur aplikasi yang baik
- ✅ Siap untuk belajar framework modern
- ✅ Punya portfolio project yang solid

**Keep learning, keep coding! 🚀**

---

## 📚 **Appendix**

### **A. Git Basics (Optional)**
```bash
# Initialize repository
git init

# Add files
git add .

# Commit
git commit -m "Initial commit"

# Connect to GitHub
git remote add origin [your-repo-url]

# Push
git push -u origin main
```

### **B. Useful PHP Snippets**

**Debug Helper:**
```php
function dd($data) {
    echo '<pre>';
    var_dump($data);
    echo '</pre>';
    die();
}
```

**Redirect Helper:**
```php
function redirect($url, $message = null, $type = 'success') {
    if ($message) {
        $_SESSION['message'] = $message;
        $_SESSION['message_type'] = $type;
    }
    header("Location: $url");
    exit;
}
```

**Flash Message Helper:**
```php
function flash($key = null) {
    if ($key === null) {
        return isset($_SESSION['message']);
    }
    
    if (isset($_SESSION[$key])) {
        $value = $_SESSION[$key];
        unset($_SESSION[$key]);
        return $value;
    }
    return null;
}
```

### **C. MySQL Useful Queries**

**Backup Database:**
```bash
mysqldump -u root -p blog_db > backup.sql
```

**Restore Database:**
```bash
mysql -u root -p blog_db < backup.sql
```

**Check Table Structure:**
```sql
DESCRIBE posts;
```

**Count Records:**
```sql
SELECT COUNT(*) FROM posts;
```

---

**End of Document**

_Version 1.0 - Last Updated: January 2026_