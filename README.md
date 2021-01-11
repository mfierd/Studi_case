# Studi_case
aplikasi studi kasus (File-nya ada di branch master)

## Scope & Fuctionalities
- user dapatmelihat daftar makanan yang ditawarkan
- user dapat memasukkan atau menghapus makanan yang terdapat pada keranjang
- user dapat melihat subtotal makanan yang terdapat pada keranjang
- user dapat melihat daftar voucher yang ditawarkan
- user dapat menggunakan salah satu voucher
- user dapat melihat harga total termasuk potongannya

### How Does it Works?
Project ini terdiri dari :
- tampilan aplikasinya. MainWindow.xaml.cs, Penawaran.xaml.cs, PilihVoucher.xaml.cs
- Model yang berisi item.cs, payment.cs, KeranjangBelanja.cs dan Voucher.cs
- Controller yang berisi MainWindoController.cs, PenawaranController.cs, VoucherController.cs

Controller berfungsi untuk memberikan beberapa operasi seperti menambahkan atau mengurangi item atau voucher yang dipilih dalam list

Untuk list item makanan yang ditawarkan terdapat pada Penawaran.xaml.cs
``` csharp
private void generateContentPenawaran()
        {
            Item coffeLate = new Item("Coffe Late", 30000);
            Item blackTea = new Item("BlackTea", 20000);
            Item pizza = new Item("Pizza", 75000);
            Item milkShake = new Item("Milk Shake", 15000);
            Item friedFrice = new Item("Fried Frice Special", 45000);
            Item watermelonJuice = new Item("Watermelon Juice", 25000);
            Item lemonSquash = new Item("Lemon Squash", 30000);


            Penawarancontroller.addItem(coffeLate);
            Penawarancontroller.addItem(blackTea);
            Penawarancontroller.addItem(pizza);
            Penawarancontroller.addItem(milkShake);
            Penawarancontroller.addItem(friedFrice);
            Penawarancontroller.addItem(watermelonJuice);
            Penawarancontroller.addItem(lemonSquash);            

            listPenawaran.Items.Refresh();
        }
```
Lalu pada MainWindow.xaml.cs terdapat inisialisasi payment dan keranjangbelanja untuk menampilkan penghitungan pembayaran nanti
``` csharp
public MainWindow()
        {
            InitializeComponent();

            payment = new Payment(this);

            KeranjangBelanja keranjangBelanja = new KeranjangBelanja(payment, this);

            controller = new MainWindowController(keranjangBelanja);

            listBoxPesanan.ItemsSource = controller.getSelectedItems();
            listBoxPakaiVoucher.ItemsSource = controller.getSelectedVouchers();

            initializeView();

        }
```
Dan PilihVoucher.xaml.cs berfungsi untuk menampilkan Voucher yang digunakan nanti pada listbox
``` csharp
private void generateListVoucher()
        {
            Model.Voucher awalTahun = new Model.Voucher(title: "Promo Awal Tahun Diskon 25%", discInPercent: 25);
            Model.Voucher tebusMurah = new Model.Voucher(title: "Promo Tebus Murah Diskon 30% atau max. 30.000", discInPercent: 30);
            Model.Voucher promoNatal = new Model.Voucher(title: "Promo Natal Potongan 10000", disc: 10000);

            voucherController.addItem(awalTahun);
            voucherController.addItem(tebusMurah);
            voucherController.addItem(promoNatal);

            DaftarVoucher.Items.Refresh();
        }
```
File didalam folder Model berfungsi untuk mendeskripsikan item, pembayaran dan voucher yang digunakan, khusunya payment.cs terdapat operasi untuk menghitung pembayaran.
File didalam folder Controller berfungsi untuk mengatur pemanggilan dari model agar lebih padat saat akan dipanggil di file MainWindow.xaml.cs, Penawaran.xaml.cs, PilihVoucher.xaml.cs
File MainWindow.xaml.cs menyediakan tampilan dari keranjangbelanja atau item yang telah dipilih.
File Penawaran.xaml.cs menyediakan tampilan list item-item yang ditawarkan.
File PilihVoucher.xaml.cs menyediakan tampilan list voucher yang tersedia.

19.11.2789
