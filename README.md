# SQL Awakens

> An experimental RPG-style game project with a PHP/MySQL account system and a browser-based game entry point.

[ภาษาไทย](#ภาษาไทย) | [English](#english)

---

## ภาษาไทย

### เกี่ยวกับโปรเจกต์

**SQL Awakens** เป็นโปรเจกต์ทดลองพัฒนาเกมแนว RPG ที่เชื่อมต่อกับระบบสมาชิกด้วย PHP และ MySQL/MariaDB ผู้ใช้สามารถสมัครสมาชิก เข้าสู่ระบบ และเข้าสู่หน้าเกมได้

โปรเจกต์นี้เป็นพื้นที่สำหรับทดลองและเรียนรู้การทำงานร่วมกันระหว่าง Web Application, Database และ Game Client

### ฟีเจอร์ที่มีในโค้ดปัจจุบัน

- สมัครสมาชิกด้วยชื่อผู้ใช้และรหัสผ่าน
- เข้าสู่ระบบและตรวจสอบสถานะด้วย PHP Session
- เข้ารหัสและตรวจสอบรหัสผ่านด้วย PHP `password_hash()` และ `password_verify()`
- จัดเก็บข้อมูลบัญชีและช่องข้อมูล RPG จำนวน 20 ช่องในฐานข้อมูล
- หน้า Welcome สำหรับผู้ใช้ที่เข้าสู่ระบบแล้ว
- หน้าเริ่มต้นเกม HTML ที่อ้างอิงไลบรารีและสคริปต์ของ RPG Maker MV

### เทคโนโลยี

| ส่วน | เทคโนโลยี |
| --- | --- |
| Backend | PHP |
| Database | MySQL / MariaDB |
| Database administration | phpMyAdmin |
| Game client | HTML5 / JavaScript |
| Game runtime references | RPG Maker MV, PixiJS |
| Local development | Apache / XAMPP (แนะนำ) |

### โครงสร้างไฟล์หลัก

```text
SQLgame/
├── 127_0_0_1.sql       # Database export จาก phpMyAdmin
├── login.php           # หน้าเข้าสู่ระบบ
├── register.php        # หน้าสมัครสมาชิก
├── welcome.php         # หน้าหลังเข้าสู่ระบบและทางเข้าเกม
└── www/
    ├── index.html      # Game entry point (SQL Awakens)
    ├── package.json    # Desktop wrapper configuration
    └── package-lock.json
```

### การติดตั้งเพื่อทดลองบนเครื่อง Local

**สิ่งที่ต้องมี**

- PHP 8.0 หรือใหม่กว่า (แนะนำ PHP 8.2)
- MySQL หรือ MariaDB
- Apache Web Server
- phpMyAdmin (สำหรับนำเข้าฐานข้อมูล)

**ขั้นตอน**

1. ติดตั้ง XAMPP หรือเตรียม Apache, PHP และ MySQL/MariaDB ให้พร้อม
2. Clone โปรเจกต์ลงในโฟลเดอร์เว็บเซิร์ฟเวอร์ เช่น `htdocs` ของ XAMPP

   ```bash
   git clone https://github.com/tstoon3/SQLgame.git
   ```

3. เปิด Apache และ MySQL จาก XAMPP Control Panel
4. เปิด phpMyAdmin แล้วตรวจสอบไฟล์ `127_0_0_1.sql` ก่อน Import โดยโค้ด PHP ปัจจุบันคาดหวังฐานข้อมูลชื่อ `testdbno1` และตาราง `users`
5. ตรวจสอบและแก้ไขค่าการเชื่อมต่อฐานข้อมูลในไฟล์ `login.php`, `register.php` และ `welcome.php` ให้ตรงกับเครื่องของคุณ

   ```php
   $servername = "localhost";
   $username = "root";
   $password = "";
   $dbname = "testdbno1";
   ```

   เปลี่ยนค่าให้ตรงกับการตั้งค่าฐานข้อมูลในเครื่อง ไม่ควรใช้บัญชี `root` หรือรหัสผ่านว่างในระบบที่เปิดให้ผู้อื่นใช้งาน

6. เปิดหน้าเข้าสู่ระบบผ่านเว็บเบราว์เซอร์ เช่น

   ```text
   http://localhost/SQLgame/login.php
   ```

7. สมัครบัญชีและทดลองเข้าสู่ระบบ

### ข้อควรทราบและสิ่งที่ควรปรับปรุง

- `www/index.html` อ้างอิงไฟล์ JavaScript และไลบรารีภายใน `www/js/` แต่ไฟล์เหล่านี้ยังไม่ปรากฏในรายการไฟล์ที่ตรวจสอบได้ของ Repository ดังนั้นหน้าเกมอาจยังเปิดไม่ได้จากการ Clone ใหม่
- ไฟล์ `127_0_0_1.sql` เป็น Database Export จากเครื่องพัฒนาเดิม และมีตารางระบบของ phpMyAdmin รวมอยู่ด้วย ควรแยกเฉพาะ Schema ที่โปรเจกต์ต้องใช้ก่อนนำไปใช้งานจริง
- ค่าการเชื่อมต่อฐานข้อมูลถูกกำหนดไว้ในไฟล์ PHP โดยตรง ควรย้ายไปใช้ Environment Variables หรือไฟล์ตั้งค่าที่ไม่ถูก Commit
- `register.php` ควรใช้ Prepared Statements สำหรับทุก Query ที่รับค่าจากผู้ใช้ พร้อมเพิ่มการตรวจสอบข้อมูลฝั่ง Server
- ควรเพิ่มการจัดการ Session ที่รัดกุม การป้องกัน CSRF และการ Escape ข้อมูลก่อนแสดงผล
- โปรเจกต์นี้ควรถูกมองเป็น Prototype และยังไม่ควรเปิดใช้งานบน Public Server จนกว่าจะปรับปรุงด้านความปลอดภัย

---

## English

### About

**SQL Awakens** is an experimental RPG-style game project with a PHP and MySQL/MariaDB account system. Users can register, log in, and continue to the game entry page.

The project serves as a learning exercise combining web application development, database integration, and a game client.

### Current Features

- User registration with a username and password
- Login flow using PHP sessions
- Password hashing and verification with PHP `password_hash()` and `password_verify()`
- Account storage with 20 RPG save-data fields in the database
- A welcome page for authenticated users
- An HTML game entry point referencing RPG Maker MV runtime scripts

### Tech Stack

| Area | Technology |
| --- | --- |
| Backend | PHP |
| Database | MySQL / MariaDB |
| Database administration | phpMyAdmin |
| Game client | HTML5 / JavaScript |
| Game runtime references | RPG Maker MV, PixiJS |
| Local development | Apache / XAMPP (recommended) |

### Main Project Structure

```text
SQLgame/
├── 127_0_0_1.sql       # phpMyAdmin database export
├── login.php           # Login page
├── register.php        # Registration page
├── welcome.php         # Authenticated welcome page and game entry
└── www/
    ├── index.html      # SQL Awakens game entry point
    ├── package.json    # Desktop wrapper configuration
    └── package-lock.json
```

### Local Setup

**Prerequisites**

- PHP 8.0 or later (PHP 8.2 recommended)
- MySQL or MariaDB
- Apache Web Server
- phpMyAdmin (for database import)

**Steps**

1. Install XAMPP, or prepare Apache, PHP, and MySQL/MariaDB separately.
2. Clone this repository into your web server's document root (for example, XAMPP's `htdocs` directory).

   ```bash
   git clone https://github.com/tstoon3/SQLgame.git
   ```

3. Start Apache and MySQL from the XAMPP Control Panel.
4. Open phpMyAdmin and inspect `127_0_0_1.sql` before importing it. The current PHP code expects a database named `testdbno1` and a table named `users`.
5. Check and update the database connection settings in `login.php`, `register.php`, and `welcome.php`.

   ```php
   $servername = "localhost";
   $username = "root";
   $password = "";
   $dbname = "testdbno1";
   ```

   Use credentials that match your local database configuration. Do not use the MySQL `root` account or an empty password in a publicly accessible deployment.

6. Open the login page in your browser:

   ```text
   http://localhost/SQLgame/login.php
   ```

7. Register an account and test the login flow.

### Notes and Recommended Improvements

- `www/index.html` references JavaScript and runtime libraries under `www/js/`, but these files were not visible in the repository file listing inspected for this README. A fresh clone may therefore be missing files required to launch the game.
- `127_0_0_1.sql` is a development database export and includes phpMyAdmin system tables. Create a clean project-specific schema before using it in a production environment.
- Database credentials are hard-coded in the PHP files. Move them to environment variables or a configuration file that is excluded from version control.
- Use prepared statements for every query that includes user-supplied data in `register.php`, and add server-side input validation.
- Improve session security, add CSRF protection, and escape output before rendering user-controlled values.
- Treat this repository as a prototype. Do not expose it to the public internet until the security issues have been addressed.

---

## License

No license has been specified yet. Unless a license is added to this repository, the project remains under the default copyright terms of its author.
