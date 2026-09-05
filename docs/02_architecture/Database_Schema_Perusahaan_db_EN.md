# Database Schema — perusahaan_db

## 1. Database

**Database Name:** `perusahaan_db`

**Database Engine:** MySQL 8.4

The `perusahaan_db` database is the project source database containing the core business entities required for transaction processing, financial records, customer management, and product management.

---

## 2. Database Tables

The database contains four core tables:

1. `produk`
2. `pelanggan`
3. `transaksi`
4. `keuangan`

---

## 3. Table: produk

| Column | Data Type | Null | Key | Extra |
|---|---|---|---|---|
| `id_produk` | `int` | NO | PRI | `auto_increment` |
| `nama_produk` | `varchar(100)` | NO | MUL | |
| `harga` | `decimal(12,2)` | NO | | |
| `stok` | `int` | NO | | |

**Primary Key:** `id_produk`

**Record Count:** 5

---

## 4. Table: pelanggan

| Column | Data Type | Null | Key | Extra |
|---|---|---|---|---|
| `id_pelanggan` | `int` | NO | PRI | `auto_increment` |
| `nama_pelanggan` | `varchar(100)` | NO | | |
| `alamat` | `varchar(200)` | YES | | |
| `no_telepon` | `varchar(20)` | YES | | |

**Primary Key:** `id_pelanggan`

**Record Count:** 2,002

---

## 5. Table: transaksi

| Column | Data Type | Null | Key | Extra |
|---|---|---|---|---|
| `id_transaksi` | `int` | NO | PRI | `auto_increment` |
| `id_pelanggan` | `int` | NO | MUL | |
| `id_produk` | `int` | NO | MUL | |
| `tanggal_transaksi` | `date` | NO | | |
| `jumlah` | `int` | NO | | |
| `total_harga` | `decimal(12,2)` | NO | | |

**Primary Key:** `id_transaksi`

**Foreign Keys:**

- `id_pelanggan` → `pelanggan.id_pelanggan`
- `id_produk` → `produk.id_produk`

**Record Count:** 5,000

---

## 6. Table: keuangan

| Column | Data Type | Null | Key | Extra |
|---|---|---|---|---|
| `id_keuangan` | `int` | NO | PRI | `auto_increment` |
| `id_transaksi` | `int` | NO | UNI | |
| `tanggal` | `date` | NO | | |
| `pemasukan` | `decimal(12,2)` | NO | | |
| `keterangan` | `varchar(200)` | YES | | |

**Primary Key:** `id_keuangan`

**Foreign Key:**

- `id_transaksi` → `transaksi.id_transaksi`

**Unique Key:** `id_transaksi`

**Record Count:** 5,000

---

## 7. Relationships

The database relationships are defined through the following Foreign Key constraints:

| Child Table | Foreign Key | Parent Table | Referenced Column | Constraint |
|---|---|---|---|---|
| `transaksi` | `id_pelanggan` | `pelanggan` | `id_pelanggan` | `transaksi_ibfk_1` |
| `transaksi` | `id_produk` | `produk` | `id_produk` | `transaksi_ibfk_2` |
| `keuangan` | `id_transaksi` | `transaksi` | `id_transaksi` | `keuangan_ibfk_1` |

### Relationship Flow

```text
pelanggan
    |
    | id_pelanggan
    ↓
transaksi
    |
    | id_produk
    ↓
produk

transaksi
    |
    | id_transaksi
    ↓
keuangan

8. Referential Integrity Verification

The database relationships were cross-checked against the actual records.

Validation	Result	Status
Transactions without matching customers	0	PASS
Transactions without matching products	0	PASS
Financial records without matching transactions	0	PASS

Referential Integrity Status: PASS

All verified Foreign Key relationships have valid corresponding parent records.

9. Record Count Verification
Table	Record Count
produk	5
pelanggan	2,002
transaksi	5,000
keuangan	5,000
10. Core Data Verification

The core transaction and financial metrics were verified directly against the perusahaan_db database.

Metric	Verified Value
Total Transactions	5,000
Total Unit	27,400
Total Revenue	Rp110,380,250,000.00
Total Financial Records	5,000
Total Pemasukan	Rp110,380,250,000.00
Revenue Consistency
Transaction Revenue
= Rp110,380,250,000.00

Financial Pemasukan
= Rp110,380,250,000.00

Difference
= Rp0.00

Financial Consistency Status: PASS

11. Cross-Check with Final Project

The core database metrics were cross-checked against the final project results.

Metric	Database	Final Project	Status
Total Transactions	5,000	5,000	PASS
Total Unit	27,400	27,400	PASS
Total Revenue	Rp110,380,250,000.00	Rp110,380,250,000.00	PASS

Final Database Cross-Check: PASS

The verified transaction volume, total units, and total revenue are consistent with the final project results.

12. Database Verification Status

Database: perusahaan_db

Schema Verification: PASS

Table Verification: PASS

Column Verification: PASS

Primary Key Verification: PASS

Foreign Key Verification: PASS

Relationship Verification: PASS

Referential Integrity: PASS

Record Count Verification: PASS

Financial Consistency: PASS

Final Project Cross-Check: PASS

Overall Database Schema Verification: PASS

13. Verification Basis

This documentation reflects the actual structure and data state verified from the active MySQL database perusahaan_db.

The verification covered:

Database existence
Table existence
Column definitions
Data types
NULL constraints
Primary Keys
Foreign Keys
Unique Key
Foreign Key relationships
Record counts
Referential integrity
Transaction totals
Unit totals
Revenue totals
Financial income totals
Cross-check against final project results

The documented schema and verification results are based on the verified database state and are intended to serve as the authoritative technical documentation for the project database.