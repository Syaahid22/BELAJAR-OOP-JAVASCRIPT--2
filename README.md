[OOP #2.txt](https://github.com/user-attachments/files/21821995/OOP.2.txt)
Object-Oriented Programming
Basic concept Encapsulation dalam OOP Javascript

Penjelasan Encapsulation
Enkapsulasi adalah salah satu konsep dasar dalam OOP yang bertujuan agar sebuah class data properties dan method yang kita miliki dibungkus dengan aman, 
datanya terlindungi dan penggunaannya menjadi lebih simpel.
Maksudnya, ketika user bisa menjalankan/menggunakan interface (public method) tanpa perlu tau bagaimana sistem internal memproses interface tersebut.


A. Tujuan Encapsulation
1. Keamanan Data
Mencegah akses langsung yang bisa merusak data. Misalnya, user hanya bisa mengakses/menjalankan fitur pada interface yang diberikan sebuah website tanpa menyentuh sistem internal/codingan dari website tersebut.

2. Kontrol Akses
Hanya method tertentu yang bisa mengubah atau mengambil sebuah data.
Di dalam sebuah sistem (website), setiap tombol/fitur yang muncul di UI sudah di-mapping ke method tertentu dibelakang layar.
Contoh:
* Tombol Login → menjalankan method login()
* Tombol Daftar → menjalankan method register()
* Tombol Tambahkan ke Keranjang → menjalankan method addToCart()
* Tidak mungkin tombol login menjalankan method addToCart() ataupun method lain karena sudah dibungkus (encapsulated) sesuai fungsi dan tujuan dari masing masing tombol pada UI.

3. Fleksibilitas
Implementasi internal bisa berubah tanpa memengaruhi kode lain yang menggunakan class tersebut.
Selama interface (public method) tidak berubah, kita bisa bebas mengubah sistem internal dalam class tanpa merusak bagian lain dalam program.
Dengan kata lain, user tetap akan menjalankan fitur dengan interface yang sama, walaupun cara kerja fiturnya dalam sistem internal sudah diubah.

5. Kerapian Kode
Pemisahan dengan jelas antara” apa yang bisa dipakai orang luar” (public) dengan “apa yang hanya bisa dipakai internal” (private)

B. Praktek Encapsulation
Bagaimana Penerapan Encapsulation di Javascript?
Dalam Javascript modern (EcmaScript 6+), Encapsulation dilakukan dengan acces modifier seperti:
* Private (#) → hanya diakses dalam class.
Syntax-nya ditulis dengan tanda # sebelum properties atau method yang ingin dibuat menjadi private.
* Public → diakses dimana saja.
Ditulis tanpa perlu syntax tambahan.

Studi Kasus: Sistem Login Sederhana dengan Class User
Kita akan membuat sebuah sistem login sederhana yang bisa memproses user login dan ganti password.

Langkah Pertama:
Kita perlu membuat sebuah class bernama User, class ini memiliki properties username (public) dan password (private) seperti berikut:
  Di dalam class user kita perlu membuat sebuah constructor sebagai tempat menyiapkan nilai awal dan aturan dasar sebuah object saat pertama kali dibuat. 
  Constructor berisi properti username untuk menyimpan nama user dan password untuk menyimpan password user, dan kita bisa meletakan parameter dalam constructor tersebut.
  ```
      class User {
        #password; // private → tidak bisa diakses dari luar
        constructor(username, password) {
          this.username = username;
          this.#password = password;
        }
```
Properti password kita buat tidak berada di dalam constructor karena ini merupakan sebuah private field. Dengan begitu sistem tau bahwa setiap object User memiliki private field yaitu #password. 
Sesuai dengan keamanan data yang dimaksud dalam konsep enkapsulasi, dimana password user tidak bisa diakses langsung dari luar class, karena disimpan dalam private field #password.

Langkah Kedua:
Lalu kita memerlukan 2 method untuk class User yaitu method untuk login dan method untuk mengganti password.
Berikut adalah syntax untuk method login:
Syntax berikut hanya memiliki tujuan untuk menjalankan proses login yang User lakukan:
        login(inputPassword) {
          if (inputPassword === this.#password) {
            return "Login berhasil!";
          } else {
            return "Password salah!";
          }
        }

Menggunakan if else untuk menentukan kondisi “jika input password memiliki kriteria yang sesuai dengan password di object instance, maka login berhasil”
dan “jika tidak, maka password dinyatakan salah”. Dan return untuk mengembalikan/menampilkan bahwa data yang diinput sesuai kondisi.

Selanjutnya adalah syntax untuk method ganti password:
        changePassword(oldPassword, newPassword) {
          if (oldPassword === this.#password) {
            this.#password = newPassword;
            return "Password berhasil diganti!";
          } else {
            return "Password lama salah!";
          }
        }
      }

Sesuai dengan konsep enkapsulasi dimana setiap fitur sudah memiliki method-nya masing-masing dalam sistem internal. Kalau tadi adalah method khusus untuk memproses login dari User.
Maka kita akan membuat method baru untuk memproses penggantian password milik user. Berisi 2 parameter yaitu password lama dan password baru. 
Diproses dengan condition if else “jika password lama sesuai maka akan langsung diganti dengan password baru” dan “jika password lama tidak sesuai maka tidak bisa ganti password baru”.

Langkah Ketiga:
Membuat instance object user1 untuk nantinya di-aktivasi apakah sistem yang kita buat dari class User berjalan dengan baik.
      const user1 = new User("Syahrul", "1234");
Sesuai dengan struktur class dan parameter dari constructor. User1 memiliki username bernama “Syahrul” dan password “1234”.


Langkah Keempat:
Kita akan mencoba menjalankan sistem login user ini.
1. User1 login menggunakan password yang benar.
  Jika kita menggunakan syntax di atas maka, sistem akan memproses bahwa User1 berhasil login dengan password yang sesuai milik instance object user1.
      console.log(user1.login("1234")); // ✅ Login berhasil!

2. User1 login menggunakan password yang salah.
  Dan jika user1 mencoba login dengan password yang berbeda maka, proses login akan gagal seperti berikut:
      console.log(user1.login("2345")); // ❌ Password salah!

3. User1 mengganti password.
  Disini user1 akan mengganti password lama dengan yang baru, karena password yang lama sesuai maka method berhasil diproses:
      console.log(user1.changePassword("1234", "abcd")); // ✅ Password berhasil diganti

4. User1 login kembali dengan password baru.
  User1 kembali login, tetapi menggunakan password baru dan berhasil karena password berhasil diganti sebelumnya.
      console.log(user1.login("abcd")); // ✅ Login berhasil!

Bagian user login dan mengganti password juga merupakan penerapan konsep enkapsulasi, dimana akses dan perubahan password hanya bisa dilakukan lewat method publik resmi.
Maksudnya, user tidak bisa menjalankan sistem yang tidak sesuai dengan yang ditampilkan pada interface atau fitur yang tidak dalam kondisi public method seperti fitur dalam private field contohnya.
Tidak hanya itu, fleksibilitas dan kerapian yang dimiliki kode di atas juga sudah sesuai dengan konsep enkapsulasi karena mudah untuk mengubah aturan baru dalam method semua data terangkum dalam class User.
