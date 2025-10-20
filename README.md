[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/Psgen4Dj)

# Ujian Praktikum Flutter POS SQLite
**Nama Mahasiswa:** Muhamad Abdul Ghofur

**NIM:** 362458302016

**Kelompok:** 1

## Deskripsi Fitur yang Ditambahkan
* Ubah navigasi utama menjadi BottomNavigationBar dengan 3 tab: Menu, Transaction, Report.
* 
## File yang Dimodifikasi
Tuliskan nama file dan deskripsi singkat:
* lib/screens/home/home_screen.dart -> saya ubah bagian NavigationBar itu diganti nama 3 menunya menjadi :
Menu, Transaction, Report. Lalu diubah List pages supaya tap Report itu mengarah ke halaman history
* lib/database/database_helper.dart -> menambahkan fungsi getTransactionsByTotalAmount(int totalAmount), 
sebenarnya saya copas dari fungsi getTransactions() cuman saya ubah kode query db.query menjadi
'select * from transactions where totalAmount > $totalAmount' supaya menampilkan transaksi dimana harga
totalnya lebih besar dari inputan harga total.
* lib/screens/transaction/transaction_history_screen.dart -> menambahkan floating button di tengah yang 
mana isinya inputan untuk menginput input filter total harga, saya referensikan dari file 
product_management_screen.dart untuk mengatur bagaimana inputan dan bagaimana ketika di klik floating
button itu memanggil fungsi getTransactionsByTotalAmount(int totalAmount). Lalu kan saya ubah jadi menggunakan 
Row didalamnya ada inputan dan FutureBuilder yang akan menampilkan list transaksi

## Cara Menjalankan Aplikasi
1. Jalankan ‘flutter pub get‘
2. Jalankan ‘flutter run‘
3. Uji fitur yang telah Anda tambahkan
   
## Screenshot
Lampirkan minimal 2 screenshot hasil implementasi fitur.

<img width="436" height="890" alt="image" src="https://github.com/user-attachments/assets/895e4526-b075-413b-86c9-22fe948cec18" />
<img width="1474" height="894" alt="image" src="https://github.com/user-attachments/assets/9ce806ed-0d15-4147-8031-b4b58dd7f4be" />

NB: saat saya pindah projeknya itu jadi error tidak keluar floating button yang sudah dibuat untuk filter
## Catatan Tambahan
Awalnya saya bingung dengan soalnya untuk membuat report, namun saya tanya pak sepyan dan diarahkan untuk
mengubah halaman history dengan menambahkan filter.

Kemudian saya melihat tutorial berikut : 
 - https://stackoverflow.com/questions/2309227/sqlite-select-with-condition-on-date
 - https://docs.flutter.dev/cookbook/forms/text-input
 - https://medium.com/@wartelski/flutter-3-floating-action-buttons-949be319df82

Lalu saya bingung saat menjalankan di HP teman tapi  error dengan versi gradle, namun saya mendapat tutorial dari
teman saya yang menggunakan CHATGPT untuk mengfiks kan error yang sama namun tapi tetap error.
