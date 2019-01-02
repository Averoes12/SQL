# Create Database

	CREATE DATABASE databasename;

# Delete Database

	DROP DATABASE databasename;

# Backup Database 
 Untuk membackup seluruh data pada database yang sudah ada

 	BACKUP DATABASE databasename
	TO DISK = 'filepath';

	BACKUP DATABASE testDB
	TO DISK = 'D:\backups\testDB.bak';

Selalu cadangkan database ke drive yang berbeda dari database yang sebenarnya. Jika Anda mengalami kerusakan disk, Anda tidak akan kehilangan file cadangan bersama dengan database.

	BACKUP DATABASE databasename
	TO DISK = 'filepath'
	WITH DIFFERENTIAL;

	BACKUP DATABASE testDB
	TO DISK = 'D:\backups\testDB.bak'
	WITH DIFFERENTIAL;

Back up diferensial akan menghemat waktu karna hanya mencadangkan perubahan data

# Create Table

	CREATE TABLE table_name (
    	column1 datatype,
    	column2 datatype,
    	column3 datatype,
   		....	
	);

	CREATE TABLE Persons (
    	PersonID int,
    	LastName varchar(255),
    	FirstName varchar(255),
    	Address varchar(255),
    	City varchar(255) 
	);

untuk melihat macam-macam tipe data kita bisa meliharnuya di link ini https://www.w3schools.com/sql/sql_datatypes.asp

Salinan tabel yang ada juga dapat dibuat menggunakan CREATE TABLE.

Tabel baru mendapatkan definisi kolom yang sama. Semua kolom atau kolom tertentu dapat dipilih.

Jika Anda membuat tabel baru menggunakan tabel yang ada, tabel baru akan diisi dengan nilai yang ada dari tabel lama.

	CREATE TABLE TestTable AS
	SELECT customername, contactname
	FROM customers;

# Delete Table

	DROP TABLE table_name;

	DROP TABLE Shippers;

Kita harus berhati-hati dalam menghapus table,karna akan menghilangkan data lengkap yang di dalam table

	TRUNCATE TABLE table_name;

TRUNCATE untuk mengahapus data yang ada dalam table tapi tidak mengahapus table nya

# ALTER TABLE

ALTER TABLE biasa digunakan untuk menambah menghapus atau memodifikasi data pada table yang sudah ada

ADD kolom

	ALTER TABLE table_name
	ADD column_name datatype;

	ALTER TABLE Customers
	ADD Email varchar(255);

DROP kolom

	ALTER TABLE table_name
	DROP COLUMN column_name;

	ALTER TABLE Customers
	DROP COLUMN Email;

Modifikasi data

	ALTER TABLE table_name
	ALTER COLUMN column_name datatype;

# UNIQUE

untuk memastikan bahwa semua nilai dalam kolom berbeda.

	CREATE TABLE Persons (
    	ID int NOT NULL UNIQUE,
    	LastName varchar(255) NOT NULL,
    	FirstName varchar(255),
    	Age int
	);

SQL membuat UNIQUE Constraint pada kolom ID pada saat table Persons dibuat

	ALTER TABLE Persons
	ADD UNIQUE (ID);

Membuat UNIQUE Constraint pada kolom ID ketika table sudah dbuat

# PRIMARY KEY

Primary Key mengidentifikasi semua data pada sebuah table,Primary Key harus mengandung nilai UNIQUE tidak bisa mengandung nilai NULL,dan kita hanya bisa membuat satu primary key pada sebuah table

Membuat primary key pada kolom ID saat table Persons dibuat
	CREATE TABLE Persons (
    	ID int NOT NULL PRIMARY KEY,
    	LastName varchar(255) NOT NULL,
    	FirstName varchar(255),
    	Age int
	);

Membuat Primary Key pada kolom ID ketika table sudah dibuat

	ALTER TABLE Persons
	ADD PRIMARY KEY (ID);

Untuk mengahapus primary key

	ALTER TABLE Persons
	DROP PRIMARY KEY;

# FOREIGN KEY

Digunakan untuk menghubungkan dua table bersamaan,Tabel yang berisi foreign key disebut child table, dan tabel yang berisi candidate key disebut tabel referensi atau parent table,Foreign key digunakan untuk mencegah tindakan yang akan menghancurkan hubungan antar tabel,Foreign Key juga mencegah data yang tidak valid dimasukkan ke dalam kolom.

Membuat foreingn key saat table dibuat

	CREATE TABLE Orders (
    	OrderID int NOT NULL PRIMARY KEY,
    	OrderNumber int NOT NULL,
    	PersonID int FOREIGN KEY REFERENCES Persons(PersonID)
	);

Membuat foreign key ketika table sudah dibuat

	ALTER TABLE Orders
	ADD CONSTRAINT FK_PersonOrder
	FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);

Menghapus foreign key

	ALTER TABLE Orders
	DROP CONSTRAINT FK_PersonOrder;

# CHECK

Digunakan untuk membatasi rentang nilai yang dapat ditempatkan dalam kolom,Jika kita membuat CHECK pada satu kolom, ini hanya mengizinkan nilai tertentu untuk kolom tersebut,Jika Kita membuat CHECK pada tabel itu bisa membatasi nilai dalam kolom tertentu berdasarkan pada nilai di kolom.

	CREATE TABLE Persons (
    	ID int NOT NULL,
    	LastName varchar(255) NOT NULL,
    	FirstName varchar(255),
    	Age int CHECK (Age>=18)
	);


	ALTER TABLE Persons
	ADD CHECK (Age>=18);

	ALTER TABLE Persons
	DROP CHECK CHK_PersonAge;

# DEFAULT 

Jika kita tidak memasukkan nilai pada sebuah kolom kita bisa membuat nilai default untuk menambahkan ke kolom tersebut

	CREATE TABLE Persons (
    	ID int NOT NULL,
    	LastName varchar(255) NOT NULL,
    	FirstName varchar(255),
    	Age int,
    	City varchar(255) DEFAULT 'Sandnes'
	);

Default juga bisa menggunakan system input data dengan menggunakan function GETDATE()

	CREATE TABLE Orders (
    	ID int NOT NULL,
    	OrderNumber int NOT NULL,
    	OrderDate date DEFAULT GETDATE()
	);

Menambahkan default jika table sudah dibuat

	ALTER TABLE Persons
	ADD CONSTRAINT df_City 
	DEFAULT 'Sandnes' FOR City

Menghapus DEFAULT

	ALTER TABLE Persons
	ALTER COLUMN City DROP DEFAULT;

# INDEX 

untuk membuat index pada table 

membiarkan duplicate data

	CREATE INDEX index_name
	ON table_name (column1, column2, ...);

	CREATE INDEX idx_lastname
	ON Persons (LastName);

agar tidak ada yang duplicate

	CREATE UNIQUE INDEX index_name
	ON table_name (column1, column2, ...);

	CREATE UNIQUE INDEX idx_pname
	ON Persons (LastName, FirstName);

Mengahapus index

	DROP INDEX table_name.index_name;

# AUTO INCREMENT

Menamabahkan nomor secara otomatis ketika data di masukkan\

	CREATE TABLE Persons (
    	ID Integer PRIMARY KEY AUTOINCREMENT,
    	LastName varchar(255) NOT NULL,
    	FirstName varchar(255),
    	Age int
	);

# DATE

Bagian tersulit ketika bekerja dengan tanggal adalah memastikan bahwa format tanggal yang Anda coba masukkan, cocok dengan format kolom tanggal dalam database.

- DATE - format YYYY-MM-DD

- DATETIME - format: YYYY-MM-DD HH:MI:SS

- SMALLDATETIME - format: YYYY-MM-DD HH:MI:SS

- TIMESTAMP - format: a unique number

Jenis format tanggal dipilih saat kita membuat tabel baru di database

# SQL INJECTION

Injeksi SQL adalah teknik injeksi kode yang dapat merusak database Anda.

Injeksi SQL adalah salah satu teknik peretasan web yang paling umum.

Injeksi SQL adalah penempatan kode berbahaya dalam pernyataan SQL, melalui input halaman web.

