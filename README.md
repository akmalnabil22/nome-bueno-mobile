# nome_bueno  
[Tugas 7](#tugas-7)

## Tugas 7  
1. Perbedaan stateless widget dan stateful widget  
    Stateless widget adalah widget yang bersifat statis atau tidak memiliki state yang bisa berubah setelah pertama kali di-build. StatelessWidget hanya merender tampilan yang sama setiap kali dipanggil, sehingga cocok untuk tampilan yang tidak akan berubah.  
    Stateful widget adalah Widget ini memiliki state yang bisa berubah selama aplikasi berjalan.  Saat ada perubahan state, widget akan di-render ulang untuk menampilkan perubahan tersebut. Cocok untuk UI yang dinamis atau interaktif, misalnya tombol yang berubah warna saat ditekan, kolom teks yang menampilkan input pengguna, atau elemen yang bergantung pada data dari jaringan.  

2. Widget yang digunakan pada project dan kegunaannya  
    `MyApp`: root dari semua widget di aplikasi  
    `MyHomePage`: Menampilkan halaman utama aplikasi  
    `InfoCard`:  Kartu informasi yang menampilkan title dan content.  

3. fungsi `setState()` dan variabel yang terdampak  
    Fungsi `setState()` di Flutter adalah metode yang digunakan dalam StatefulWidget untuk memberi tahu framework bahwa ada perubahan pada yang perlu diperbarui atau dirender ulang di layar. Ketika `setState()` dipanggil, Flutter akan menjalankan ulang fungsi `build()` dari widget tersebut dan menerapkan perubahan yang ada pada tampilan aplikasi.  
    Variabel yang bisa terdampak:  
    - Variabel yang Didefinisikan dalam Kelas State, contoh: `counter`, `isVisible`, atau `isLoading`
    - Properti yang Bergantung pada Input Pengguna, contoh: teks dalam `TextField`, pilihan dari `Dropdown`, atau status dari `Checkbox` 
    - Variabel Tipe Data Koleksi, contoh: List, Map, dan Set

4. Perbedaan `const` dan `final`  
    Nilai `const` diinisialisasi pada waktu kompilasi. Biasanya digunakan untuk nilai yang sepenuhnya statis. `const` dapat digunakan sebagai konstanta dalam ekspresi.  
    Nilai `final` diinisialisasi saat runtime, bukan pada waktu kompilasi. Cocok digunakan ketika nilai hanya perlu ditetapkan sekali pada saat runtime, terutama ketika nilai tergantung pada hasil perhitungan atau data dari sumber eksternal. `final` memberikan fleksibilitas karena nilainya dapat bergantung pada kondisi runtime.  

5. Implementasi checklist  
    - Membuat program Flutter  
        Pada direktori tempat kita ingin menyimpan project Flutter, jalankan `flutter create nome_bueno` pada terminal  
    
    - Membuat tiga tombol (`Lihat Produk`, `Tambah Produk`, `Logout`)  
        Buat class untuk menyimpan atribut tombol (Nama dan Icon)
        ```dart
        class ItemHomepage {
            final String name;
            final IconData icon;

            ItemHomepage(this.name, this.icon);
        }
        ```
        Pada Widget MyHomePage, inisiasi tombol
        ```dart
        final List<ItemHomepage> items = [
            ItemHomepage("Lihat Produk", Icons.all_inbox, Colors.orange.shade800),
            ItemHomepage("Tambah Produk", Icons.add, Colors.lightGreen.shade800),
            ItemHomepage("Logout", Icons.logout, Colors.deepOrange.shade800),
        ];
        ```
        Buat widget ItemCard untuk menampilkan tombol
        ```dart
        class ItemCard extends StatelessWidget {
            // Menampilkan kartu dengan ikon dan nama.

            final ItemHomepage item; 
            
            const ItemCard(this.item, {super.key}); 

            @override
            Widget build(BuildContext context) {
                return Material(
                // Menentukan warna latar belakang dari tema aplikasi.
                color: Theme.of(context).colorScheme.secondary,
                // Membuat sudut kartu melengkung.
                borderRadius: BorderRadius.circular(12),
                
                child: InkWell(
                    // Container untuk menyimpan Icon dan Text
                    child: Container(
                    padding: const EdgeInsets.all(8),
                    child: Center(
                        child: Column(
                        // Menyusun ikon dan teks di tengah kartu.
                        mainAxisAlignment: MainAxisAlignment.center,
                        children: [
                            Icon(
                            item.icon,
                            color: Colors.white,
                            size: 30.0,
                            ),
                            const Padding(padding: EdgeInsets.all(3)),
                            Text(
                            item.name,
                            textAlign: TextAlign.center,
                            style: const TextStyle(color: Colors.white),
                            ),
                        ],
                        ),
                    ),
                    ),
                ),
                );
            }
        }
        ```
        Tampilkan tombol di MyHomePage
        ```dart
        class MyHomePage extends StatelessWidget {
            ...
            Widget build(BuildContext context) {
                // Scaffold menyediakan struktur dasar halaman dengan AppBar dan body.
                return Scaffold(
                // Body halaman dengan padding di sekelilingnya.
                body: Padding(
                    padding: const EdgeInsets.all(16.0),
                    // Menyusun widget secara vertikal dalam sebuah kolom.
                    child: Column(
                    crossAxisAlignment: CrossAxisAlignment.center,
                    children: [
                        ...
                        // Menempatkan widget berikutnya di tengah halaman.
                        Center(
                        child: Column(
                            // Menyusun teks dan grid item secara vertikal.
                            children: [
                            ...
                            // Grid untuk menampilkan ItemCard dalam bentuk grid 3 kolom.
                            GridView.count(
                                primary: true,
                                padding: const EdgeInsets.all(20),
                                crossAxisSpacing: 10,
                                mainAxisSpacing: 10,
                                crossAxisCount: 3,
                                // Agar grid menyesuaikan tinggi kontennya.
                                shrinkWrap: true,

                                // Menampilkan ItemCard untuk setiap item dalam list items.
                                children: items.map((ItemHomepage item) {
                                return ItemCard(item);
                                }).toList(),
                            ),
                            ],
                        ),
                        ),
                    ],
                    ),
                ),
                );
            }
        }
        ```
    - Menampilkan warna berbeda untuk setiap tombol  
        Tambahkan atribut color pada ItemHomepage
        ```dart
        class ItemHomepage {
            final String name;
            final IconData icon;
            final Color color;

            ItemHomepage(this.name, this.icon, this.color);
        }
        ```
        Inisiasi tombol dengan warna berbeda
        ```dart
        final List<ItemHomepage> items = [
            ItemHomepage("Lihat Produk", Icons.all_inbox, Colors.orange.shade800),
            ItemHomepage("Tambah Produk", Icons.add, Colors.lightGreen.shade800),
            ItemHomepage("Logout", Icons.logout, Colors.deepOrange.shade800),
        ];
        ```
        Pada widget ItemCard, ubah color yang dipakai
        ```dart
        class ItemCard extends StatelessWidget {
            ...

            @override
            Widget build(BuildContext context) {
                return Material(
                // Menentukan warna latar belakang dari tema aplikasi.
                color: Item.color,
                ...
                );
            }
        }
    - Memunculkan Snackbar ketika tombol ditekan  
        Pada widget ItemCard, tambahkan
        ```dart
        child: InkWell(
            // Aksi ketika kartu ditekan.
            onTap: () {
            // Menampilkan pesan SnackBar saat kartu ditekan.
            ScaffoldMessenger.of(context)
                ..hideCurrentSnackBar()
                ..showSnackBar(
                SnackBar(content: Text("Kamu telah menekan tombol ${item.name}!"))
                );
            },            
        ),
        ```
