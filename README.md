# Tugas Praktikum { Pertemuan ke 13 } <img src=https://logos-download.com/wp-content/uploads/2016/05/MySQL_logo_logotype.png width="130px" >


|**Nama**|**NIM**|**Kelas**|**Matkul**|
|----|---|-----|------|
|Oktavia Rizkha Kurniawati|312310509|TI.23.A5|Basis Data|

![gambar_tugas](screenshot/Soal%20Tabel.png)

***Query MySQL Pada Tabel Perusahaan***

```
CREATE TABLE Perusahaan(
id_p VARCHAR(10) PRIMARY KEY,
nama VARCHAR(45) NOT NULL,
alamat VARCHAR(45) DEFAULT NULL
);

INSERT INTO Perusahaan VALUES
('P01', 'Kantor Pusat', NULL),
('P02', 'Cabang Bekasi', NULL);
SELECT * FROM Perusahaan;
```

***Output :***

![Screenshot 2024-06-10 104109](https://github.com/oktavia18/tugas-praktikum7/assets/147913672/e4d57cbd-f1a5-4c03-b799-6f5edf5daa8c)



***Query MySQL Pada Tabel Departemen***

```
CREATE TABLE Departemen(
id_dept VARCHAR(10) PRIMARY KEY,
nama VARCHAR(45) NOT NULL,
id_p VARCHAR(10) NOT NULL,
manajer_nik VARCHAR(10) DEFAULT NULL
);

INSERT INTO Departemen VALUES
('D01', 'Produksi', 'P02', 'N01'),
('D02', 'Marketing', 'P01', 'N03'),
('D03', 'RnD', 'P02', NULL),
('D04', 'Logistik', 'P02', NULL);
SELECT * FROM Departemen;
```

***Output :***

![Screenshot 2024-06-10 104131](https://github.com/oktavia18/tugas-praktikum7/assets/147913672/9263096d-b6a0-4016-9078-b745b16a0faf)



***Query MySQL Pada Tabel Karyawan***

```
CREATE TABLE Karyawan(
nik VARCHAR(10) PRIMARY KEY,
nama VARCHAR(45) NOT NULL,
id_dept VARCHAR(10) NOT NULL,
sup_nik VARCHAR(10) DEFAULT NULL
);

INSERT INTO Karyawan VALUES
('N01', 'Ari', 'D01', NULL),
('N02', 'Dina', 'D01', NULL),
('N03', 'Rika', 'D03', NULL),
('N04', 'Ratih', 'D01', 'N01'),
('N05', 'Riko', 'D01', 'N01'),
('N06', 'Dani', 'D02', NULL),
('N07', 'Anis', 'D02', 'N06'),
('N08', 'Dika', 'D02', 'N06');
SELECT * FROM Karyawan;
```

***Output :***

![Screenshot 2024-06-10 104147](https://github.com/oktavia18/tugas-praktikum7/assets/147913672/6b176875-6c54-4ec6-9d15-f6b019509945)



***Query MySQL Pada Tabel Project***

```
CREATE TABLE Project(
id_proj VARCHAR(10) PRIMARY KEY,
nama VARCHAR(45) NOT NULL,
tgl_mulai DATETIME,
tgl_selesai DATETIME,
status TINYINT(1)
);

INSERT INTO Project VALUES
('PJ01', 'A', '2019-01-10', '2019-03-10', '1'),
('PJ02', 'B', '2019-02-15', '2019-04-10', '1'),
('PJ03', 'C', '2019-03-21', '2019-05-10', '1');
SELECT * FROM Project;
```

***Output :***

![Screenshot 2024-06-10 104159](https://github.com/oktavia18/tugas-praktikum7/assets/147913672/49790017-8fff-4c20-920a-da2c6614df38)



***Query MySQL Pada Tabel Project Deatil***

```
CREATE TABLE Project_detail(
id_proj VARCHAR(10) NOT NULL,
nik VARCHAR(10) NOT NULL
);

INSERT INTO Project_detail VALUES
('PJ01', 'N01'),
('PJ01', 'N02'),
('PJ01', 'N03'),
('PJ01', 'N04'),
('PJ01', 'N05'),
('PJ01', 'N07'),
('PJ01', 'N08'),
('PJ02', 'N01'),
('PJ02', 'N03'),
('PJ02', 'N05'),
('PJ03', 'N03'),
('PJ03', 'N07'),
('PJ03', 'N08');
SELECT * FROM Project_detail;
```

***Output :***

![Screenshot 2024-06-10 104217](https://github.com/oktavia18/tugas-praktikum7/assets/147913672/be591507-bb3b-4b80-8e3d-5d4147f632b9)



## Menampilkan Nama Manajer Tiap Departemen

```
Select Departemen.nama AS Departemen, Karyawan.nama AS Manajer
FROM Departemen
LEFT JOIN Karyawan ON Karyawan.nik = Departemen.manajer_nik;
```

***Output :***

![Screenshot 2024-06-10 104249](https://github.com/oktavia18/tugas-praktikum7/assets/147913672/7bfea01d-0fe0-4153-92c9-456c72aa00d8)



## Menampilkan Nama Supervisor Tiap Karyawan

```
SELECT Karyawan.nik, Karyawan.nama, Departemen.nama AS Departemen, Supervisor.nama AS Supervisor
FROM Karyawan
LEFT JOIN Karyawan AS Supervisor ON Supervisor.nik = Karyawan.sup_nik
LEFT JOIN Departemen ON Departemen.id_dept = Karyawan.id_dept;
```
***Output :***

![Screenshot 2024-06-10 104501](https://github.com/oktavia18/tugas-praktikum7/assets/147913672/138d62d0-f669-41a5-84ce-ee37bf0c3a89)



## Menampilkan Daftar Karyawan Yang Bekerja Pada Project A
```
SELECT Karyawan.nik, Karyawan.nama
FROM Karyawan
JOIN Project_detail ON Project_detail.nik = Karyawan.nik
JOIN Project ON Project.id_proj = Project_detail.id_proj
WHERE Project.nama = 'A';
```
***Output :***

![Screenshot 2024-06-10 104514](https://github.com/oktavia18/tugas-praktikum7/assets/147913672/6998731b-f19a-49f9-9f22-a86d21931695)



# Soal Latihan Praktikum

## 1. Departemen Apa Saja Yang Terlibat Dalam Tiap-tiap Project.

```
SELECT Project.nama AS Project, GROUP_CONCAT(Departemen.nama) AS Departemen
FROM Project
INNER JOIN Project_detail ON Project.id_proj = Project_detail.id_proj
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
INNER JOIN Departemen ON Karyawan.id_dept = Departemen.id_dept
GROUP BY Project.id_proj;
```
***Output :***

![Screenshot 2024-06-10 104528](https://github.com/oktavia18/tugas-praktikum7/assets/147913672/5eb50ab8-5a3f-4b09-83bb-7e7904d4210a)



## 2. Jumlah Karyawan Tiap Departemen Yang Bekerja Pada Tiap-tiap Project.

```
SELECT Project.nama AS Project, Departemen.nama AS Departemen, COUNT(*) AS 'Jumlah Karyawan'
FROM Project
INNER JOIN Project_detail ON Project.id_proj = Project_detail.id_proj
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
INNER JOIN Departemen ON Karyawan.id_dept = Departemen.id_dept
GROUP BY Project.id_proj, Departemen.id_dept;
```
***Output :***

![Screenshot 2024-06-10 104725](https://github.com/oktavia18/tugas-praktikum7/assets/147913672/34b0a023-f631-4173-b176-88ce9fb5be9e)



## 3. Ada Berapa Project Yang Sedang Dikerjakan Oleh Departemen ***RnD***? (ket: project berjalan adalah yang statusnya 1).

```
SELECT COUNT(*) AS 'Jumlah Project'
FROM Project
INNER JOIN Project_detail ON Project.id_proj = Project_detail.id_proj
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
INNER JOIN Departemen ON Karyawan.id_dept = Departemen.id_dept
WHERE Departemen.nama = 'RnD' AND Project.status = 1;
```
***Output :***

![Screenshot 2024-06-10 104742](https://github.com/oktavia18/tugas-praktikum7/assets/147913672/4924ab75-052b-4fe5-b55b-e13abea80c20)



## 4. Berapa banyak Project yang sedang dikerjakan oleh Ari ?

```
SELECT COUNT(*) AS 'Jumlah Project'
FROM Project_detail
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
WHERE Karyawan.nama = 'Ari' AND Project_detail.id_proj IN (SELECT id_proj FROM Project WHERE status = 1);
```
***Output :***

![Screenshot 2024-06-10 104801](https://github.com/oktavia18/tugas-praktikum7/assets/147913672/b8f3d8ae-90a7-449c-8c31-40f8f95613aa)



## 5. Siapa Saja Yang Mengerjakan Project B ?

```
SELECT Karyawan.nama
FROM Project_detail
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
WHERE Project_detail.id_proj IN (SELECT id_proj FROM Project WHERE nama = 'B');
```
***Output :***

![Screenshot 2024-06-10 104823](https://github.com/oktavia18/tugas-praktikum7/assets/147913672/6cced1fa-918c-4513-8f7d-8e30c947e59b)

