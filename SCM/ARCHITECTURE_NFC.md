# NFC Farmer Card Architecture

## Overview

Modul NFC Farmer Card merupakan bagian dari Enterprise AI & Traceability Platform yang digunakan sebagai identitas digital petani selama siklus operasional agribisnis.

Kartu NFC **tidak menyimpan data operasional internal**, tetapi berfungsi sebagai media identifikasi yang dipetakan ke database internal perusahaan.

Pendekatan ini dipilih untuk menjaga kompatibilitas dengan kartu donor, mempermudah pemeliharaan data, serta mendukung audit dan traceability.

---

# Design Principles

1. Do not modify donor-issued NFC cards.
2. Use NFC card as identity only.
3. All business data remains in MySQL.
4. Every transaction is recorded.
5. Every transaction is traceable.
6. Support future Blockchain integration.
7. Support future QR Hybrid implementation.

---

# High Level Architecture

```
NFC Farmer Card
        │
        ▼
Android Application (B4A)
        │
WebView
        │
HTML5 + JavaScript
        │
PHP API
        │
MySQL
        │
Enterprise Dashboard
```

---

# NFC Data Strategy

The NFC card acts only as an identity token.

Preferred order of identification:

1. Hardware UID
2. NDEF Record (if available)
3. Donor Identifier

Internal systems never depend on data stored inside the NFC memory.

---

# Internal Mapping

```
Donor NFC Card
        │
        ▼
UID Hardware
        │
        ▼
Internal Mapping Table
        │
        ▼
Farmer Master Data
```

---

# Core Database

## farmer

Master farmer information.

## farmer_card

Stores NFC UID and donor information.

## farmer_card_mapping

Relationship between farmer and NFC card.

## distribution_seed

Seed distribution records.

## distribution_fertilizer

Fertilizer distribution records.

## harvest_transaction

Harvest purchasing records.

## production_lot

Production lot generation.

## blockchain_event (Future)

Immutable traceability events.

---

# Operational Flow

Farmer Registration

```
Scan NFC
↓
Read UID
↓
Check Mapping
↓
Register Farmer
↓
Save Mapping
```

Seed Distribution

```
Scan NFC
↓
Load Farmer
↓
Input Seed
↓
Save Transaction
```

Fertilizer Distribution

```
Scan NFC
↓
Load Farmer
↓
Input Fertilizer
↓
Save Transaction
```

Harvest Purchase

```
Scan NFC
↓
Load Farmer
↓
Input Weight
↓
Generate Lot
↓
Save Transaction
```

---

# Traceability Flow

```
Farmer
      │
      ▼
Farm Polygon
      │
      ▼
Harvest
      │
      ▼
Production Lot
      │
      ▼
Warehouse
      │
      ▼
Export
      │
      ▼
Buyer
```

---

# Security Principles

* Never overwrite donor NFC cards.
* Preserve original donor information.
* Store all mappings internally.
* Log every NFC scan.
* Support offline synchronization in future versions.

---

# Technology Stack

Backend

* PHP
* MySQL

Frontend

* HTML5
* Bootstrap
* JavaScript

Mobile

* B4A (B4X)
* Android NFC
* WebView

GIS

* Leaflet
* GeoJSON

Future

* Blockchain Traceability
* Enterprise AI
* Offline Sync
* QR + NFC Hybrid
