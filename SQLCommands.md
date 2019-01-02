1. SELECT

 Untuk meilih  table database untuk di tampilkan 
	SELECT column1, column2, ...
	FROM table_name;

	SELECT ContactName, City
	FROM Customers;

	SELECT * FROM Customers;

	SELECT DISTINCT City FROM Customers;

	//DISTINCT digunakan ketika di table database kita banyak yang duplicate,kita bisa menampilkan data tanpa duplicate nya 


2. WHERE 

Untuk memfilter data yang kita tampilkan

	SELECT column1, column2, ...
	FROM table_name
	WHERE condition;

	SELECT ContactName
	FROM Customers
	WHERE London;

Operator WHERE

	=		Equal
	<>		Not equal. Note: In some versions of SQL this operator may be written as !=
	>		Greater than
	<		Less than
	>=		Greater than or equal
	<=		Less than or equal
	BETWEEN	Between a certain range
	LIKE	Search for a pattern
	IN		To specify multiple possible values for a column


3. AND,OR and NOT

AND jika kedua kondisi benar
OR Jika salah satu kondisi benar
NOT Jika kedua kondisi tidak ada yang benar

AND Syntax

	SELECT column1, column2, ...
	FROM table_name
	WHERE condition1 AND condition2 AND condition3 ...;

	SELECT * FROM Customers
	WHERE Country='Germany' AND City='Berlin';

OR Syntax

	SELECT column1, column2, ...
	FROM table_name
	WHERE condition1 OR condition2 OR condition3 ...;

	SELECT * FROM Customers
	WHERE City='Berlin' OR City='München';

NOT Syntax

	SELECT column1, column2, ...
	FROM table_name
	WHERE NOT condition;

	SELECT * FROM Customers
	WHERE NOT Country='Germany';

AND dan OR

	SELECT * FROM Customers
	WHERE Country='Germany' AND (City='Berlin' OR City='München');

AND dan Not

	SELECT * FROM Customers
	WHERE NOT Country='Germany' AND NOT Country='USA';


4. ORDER By

Untuk menampilkan secara urut dari atas atau bawah

ASC urut dari atas 

DESC urut dari bawah

	SELECT column1, column2, ...
	FROM table_name
	ORDER BY column1, column2, ... ASC|DESC;

Menampilkan urut sesuai abjad

	SELECT * FROM Customers
	ORDER BY Country;

Menampilkan dari bawah sesuai abjad

	SELECT * FROM Customers
	ORDER BY CustomerName DESC;

Jika kita ingin menampilkan 2 kolom dan berbeda kondisi

	SELECT * FROM Customers
	ORDER BY Country ASC, CustomerName DESC;

	//Country akan tampil urut dari atas ke bawah dan CustomerName akan tampil urut dari bawah ke atas

5. INSERT INTO

Untuk memasukkan data kedalam tabel database

	INSERT INTO table_name (column1, column2, column3, ...)
	VALUES (value1, value2, value3, ...);

	INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
	VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway');

6. Null Values

Null adalah ketika suatu data tidak ada isinya atau kosong, dan Null beda dengan nol,kalo nol masih ada isinya tapi kalo null blank tidak ada sama sekali

Kita bisa mengetes Null Values dengan 

IS NULL Untuk mengetes null values 

	SELECT CustomerName, ContactName, Address
	FROM Customers
	WHERE Address IS NULL;

	//Jika data nya tidak ada yang null maka tidak akan tampil

IS NOT NULL untuk mengetes data yang bukan null

	SELECT CustomerName, ContactName, Address
	FROM Customers
	WHERE Address IS NOT NULL;

7. UPDATE

Untuk mengupdate table database

	UPDATE table_name
	SET column1 = value1, column2 = value2, ...
	WHERE condition;

	UPDATE Customers
	SET ContactName = 'Alfred Schmidt', City= 'Frankfurt'
	WHERE CustomerID = 2;

Syntax diatas akan mengupdate data cutomer nomer 2.

	UPDATE Customers
	SET ContactName='Juan'
	WHERE Country='Mexico';

Syntax diatas akan mengupdate data customer yang berasal dari mexico.

Untuk menggunakan UPDATE kita harus berhati-hati,jika kita tidak menggunakan WHERE maka satu table database akan terupdate

8. DELETE

Untuk menghapus data customer

	DELETE FROM table_name WHERE condition;

	DELETE FROM Customers WHERE CustomerName='Alfreds Futterkiste';

	DELETE FROM table_name;
	//Syntax ini akan semua baris dalam table tapi tidak mengahus table tersebut,struktur, atribut dan index akan tetap utuh 

9. SELECT TOP

Untuk menampilkan nomer spesifik

	SELECT TOP number|percent column_name(s)
	FROM table_name
	WHERE condition;

	SELECT TOP 3 * FROM Customers;
	//akan menampilkan 3 data pertama

	SELECT TOP 3 * FROM Customers
	WHERE Country='Germany';
	//akan menampilkan 3 data pertama yang berasal dari jerman

	SELECT TOP 50 PERCENT * FROM Customers;
	//akan menampilkan 50 persen data pertama

10. MIN() dan MAX()

MIN() untuk menampilkan isi yang terkecil dari suatu kolom

MAX() untuk menampilkan isi yang terbesar dari suatu kolom 

	SELECT MIN(column_name)
	FROM table_name
	WHERE condition;

	SELECT MIN(Price) AS SmallestPrice
	FROM Products;

	SELECT MAX(column_name)
	FROM table_name
	WHERE condition;

	SELECT MAX(Price) AS LargestPrice
	FROM Products;

11. COUNT(), AVG() and SUM() Functions

COUNT() untuk menampilkan nomer baris sesuai yang kita cari

	SELECT COUNT(column_name)
	FROM table_name
	WHERE condition;

	SELECT COUNT(ProductID)
	FROM Products;

AVG() untuk menampilkan rata-rata

	SELECT AVG(column_name)
	FROM table_name
	WHERE condition;

	SELECT AVG(Price)
	FROM Products;

SUM()  untuk menampilkan jumlah dari suatu kolom

	SELECT SUM(column_name)
	FROM table_name
	WHERE condition;

	SELECT SUM(Quantity)
	FROM OrderDetails;

12. LIKE 

untuk mencari data pada kolom sesuai yang kita tentukan

Ada dua wilcard yang bisa kita gunakan untuk mempermudak kita

% - Tanda persen mewakili nol, satu, atau beberapa karakter
_ - Garis bawah mewakili satu karakter

	SELECT column1, column2, ...
	FROM table_name
	WHERE columnN LIKE wildcard;

LIKE Operator					Description
WHERE CustomerName LIKE 'a%'	Menemnukan semua data yang diawali dengan "a"
WHERE CustomerName LIKE '%a'	Menemukan semua data yang diakhiri dengan "a"
WHERE CustomerName LIKE '%or%'	Menemukan semua data yang memilki "or" disemua posisi
WHERE CustomerName LIKE '_r%'	Menemukan semua data yang meiliki "r" diposisi kedua
WHERE CustomerName LIKE 'a_%_%'	Menemukan semua data yang diawali "a" dan punya 3 karakter di belakangnya
WHERE ContactName LIKE 'a%o'	Menemukan semua data yang diawali "a" dan diakhiri dengan "o"


	SELECT * FROM Customers
	WHERE CustomerName LIKE 'a%';

Wilcard 

'[bsp]%' = yang diawali 'b' atau 's' atau 'p'

'[a-c]%' = yang diawali 'a' atau 'b' atau 'c'

'[!bsp]%' = yang tidak diawali  'b' atau 's' atau 'p'

13. IN

untuk menampilkan data sesuai yang kita cari

	SELECT column_name(s)
	FROM table_name
	WHERE column_name IN (value1, value2, ...);

	SELECT * FROM Customers
	WHERE Country IN ('Germany', 'France', 'UK');

Syntax diatas untuk menampilkan data yang berasal dari German France dan UK


14. BETWEEN

untuk menampilkan isi data dalam renang yang ditentukan

	SELECT column_name(s)
	FROM table_name
	WHERE column_name BETWEEN value1 AND value2;\

	SELECT * FROM Products
	WHERE Price BETWEEN 10 AND 20;

	SELECT * FROM Products
	WHERE (Price BETWEEN 10 AND 20)
	AND NOT CategoryID IN (1,2,3);

Syntax diatas akan menampikan data dengan rentang harga dari antara 10 dan 20 dan Category ID nya bukan 1,2,3.

Kita juga bisa menggunakan tanggal 

	SELECT * FROM Orders
	WHERE OrderDate BETWEEN #01/07/1996# AND #31/07/1996#;

Atau

	SELECT * FROM Orders
	WHERE OrderDate BETWEEN '1996-07-01' AND '1996-07-31';

15. AS

untuk membuat nama alias,agar nama kolo lebih mudah dibaca

Syntax nama alias pada kolom

	SELECT column_name AS alias_name
	FROM table_name;

	SELECT CustomerID AS ID, CustomerName AS Customer
	FROM Customers;

Syntax nama alias pada table

	SELECT column_name(s)
	FROM table_name AS alias_name;

	SELECT o.OrderID, o.OrderDate, c.CustomerName
	FROM Customers AS c, Orders AS o
	WHERE c.CustomerName="Around the Horn" AND c.CustomerID=o.CustomerID;

16. UNION

Union digunakan untuk menggabungkan dua hasil dari SELECT

	SELECT column_name(s) FROM table1
	UNION
	SELECT column_name(s) FROM table2;

Jika kita ingin menampilkan data yang duplicate juga kita bisa gunakan UNION ALL

	SELECT column_name(s) FROM table1
	UNION ALL
	SELECT column_name(s) FROM table2;

dalam penggunaan UNION kita hanya menggabungkan data beredasarkan kolom yang sama

17. EXIST

Untuk mengetes apakah datanya sudah ada atau belom

	SELECT column_name(s)
	FROM table_name
	WHERE EXISTS
	(SELECT column_name FROM table_name WHERE condition);

	SELECT SupplierName
	FROM Suppliers
	WHERE EXISTS (SELECT ProductName FROM Products WHERE SupplierId = Suppliers.supplierId AND Price < 20);

18. SELECT INTO 

Untuk menyalin data yang ada dalam table ke table yang lain

	SELECT * INTO CustomersBackup2017
	FROM Customers;

Membuat salinan data backup customer

	SELECT * INTO CustomersBackup2017 IN 'Backup.mdb'
	FROM Customers;

Membuat salinan ke dalam table di database yang lain

	SELECT CustomerName, ContactName INTO CustomersBackup2017
	FROM Customers;

Menyalin beberapa kolom ke table yang baru

	SELECT * INTO CustomersGermany
	FROM Customers
	WHERE Country = 'Germany';

Menyalin Cutomer yang berasal dari german ke table yang baru

19. CASE 

untuk menyatakan lebih dari satu kondisi sama seperti if else

	SELECT OrderID, Quantity,
	CASE
    	WHEN Quantity > 30 THEN "The quantity is greater than 30"
    	WHEN Quantity = 30 THEN "The quantity is 30"
    	ELSE "The quantity is under 30"
	END AS QuantityText
	FROM OrderDetails;

	SELECT CustomerName, City, Country
	FROM Customers
	ORDER BY
	(CASE
 		WHEN City IS NULL THEN Country
    	ELSE City
	END);

20. Stored Procedure

Stored Procedure adalah kode SQL yang disiapkan yang dapat Anda simpan, sehingga kode tersebut dapat digunakan kembali berulang kali,Ketika kita memiliki SQL query kita  bisa memanggilnya dan mengaksesnya.

	CREATE PROCEDURE procedure_name
	AS
	sql_statement
	GO;

Kita bisa memmanggilnya dengan

	EXEC SelectAllCustomers;

Membuat Store Procedure yang memilih customer sesuai kota nya dari Customers table

	CREATE PROCEDURE SelectAllCustomers @City nvarchar(30)
	AS
	SELECT * FROM Customers WHERE City = @City
	GO;

	EXEC SelectAllCustomers City = "London";

# SQL Comment

kita bisa membuat komentar dengan tanda "--" di awal baris

