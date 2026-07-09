NFC Farmer Card System
Source Code Summary

Version : 0.1.0 (Prototype)

Overview

Modul NFC Farmer Card merupakan bagian dari Enterprise Agriculture Platform yang digunakan sebagai identitas digital petani.
Aplikasi Android dibangun menggunakan B4X (B4A) sebagai mobile client, sedangkan backend menggunakan PHP Native + MySQL dengan antarmuka berbasis HTML5 yang ditampilkan melalui WebView.
Seluruh data operasional disimpan pada server. Kartu NFC hanya berfungsi sebagai media identifikasi.

Technology Stack
@Mobile
B4A (B4X) , Android NFC API , WebView

@Backend
PHP Native --   MySQL / MariaDB   --  REST API (JSON)

@Frontend
HTML5 - Bootstrap 5 - JavaScript - Fetch API

@Future Integration
Leaflet GIS - Blockchain Traceability - QR Hybrid - Enterprise AI


Project Structure
mobile/
│
├── Main.bas
├── NFCManager.bas
├── WebView.bas
└── Utils.bas

server/
│
├── api/
│     get_farmer.php
│     save_seed.php
│     save_fertilizer.php
│     save_harvest.php
│     register_card.php
│
├── pages/
│     farmer.php
│     harvest.php
│     seed.php
│     fertilizer.php
│
├── assets/
├── js/
├── css/
└── config/


Scan Flow
Tap NFC Card
        │
        ▼
Android NFC Reader
        │
        ▼
Read UID
        │
        ▼
WebView
        │
        ▼
PHP API
        │
        ▼
MySQL
Registration Flow
Scan Card
      │
      ▼
Read UID
      │
      ▼
Check Database
      │
      ├── Already Registered
      │          │
      │          ▼
      │     Open Farmer Profile
      │
      └── Not Registered
                 │
                 ▼
          Register Farmer
Distribution Flow

Seed Distribution

Tap Card
↓
Read UID
↓
Load Farmer
↓
Input Seed
↓
Save Transaction

Fertilizer Distribution

Tap Card
↓
Read UID
↓
Load Farmer
↓
Input Fertilizer
↓
Save Transaction

Harvest Purchase

Tap Card
↓
Read UID
↓
Load Farmer
↓
Input Weight
↓
Generate Lot Number
↓
Save Purchase
NFC Strategy

The system does NOT overwrite donor-issued NFC cards.

The application stores:

NFC Hardware UID
NDEF Information (if available)
Donor Information (optional)

Business data is maintained inside the internal database.

Database Mapping
NFC Card
    │
    ▼
farmer_card
    │
    ▼
farmer_card_mapping
    │
    ▼
farmer
****Suggested Tables
****farmer
****farm_polygon
****farmer_card
****farmer_card_mapping
****seed_distribution
****fertilizer_distribution
****harvest_transaction
****production_lot
****scan_log

API Summary
Read Farmer
GET
/api/get_farmer.php?uid={UID}

Register Card
POST
/api/register_card.php

Save Seed Distribution
POST
/api/save_seed.php

Save Fertilizer Distribution
POST
/api/save_fertilizer.php

Save Harvest
POST
/api/save_harvest.php
WebView Communication

Android (B4A)

Read NFC UID
↓
Load URL

https://server/api/get_farmer.php?uid=XXXXXXXX

PHP

Receive UID
↓
Query Database
↓
Return JSON

HTML5

Receive JSON
↓
Display Farmer Information
Security Notes
Never modify donor NFC cards.
Preserve original NFC information.
Record every NFC scan.
Validate duplicate UID.
Keep UID unique in database.
Maintain audit logs for every transaction.
Future Roadmap

Phase 1

NFC Registration
Farmer Mapping

Phase 2

Seed Distribution
Fertilizer Distribution

Phase 3

Harvest Purchasing
Production Lot

Phase 4

GIS Integration
Polygon Verification

Phase 5

Blockchain Event Logging

Phase 6

AI Analytics
Farmer Dashboard
Production Prediction
Development Notes

Current implementation follows the principle:

NFC Card → Internal Mapping → Farmer → Transaction → Traceability

This design allows the organization to use donor-issued NFC cards without modifying their original contents while maintaining a fully independent internal information system.

The architecture is scalable and intended to support future expansion into enterprise traceability, GIS integration, blockchain event recording, and AI-assisted decision support.
