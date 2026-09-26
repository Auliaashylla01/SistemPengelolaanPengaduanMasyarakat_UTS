# Sistem Pengelolaan Pengaduan Masyarakat

**Oleh Aulia Ashylla Ananda Putri Hariawan (2509116076)**

## 1. Deskripsi Singkat Program

Sistem Pengelolaan Pengaduan Masyarakat merupakan program yang digunakan untuk mencatat dan mengelola data pengaduan yang disampaikan oleh masyarakat. Program ini dapat digunakan untuk menangani berbagai jenis laporan, seperti fasilitas umum, kebersihan, keamanan, jalan, dan pelayanan. Setiap data pengaduan memiliki informasi berupa ID Pengaduan, Nama Pelapor, Jenis Pengaduan, Isi Pengaduan, Tanggal Pengaduan, Tingkat Urgensi, dan Status Pengaduan. ID pengaduan dibuat secara otomatis oleh sistem dengan format `P001`, `P002`, dan seterusnya. Jenis pengaduan dipilih melalui kategori yang telah disediakan sehingga data yang dimasukkan lebih terstruktur.

Program membedakan pengaduan menjadi dua jenis berdasarkan tingkat urgensinya, yaitu **pengaduan biasa** dan **pengaduan darurat**. Pengaduan biasa memiliki target penyelesaian standar 7 hari, sedangkan pengaduan darurat memiliki target respons awal standar 24 jam dan menyimpan kontak darurat pelapor. Pengguna dapat menjalankan beberapa fitur utama melalui menu interaktif, yaitu Tambah Pengaduan, Lihat Pengaduan, Ubah Status Pengaduan, Hapus Pengaduan, dan Keluar. Data selama program berjalan disimpan menggunakan `ArrayList`.

---

## 2. Tujuan Program

Program ini dibuat sebagai penerapan konsep Pemrograman Berorientasi Objek melalui sebuah sistem pengelolaan pengaduan sederhana.

Tujuan program adalah:

* Mencatat data pengaduan masyarakat secara terstruktur.
* Mengelompokkan pengaduan berdasarkan jenis dan tingkat urgensi.
* Menampilkan data pengaduan yang tersimpan.
* Mengubah status pengaduan berdasarkan tahapan penanganan.
* Menghapus data pengaduan berdasarkan ID.

---

## 3. Struktur Program

Program terdiri dari beberapa class yang dikelompokkan berdasarkan fungsinya.

| Package      | Class                           | Peran                                                                                                                          |
| ------------ | ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `main`       | `PengelolaanPengaduanMasyarakt` | Menjadi *entry point* program dan mengatur alur utama menu serta proses input pengguna.                                        |
| `main`       | `ValidasiInput`                 | Menangani validasi berbagai input pengguna agar data sesuai aturan yang ditentukan.                                            |
| `controller` | `PengelolaDataPengaduan`        | Mengelola data pengaduan dalam `ArrayList`, menjalankan proses tambah, cari, ubah status, hapus, dan menghasilkan ID otomatis. |
| `model`      | `Pengaduan`                     | Menjadi superclass yang menyimpan atribut dan data umum dari sebuah pengaduan.                                             |
| `model`      | `pengaduanBiasa`                | Subclass dari `Pengaduan` untuk data pengaduan dengan tingkat urgensi biasa.                                                        |
| `model`      | `pengaduanDarurat`              | Subclass dari `Pengaduan` untuk data pengaduan dengan tingkat urgensi darurat.                                                      |
| `view`       | `PengaduanView`                 | Mengatur tampilan program pada terminal, seperti menu, judul, pilihan, informasi, pesan sukses, dan pesan error.               |

### Struktur package

```text
src/
└── main/
    └── java/
        ├── main/
        │   ├── PengelolaanPengaduanMasyarakt.java
        │   └── ValidasiInput.java
        │
        ├── controller/
        │   └── PengelolaDataPengaduan.java
        │
        ├── model/
        │   ├── Pengaduan.java
        │   ├── pengaduanBiasa.java
        │   └── pengaduanDarurat.java
        │
        └── view/
            └── PengaduanView.java
```

---

## 4. Menu Program

Menu utama yang tersedia pada sistem adalah:

<img width="280" height="119" alt="image" src="https://github.com/user-attachments/assets/f8c819d5-7c75-4229-99bd-28b323aa2432" />                    

*Gambar 1: Tampilan menu utama Sistem Pengelolaan Pengaduan Masyarakat sebagai pusat navigasi seluruh fitur program.*

Menu tersebut digunakan sebagai pusat navigasi program. Setelah pengguna menyelesaikan suatu proses, program akan kembali ke menu utama selama pengguna belum memilih menu Keluar.


---

# 5. Alur Program

## 5.1 Alur Sistem

Secara umum, sistem dimulai dengan menyediakan data awal pada `ArrayList`, kemudian pengguna dapat memilih fitur yang tersedia melalui menu utama. Alur sistem tersebut menunjukkan bahwa setiap fitur bekerja melalui menu utama dan setelah proses selesai pengguna kembali ke menu. Program akan berhenti ketika pilihan menu bernilai `5`.

```text
                          ┌──────────────┐
                          │    MULAI     │
                          └──────┬───────┘
                                 │
                                 ▼
                      Inisialisasi Controller
                                 │
                                 ▼
                       Muat Dummy Data Awal
                                 │
           ┌─────────────────────┴─────────────────────┐
           │                                           │
           ▼                                           │
┌────────────────────┐                                 │
│   Tampilkan Menu   │◄────────────────────────────┐   │
└─────────┬──────────┘                             │   │
          │                                        │   │
          ▼                                        │   │
┌────────────────────┐                             │   │
│   Input Pilihan    │                             │   │
│        Menu        │                             │   │
└─────────┬──────────┘                             │   │
          │                                        │   │
          ▼                                        │   │
  ┌───────────────┐                                │   │
  │ Pilihan Menu? │                                │   │
  └───────┬───────┘                                │   │
          │                                        │   │
  ┌───────┼─────────────┬──────────────┬───────────┤   │
  │       │             │              │           │   │
  ▼       ▼             ▼              ▼           ▼   │
 [1]     [2]           [3]            [4]         [5]  │
Tambah  Lihat          Ubah          Hapus       Keluar│
  │       │             │              │           │   │
  ▼       ▼             ▼              ▼           ▼   │
Proses  Proses        Proses        Proses      Selesai│
  │       │             │              │               │
  └───────┴──────┬──────┴──────────────┘               │
                 │                                     │
                 ▼                                     │
          Kembali ke Menu ─────────────────────────────┘
```

---

## 5.2 Alur Tambah Pengaduan

Fitur **Tambah Pengaduan** digunakan untuk membuat data pengaduan baru.

Urutan prosesnya adalah:

```text
Pilih Menu Tambah Pengaduan
                         │
                         ▼
                Generate ID Otomatis
                         │
                         ▼
                Input Nama Pelapor
                         │
                         ▼
              Pilih Jenis Pengaduan
                         │
                         ▼
                 Input Isi Pengaduan
                         │
                         ▼
               Input Tanggal Pengaduan
                         │
                         ▼
               Pilih Tingkat Urgensi?
                  ┌──────┴──────┐
                  │             │
                  ▼             ▼
                Biasa        Darurat
                  │             │
                  ▼             ▼
             Buat Object   Input Kontak
           pengaduanBiasa    Darurat
                  │             │
                  │             ▼
                  │        Buat Object
                  │      pengaduanDarurat
                  │             │
                  └──────┬──────┘
                         │
                         ▼
                Simpan ke ArrayList
                         │
                         ▼
                Tampilkan Berhasil
                         │
                         ▼
                 Kembali ke Menu
```

ID tidak dimasukkan secara manual oleh pengguna. Sistem menghasilkan ID berdasarkan ID yang belum digunakan, misalnya `P001`, `P002`, dan seterusnya.

Jenis pengaduan juga tidak dimasukkan sebagai teks bebas. Pengguna memilih salah satu dari lima kategori yang disediakan, yaitu:

```text
1. Fasilitas Umum
2. Kebersihan
3. Keamanan
4. Jalan
5. Pelayanan
```

Pada tahap berikutnya pengguna memilih tingkat urgensi:

```text
1. Biasa
2. Darurat
```

Pilihan tersebut menentukan object subclass yang dibuat. Pengaduan biasa akan menghasilkan object `pengaduanBiasa`, sedangkan pengaduan darurat akan menghasilkan object `pengaduanDarurat`.

### Bukti output proses tambah pengaduan biasa

<img width="334" height="298" alt="image" src="https://github.com/user-attachments/assets/dfbd73e3-e3bb-42e5-a5b6-16b4828c6dbb" />                      

*Gambar 2: Proses penambahan pengaduan biasa, mulai dari ID otomatis, pengisian data pengaduan, pemilihan jenis dan urgensi, hingga data berhasil disimpan.*                 

### Bukti output proses tambah pengaduan darurat            

<img width="374" height="306" alt="image" src="https://github.com/user-attachments/assets/2dbff5be-98f0-43bc-88fe-7545cee8f4b1" />        

*Gambar 3: Proses penambahan pengaduan darurat yang menghasilkan object `pengaduanDarurat` dan meminta input kontak darurat pelapor.*          

---

## 5.3 Alur Lihat Pengaduan

Fitur **Lihat Pengaduan** digunakan untuk menampilkan seluruh data yang tersimpan pada `ArrayList`.


<img width="464" height="283" alt="image" src="https://github.com/user-attachments/assets/05dbb5a0-5465-4e98-bd92-143d5d8dfaa0" />                        

*Gambar 4: Tampilan data pengaduan pada fitur Lihat Pengaduan, termasuk data dummy yang telah tersedia sejak program dijalankan.*   

Data dummy telah dimasukkan sejak `PengelolaDataPengaduan` dibuat. Oleh karena itu, ketika program pertama kali menjalankan menu Lihat Pengaduan, data sudah langsung tersedia tanpa harus melakukan proses tambah terlebih dahulu.                    

```text
Pilih Menu Lihat Pengaduan
          ↓
Controller mengambil ArrayList
          ↓
View menerima daftar pengaduan
          ↓
Perulangan menampilkan setiap object
          ↓
Method getDetailPengaduan()
          ↓
Data tampil pada terminal
```
---

## 5.4 Alur Ubah Status Pengaduan

Fitur **Ubah Status Pengaduan** menggunakan alur status bertahap agar perubahan status tidak dapat dilakukan secara acak.

<img width="377" height="242" alt="image" src="https://github.com/user-attachments/assets/bac2cd7f-d218-4dde-9450-e6c6bf2493e8" />                

*Gambar 5: Proses perubahan status pengaduan berdasarkan ID dengan konfirmasi pengguna sebelum status diperbarui.*        

Urutan status adalah:

```text
Menunggu Konfirmasi Petugas
             ↓
       Sedang Diproses
             ↓
   Selesai Ditindaklanjuti
```

Pengguna memasukkan ID pengaduan yang akan diubah. Sistem kemudian mencari data berdasarkan ID tersebut. Setelah data ditemukan, sistem menentukan status berikutnya berdasarkan status saat ini.

Apabila pengaduan sudah berada pada status `Selesai Ditindaklanjuti`, status tidak dapat diubah lagi.

```text
Pilih Ubah Status
                      │
                      ▼
           ┌► Input ID Pengaduan ◄────────────────┐
           │          │                           │
           │          ▼                           │
           │ Cari Data berdasarkan ID             │
           │          │                           │
           │          ▼                           │
           │   Data ditemukan?                    │
           │     ┌────┴────┐                      │
           │   Tidak       Ya                     │
           │     │          │                     │
           │     ▼          ▼                     │
           └── Error  Cek Status Saat Ini         │
                            │                     │
                            ▼                     │
                 Tentukan Status Berikutnya       │
                            │                     │
                            ▼                     │
                 Konfirmasi perubahan?            │
                     ┌──────┴──────┐              │
                     │             │              │
                     ▼             ▼              │
                    'y'           'n'             │
                     │             │              │
                     ▼             ▼              │
                Ubah Status      Batal            │
                     │             │              │
                     └──────┬──────┘              │
                            │                     │
                            ▼                     │
                     Kembali ke Menu ─────────────┘
```

---

## 5.5 Alur Hapus Pengaduan

Fitur **Hapus Pengaduan** digunakan untuk menghapus data berdasarkan ID.

<img width="328" height="239" alt="image" src="https://github.com/user-attachments/assets/11717486-9d2c-4af5-b98a-645641ac31d8" />            

*Gambar 6: Proses penghapusan data pengaduan melalui pencarian ID dan konfirmasi pengguna sebelum data dihapus.*


Sebelum data benar-benar dihapus, sistem menampilkan ringkasan data dan meminta konfirmasi. Hal tersebut mencegah penghapusan dilakukan secara langsung tanpa persetujuan pengguna.


```text
Pilih Hapus Pengaduan
                         │
                         ▼
           ┌► Input ID Pengaduan
           │             │
           │             ▼
           │       Cari Pengaduan
           │             │
           │             ▼
           │      Data ditemukan?
           │        ┌────┴────┐
           │      Tidak      Ya
           │        │         │
           │        ▼         ▼
           └─── Error    Tampilkan Ringkasan Data
                              │
                              ▼
                     Konfirmasi (y/n)?
                        ┌─────┴─────┐
                        │           │
                        ▼           ▼
                       'y'         'n'
                        │           │
                        ▼           ▼
                      Hapus       Batal
                        │           │
                        └─────┬─────┘
                              │
                              ▼
                       Kembali ke Menu
```

---

## 5.6 Alur Keluar Program

Ketika pengguna memilih menu `5`, program menampilkan pesan penutup dan mengakhiri perulangan menu.

<img width="380" height="170" alt="image" src="https://github.com/user-attachments/assets/e3a15630-7d23-4331-92f8-e794194d1c5a" />                    

*Gambar 7: Tampilan ketika pengguna memilih menu Keluar dan program mengakhiri proses.*

---

# 6. Penerapan Ketentuan OOP

## 6.1. Access Modifier

Access modifier digunakan untuk mengatur hak akses terhadap atribut dan method di dalam class.

Pada class `Pengaduan`, seluruh atribut utama menggunakan `private`:

<img width="503" height="120" alt="image" src="https://github.com/user-attachments/assets/b669957c-23b5-4e6c-960b-8462c1d6283d" />                

*Gambar 8: Penerapan access modifier `private` pada atribut class `Pengaduan` untuk membatasi akses langsung terhadap data pengaduan.*            

Atribut tersebut tidak dapat diakses secara langsung dari class lain. Akses terhadap data dilakukan melalui method yang telah disediakan.            

---

## 6.2. Encapsulation

**Encapsulation** diterapkan dengan menyembunyikan data internal object melalui atribut `private` dan menyediakan method `getter` serta `setter` sesuai kebutuhan.

Contoh penerapannya pada class `Pengaduan`:

<img width="526" height="143" alt="image" src="https://github.com/user-attachments/assets/c8f08e32-85c0-4df3-a6bc-b0eb24199b00" />                            

*Gambar 9: Penerapan encapsulation melalui method `getter` dan `setter` pada class `Pengaduan`.* 

Atribut `idPengaduan` tidak memiliki `setter`. Hal tersebut dilakukan karena ID dibuat secara otomatis oleh sistem dan digunakan sebagai identitas pengaduan sehingga tidak diubah melalui setter. Dengan demikian, data tidak diberikan akses langsung dari luar class, tetapi melalui method yang disediakan oleh class tersebut.                

---

## 6.3. Inheritance

**Inheritance** digunakan dengan membuat class `Pengaduan` sebagai superclass yang memiliki atribut dan method umum untuk seluruh jenis pengaduan.

Dua subclass mewarisi class tersebut:                        

<img width="650" height="205" alt="Screenshot 2026-09-24 102039" src="https://github.com/user-attachments/assets/07d38eb8-0684-4561-987b-2c377e467402" />                
      
*Gambar 10: Penerapan inheritance pada class `pengaduanBiasa` melalui keyword `extends` dan penggunaan `super()` untuk memanggil constructor superclass `Pengaduan`.*

<img width="449" height="62" alt="image" src="https://github.com/user-attachments/assets/8d4f92c8-39de-4783-9c28-5402edc97443" />            

*Gambar 11: Penerapan inheritance pada class `pengaduanDarurat` sebagai subclass kedua dari superclass `Pengaduan`.*

Pada constructor subclass digunakan `super()` untuk menginisialisasi atribut yang berasal dari superclass.                    
Contoh:                        

<img width="556" height="115" alt="image" src="https://github.com/user-attachments/assets/cbf53c77-af77-4ed7-bdb3-b739e0842dae" />            

*Gambar 12: Inisialisasi `super()` pada subclass*                

Dengan inheritance, atribut dan perilaku umum tidak perlu ditulis kembali pada masing-masing subclass.

---

## 6.4. Polymorphism - Method Overriding

Polymorphism diterapkan melalui method overriding pada kedua subclass.

Class Pengaduan memiliki method:

<img width="650" height="205" alt="Screenshot 2026-09-24 102039" src="https://github.com/user-attachments/assets/c4f59f75-82a1-4cc1-aac7-d78343b801fb" />                
  

*Gambar 13: Penerapan polymorphism melalui method overriding pada subclass `pengaduanBiasa` dan `pengaduanDarurat` dengan mengimplementasikan kembali method dari superclass `Pengaduan`.*

Method tersebut kemudian dioverride pada class `pengaduanBiasa` dan `pengaduanDarurat`.

Pada `pengaduanBiasa`:

<img width="712" height="176" alt="Screenshot 2026-09-24 105335" src="https://github.com/user-attachments/assets/7f64d18a-670a-4fb3-91ab-e40b683cf380" />  

*Gambar 14: Penerapan method overriding pada `getTingkatUrgensi()` di subclass untuk menghasilkan tingkat urgensi sesuai jenis pengaduan.*

Sedangkan pada `pengaduanDarurat`:

<img width="791" height="179" alt="Screenshot 2026-09-24 102822" src="https://github.com/user-attachments/assets/1b9a259c-597e-4eaa-bda6-00d28f1e343f" />  

*Gambar 15: Penerapan method overriding pada `getTingkatUrgensi()` di subclass untuk menghasilkan tingkat urgensi sesuai jenis pengaduan.*

Method `getDetailPengaduan()` juga dioverride pada kedua subclass untuk menampilkan informasi tambahan sesuai dengan jenis pengaduannya.

Penerapan ini membuat method yang sama dapat menghasilkan perilaku yang berbeda sesuai object yang digunakan.

---

## 6.5. Polymorphism - Method Overloading

Selain overriding, program juga menerapkan polymorphism melalui method overloading pada constructor class `Pengaduan`.

Constructor pertama digunakan untuk membuat object dengan data utama pengaduan:

<img width="643" height="197" alt="image" src="https://github.com/user-attachments/assets/ca0496cf-e048-47fd-abfa-18de6603bd41" />    

*Gambar 16: Penerapan polymorphism melalui constructor overloading pada class `Pengaduan`, yang memiliki dua constructor dengan jumlah parameter berbeda.*

Constructor kedua memiliki parameter tambahan berupa `status`:

<img width="500" height="145" alt="image" src="https://github.com/user-attachments/assets/3a954197-41ab-46d4-adb9-c27425b38090" />         

*Gambar 16: Penerapan polymorphism melalui constructor overloading pada class `Pengaduan`, yang memiliki dua constructor dengan jumlah parameter berbeda.*

Kedua constructor memiliki nama yang sama, yaitu Pengaduan, tetapi memiliki jumlah parameter yang berbeda. Hal tersebut merupakan method overloading karena Java dapat menentukan constructor yang digunakan berdasarkan parameter yang diberikan saat object dibuat.     

---

## 6.6. Condition

Condition digunakan untuk menentukan proses yang dijalankan berdasarkan kondisi tertentu. Program menggunakan percabangan if, if-else, serta switch pada beberapa bagian sistem.

Salah satu penerapannya terdapat pada class `ValidasiInput` bagian validasi input menu:

<img width="501" height="232" alt="image" src="https://github.com/user-attachments/assets/3fe7b6b4-62e0-4742-8a31-395f302afeee" />     

*Gambar 17: Penerapan condition menggunakan if untuk menentukan proses berdasarkan kondisi status pengaduan.*

Percabangan tersebut digunakan untuk memastikan input menu berupa angka dan pilihan menu 1-5. Selain if, program menggunakan switch untuk menangani pilihan menu dan kategori pengaduan.

---


## 6.7. Looping

Looping digunakan agar proses tertentu dapat dilakukan berulang kali selama kondisi yang ditentukan masih terpenuhi.

Pada menu utama, program menggunakan do-while:

<img width="547" height="331" alt="image" src="https://github.com/user-attachments/assets/ed00c9bb-0c7d-4e71-91d2-7079bb100614" />       

*Gambar 18: Penerapan looping pada program untuk mengulang menu atau proses input sampai kondisi tertentu terpenuhi.*

Perulangan tersebut membuat menu utama terus ditampilkan setelah pengguna menyelesaikan suatu proses. Program hanya berhenti ketika pengguna memilih menu 5. Keluar.

Program juga menggunakan while pada proses validasi input. Jika input yang diberikan tidak sesuai aturan, pengguna akan diminta memasukkan kembali data sampai input valid.

Selain itu, for digunakan ketika program menampilkan data pengaduan yang tersimpan dalam ArrayList, sehingga setiap object pengaduan dapat ditampilkan secara berurutan.
