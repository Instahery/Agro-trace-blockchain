# 🌿 KLUMBAYAN GOLD FARM - CARBON CALCULATION SYSTEM ROADMAP
## Integrasi GIS, Pembelian, Fasilitator, & Blockchain Product Passport

**Periode:** Juli - Agustus 2026 (8 Minggu)  
**Version:** 1.0  
**Last Updated:** 2 Juli 2026  
**Project Lead:** Finance & Operations Manager, KGF  
**Status:** 🟢 Active Development

---

## 📋 TABLE OF CONTENTS

1. [Overview & Objectives](#1-overview--objectives)
2. [Current System Status](#2-current-system-status)
3. [Tech Stack](#3-tech-stack)
4. [System Architecture](#4-system-architecture)
5. [8-Week Timeline](#5-8-week-timeline)
6. [Database Schema](#6-database-schema)
7. [API Endpoints](#7-api-endpoints)
8. [Blockchain Architecture](#8-blockchain-architecture)
9. [Integration Points](#9-integration-points)
10. [Risk Management](#10-risk-management)

---

## 1. OVERVIEW & OBJECTIVES

### 🎯 Vision
Membangun sistem perhitungan karbon **terintegrasi end-to-end** yang menghubungkan:
- 🗺️ **GIS Mapping** (GeoJSON polygon lahan petani)
- 💰 **Pembelian Lada** (first-purchase dari petani)
- 👨‍🌾 **Kegiatan Fasilitator** (monitoring & pendampingan)
- 🔗 **Blockchain Product Passport** (Polygon Amoy/Mainnet)
- 📊 **Carbon Credit Calculation** (Verra VM0047 compliant)
- 🌍 **EUDR Compliance** (EU Deforestation Regulation)

### 📊 Success Metrics
| Metric | Target | Current |
|--------|--------|---------|
| Farmers onboarded | 547 | 547 ✅ |
| Hectares mapped | 892 ha | 892 ha ✅ |
| Carbon calculation accuracy | ±5% | TBD |
| Blockchain transactions | 100% | 0% |
| System uptime | 99.5% | 99% ✅ |
| Response time (API) | <2s | TBD |

### 🏆 Key Deliverables
- [ ] GeoJSON validator (EUDR compliant)
- [ ] Carbon calculator terintegrasi dengan pembelian
- [ ] Product Passport blockchain (Polygon)
- [ ] Batch aggregation untuk ekspor
- [ ] Dashboard analytics real-time
- [ ] Mobile-friendly facilitator app

---

## 2. CURRENT SYSTEM STATUS

### ✅ Yang Sudah Ada (Production)

| File | Fungsi | Status |
|------|--------|--------|
| `data_desa.php` | Dashboard cuaca + AI | ✅ Live |
| `ai_cultivation_guide.php` | AI panduan budidaya (Groq) | ✅ Live |
| `ai_facilitator_agenda.php` | AI agenda fasilitator | ✅ Live |
| `cetak_laporan.php` | Export PDF laporan | ✅ Live |
| `AgroTechKGFChatBot.php` | Chatbot AI | ✅ Live |
| `test_ai_debug.php` | Debug API key | ✅ Live |
| `cache_ai/` | Cache system (1 jam) | ✅ Live |

### 🔧 Yang Perlu Ditambahkan (Roadmap Ini)

| Module | Priority | Timeline |
|--------|----------|----------|
| GeoJSON Validator | 🔴 HIGH | Week 2 |
| Carbon Calculator | 🔴 HIGH | Week 2 |
| Purchase Form Integration | 🔴 HIGH | Week 3 |
| Blockchain Smart Contract | 🟡 MEDIUM | Week 4 |
| Product Passport | 🟡 MEDIUM | Week 5 |
| Batch Aggregation | 🟡 MEDIUM | Week 6 |
| Dashboard Analytics | 🟢 LOW | Week 7 |
| Documentation | 🟢 LOW | Week 8 |

---

## 3. TECH STACK

### Backend
| Component | Technology | Purpose |
|-----------|-----------|---------|
| Language | PHP 8.x | Core business logic |
| Database | MySQL/MariaDB | Data persistence |
| ORM | PDO (Native) | Database abstraction |
| API | RESTful JSON | Integration layer |

### Frontend (Existing)
| Component | Technology | Purpose |
|-----------|-----------|---------|
| Framework | Bootstrap 5.3.2 | UI components |
| Admin Template | Custom dark theme | Dashboard layout |
| JavaScript | jQuery + Vanilla JS | DOM manipulation |
| Charts | Chart.js + Google Charts | Visualization |
| Maps | Leaflet.js 1.9.4 | GIS mapping |
| Icons | Font Awesome 6.5.1 | UI icons |

### Geospatial (NEW)
| Component | Technology | Purpose |
|-----------|-----------|---------|
| Map Library | Leaflet.js | Interactive maps |
| Drawing | Leaflet.draw | Polygon creation |
| Validation | Turf.js (optional) | Geospatial calc |
| Data Format | GeoJSON (RFC 7946) | Polygon storage |
| Tiles | OpenStreetMap | Base map |

### Blockchain (NEW)
| Component | Technology | Purpose |
|-----------|-----------|---------|
| Smart Contract | Solidity ^0.8.20 | Product Passport |
| Web3 Library | Ethers.js 6.x | Blockchain interaction |
| Wallet | MetaMask | User auth |
| Network | Polygon Amoy → Mainnet | Transaction layer |
| IDE | Remix IDE | Contract dev |
| Storage | IPFS (Pinata) | Metadata storage |

### Tools
| Component | Technology | Purpose |
|-----------|-----------|---------|
| Version Control | Git/GitHub | Code management |
| Hosting | cPanel | Production |
| AI Provider | Groq (Llama 3.3) | AI inference |
| Weather API | NASA POWER | Weather data |
| UV API | OpenUV | UV data |

---

## 4. SYSTEM ARCHITECTURE
