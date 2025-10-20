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
<img width="474" height="894" alt="image" src="https://github.com/user-attachments/assets/77514e33-20c7-4c5a-8a33-d346a8a1a16f" />

NB: saat saya pindah projeknya itu jadi error tidak keluar floating button yang sudah dibuat untuk filter terus saya tanya ke AI 
dengan prompt `error "Another exception was thrown: RenderBox was not laid out: RenderAnimatedOpacity#75831 NEEDS-LAYOUT NEEDS-PAINT" di code "import 'package:flutter/material.dart';
import 'package:intl/intl.dart';
import 'package:pos_app/database/database_helper.dart';
import 'package:pos_app/models/transaction_model.dart';

class TransactionHistoryScreen extends StatefulWidget {
  const TransactionHistoryScreen({super.key});

  @override
  State<TransactionHistoryScreen> createState() =>
      _TransactionHistoryScreenState();
}

class _TransactionHistoryScreenState extends State<TransactionHistoryScreen> {
  late Future<List<Transaction>> _transactionsFuture;

  @override
  void initState() {
    super.initState();
    _transactionsFuture = DatabaseHelper.instance.getTransactions();
  }

  void _showTransactionDetails(Transaction transaction) async {
    final details =
        await DatabaseHelper.instance.getTransactionDetails(transaction.id!);
    showDialog(
      context: context,
      builder: (context) => AlertDialog(
        title: Text('Detail Transaksi #${transaction.id}'),
        content: SizedBox(
          width: double.maxFinite,
          child: ListView.builder(
            shrinkWrap: true,
            itemCount: details.length,
            itemBuilder: (context, index) {
              final detail = details[index];
              return ListTile(
                title: Text(detail.productName),
                subtitle: Text(
                    '${detail.quantity} x Rp. ${detail.priceAtTransaction}'),
                trailing:
                    Text('Rp. ${detail.quantity * detail.priceAtTransaction}'),
              );
            },
          ),
        ),
        actions: [
          TextButton(
              onPressed: () => Navigator.pop(context),
              child: const Text('Tutup')),
        ],
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    final inputTotalAmountController = TextEditingController();

    return Scaffold(
      appBar: AppBar(title: const Text('Riwayat Transaksi')),
      body: Row(
        children: [
          TextField(
            controller: inputTotalAmountController,
            decoration: const InputDecoration(
              hintText: "Masukkan harga transaksi",
            ),
          ),
          FutureBuilder<List<Transaction>>(
            future: _transactionsFuture,
            builder: (context, snapshot) {
              if (snapshot.connectionState == ConnectionState.waiting) {
                return const Center(child: CircularProgressIndicator());
              }
              if (!snapshot.hasData || snapshot.data!.isEmpty) {
                return const Center(
                    child: Text('Tidak ada riwayat transaksi.'));
              }
              final transactions = snapshot.data!;
              return ListView.builder(
                itemCount: transactions.length,
                itemBuilder: (context, index) {
                  final transaction = transactions[index];
                  return Card(
                    margin:
                        const EdgeInsets.symmetric(horizontal: 16, vertical: 8),
                    child: ListTile(
                      title: Text('Transaksi #${transaction.id}'),
                      subtitle: Text(DateFormat('dd MMMM yyyy, HH:mm')
                          .format(transaction.transactionDate)),
                      trailing: Text('Rp. ${transaction.totalAmount}',
                          style: const TextStyle(fontWeight: FontWeight.bold)),
                      onTap: () => _showTransactionDetails(transaction),
                    ),
                  );
                },
              );
            },
          ),
        ],
      ),
      floatingActionButtonLocation: FloatingActionButtonLocation.centerFloat,
      floatingActionButton: FloatingActionButton.extended(
          onPressed: () {
            final totalAmount = inputTotalAmountController.text;
            final amount = int.parse(totalAmount);
            _transactionsFuture =
                DatabaseHelper.instance.getTransactionsByTotalAmount(amount);
          },
          label: const Icon(Icons.filter_alt)),
    );
  }
}
"` katanya sih mengganti Row menjadi Column dengan karena Row akan memberikan ukuran tak terbatas
sedangkan TextField dan FutureBuilder memakan ruang sebebasnya karena di bungkus didalam Row sehingga
menghasilkan error. 
## Catatan Tambahan
Awalnya saya bingung dengan soalnya untuk membuat report, namun saya tanya pak sepyan dan diarahkan untuk
mengubah halaman history dengan menambahkan filter.

Kemudian saya melihat tutorial berikut : 
 - https://stackoverflow.com/questions/2309227/sqlite-select-with-condition-on-date
 - https://docs.flutter.dev/cookbook/forms/text-input
 - https://medium.com/@wartelski/flutter-3-floating-action-buttons-949be319df82

Lalu saya bingung saat menjalankan di HP teman tapi  error dengan versi gradle, namun saya mendapat tutorial dari
teman saya yang menggunakan CHATGPT untuk mengfiks kan error yang sama namun tapi tetap error. Pada akhirnya ga jadi sih.
