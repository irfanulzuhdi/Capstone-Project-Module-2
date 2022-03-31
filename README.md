# CAPSTONE PROJECT MODULE 2 (IRFANUL ZUHDI.N)

# **DATA UNDERSTANDING**


### **Introduction :**
Database Northwind berisi data penjualan perusahaan fiktif bernama Northwind Traders. Fokus perusahaan dalam bidang mengimpor dan mengekspor beberapa makanan dan minuman khusus dari seluruh dunia. Perusahan fiktif ini melakukan penjualan makanan dan minuman khusus tersebut secara grosir ke gerai seluruh dunia. Basis data ini terdapat 2155 transaksi yang terjadi dengan 89 pelanggan berbeda selama 23 bulan, lengkap dengan informasi mengenai customer, product, detail order, employee, region, shipper, supplier, territories, dan categorie product. Dalam analisis kali ini, berfokus pada produk yang sudah melewati proses transaksi selama 23 bulan (1996 - 1998) pada perusahaan Northwind. Analisis ini bertujuan untuk mengolah data yang ada sehingga menghasilkan suatu informasi penting yang dapat meningkatkan produktivitas perusahaan dan penerapan strategi yang tepat sasaran dalam melakukan transaksi sehingga memperoleh keuntungan yang lebih lagi.

### **Database Information :**

Database yang dimiliki mempunyai 11 tabel, yaitu:
- Categories          : Menyimpan informasi tentang kategori produk
- Customers           : Menyimpan informasi tentang data pelanggan/customer
- Products            : Menyimpan informasi tentang jenis produk
- Orders              : Menyimpan informasi jual-beli yang dilakukan oleh customer
- Orderdetails        : Menyimpan informasi lebih detail terkait order yang dilakukan oleh customer
- Employees           : Menyimpan informasi tentang karyawan serta struktur organisasi dan jabatan setiap karyawan
- Employeeterritories : Menyimpan informasi tentang territoryID dari karyawan
- Region              : Menyimpan informasi tentang region
- Shippers            : Menyimpan informasi tentang shippers yang digunakan oleh perusahaan
- Suppliers           : Menyimpan informasi tentang supplier perusahaan
- Territories         : Menyimpan informasi tentang wilayah disetiap region

### **Question :**

1. Tampilkan total sale amount dan total quantity berdasarkan kategori produk! serta jabarkan insight yang didapatkan dari grafik tersebut.
3. Tampilkan 10 produk yang paling banyak dipesan (berdasarkan quantity) oleh customer!
4. Tampilkan urutan kategori produk dari yang paling banyak dipesan (berdasarkan quantity) oleh customer!
5. Tampilkan grafik serta jelaskan Total sales per tahun!
6. Pada bulan dan tahun ke berapa keuntungan terbesar yang didapatkan oleh perusahaan Northwind?
7. Tampilkan Top 10 customer yang melakukan pembelian terbanyak selama 23 bulan!
8. Tampilkan dalam bentuk peta dunia (Map) penyebaran customer perusahaan serta total saleamount dan total quantity-nya!
9. Berapa banyak pesanan yang mengalami keterlambatan atau kendala? dan Tampilkan jumlah pesanan berdasarkan hari keterlambatannya!
10. Berapa banyak produk yang memiliki harga per unit diatas rata-rata harga per unit produk?
11. Tampilkan produk apa saja yang sudah tidak lagi dijual? dan berapa sisa total produk tersebut dalam stok?
12. Tampilkan 10 produk termahal yang dijual oleh perusahaan?
13. Tampilkan stok dari produk terlaris yang tersedia saat ini (Unit in Stock best selling product)?

***
## **SQL**

**Question:**

1. Apakah tabel products, orders, orderdetails, categories, dan customers dapat digabungkan menjadi 1 tabel? Jika dapat digabungkan, tampilkan tabel yang memuat informasi terkait penjualan produk, total sale amount setiap order, customer yang membeli produk, dan sebagainya yang melibatkan kelima tabel tersebut.
2. Apakah dapat menampilkan kolom baru yang merupakan Sale amount yang didapatkan dari perkalian antara harga per unit dan quantity setiap order yang dilakukan oleh customer?
3. Buatlah tabel yang berisikan total jenis produk yang di order, total quantity setiap produk yang diorder, total ketersedian produk (UnitInStock) dan total sale amount tiap kategori produknya?

### **Data General**

**tabel_A**

Data pertama atau query pertama merupakan data utama yang akan dianalisa lebih lanjut. Query utama ini berisikan gabungan dari beberapa tabel antara lain, `orders`, `orderdetails`, `customer`, `products`, dan `categories`. Karena fokus analisis adalah seluruh hal yang berhubungan dengan produk, maka dipilih kolom dari beberapa tabel yang dapat menghasilkan informasi penting terkait produk dari perusahaan. Informasi yang diambil antara lain:

- CustomerID (orders)               = ID dari setiap customer
- OrderID (orders)                  = ID dari setiap order yang dilakukan oleh customer
- OrderDate (orders)                = Tanggal order dilakukan oleh customer
- RequiredDate (orders)             = Tanggal produk dibutuhkan customer
- ShippedDate (orders)              = Tanggal produk dikirimkan ke customer
- ProductID (products)              = ID dari setiap produk
- ProductName (products)            = Nama setiap produk
- UnitsInStock (products)           = Stok produk yang tersedia saat ini
- Discontinued (products)           = Produk masih dijual atau diberhentikan penjualannya
- UnitPrice (orderdetails)          = Harga per unit tiap produk
- Quantity (orderdetails)           = Quantity setiap produk
- CategoryName (categories)         = Nama kategori produk
- CategoryID (categories)           = ID dari kategori produk
- CompanyName (customers)           = Nama perusahaan customer
- City (customers)                  = Kota dari customer
- Region (customers)                = Region dari customer
- Country (customers)               = Negara dari customer

Selain kolom penting dari beberapa tabel, untuk menambahkan informasi penting, dilakukan gabungan beberapa kolom sehingga menghasilkan kolom baru bernama `SaleAmount`. Kolom `SaleAmount` digunakan untuk informasi total harga penjualan yang didapatkan dari perkalian antara `UnitPrice` harga tiap produk dengan `quantity` atau jumlah produk yang dipesan(diluar biaya kargo `Freight`).

Semua informasi tersebut dijadikan dalam satu tabel (query) dalam bentuk dataframe yang akan diolah informasinya.


### **Data Category Product**

**tabel_product**

query kedua merupakan tabel infromasi tambahan yang dikhususkan untuk analisa produk yang terdiri dari, `CategoryName` merupakan kategori produk yang dijual oleh perusahaan northwind, `Total_Produk` merupakan total produk berdasarkan kategori produk, `Jumlah_Quantity` merupakan jumlah kuantitas berdasarkan kategori produk, dan `Produk_Tersedia` merupakan jumlah produk yang tersedia berdasarkan kategori produk. Selain itu, kolom `SaleAmount` berdasarkan kategori produk akan diambil dari tabel_A (query 1). Tabel ini akan memberikan gambaran mengenai kategori produk. Dapat dilihat juga keadaan stok barang yang tersedia sehingga dapat diperkirakan jika ingin menambahkan quantity setiap produk menyesuaikan ketersediaan produk.
