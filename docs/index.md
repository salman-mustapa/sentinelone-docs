---
description: Deskripsi Singkat Terkait Dengan Sentinel One
---

# Pengenalan SentinelOne

!!! info "Informasi"
    Disini akan membahas secara rinci dan lengkap serta implementasi langsung penggunaan [SentinelOne](https://sentinelone.com). Sebelumnya saya juga sudah membuat dokumentasi serupa [disini](https://salman-mustapa.github.io/s1-docs) terkait dengan setup, command, dan lainnya secara umum.

### 1. Apa itu SentinelOne

SentinelOne adalah platform keamanan endpoint berbasis AI (EDR/XDR) yang di rancang untuk mendeteksi, mencegah dan merespon ancaman siber secara otomatis.

SentinelOne bekerja secara proaktif dengan memanfaatkan analisis perilaku dan kecerdasan buatan (Purple AI), sehingga dapat menghentikan serangan zero-day dan malware tanpa file yang sering lolos dari solusi konvensional

**Fitur utama:**

* **Behavior-based Detection** – Mendeteksi ancaman berdasarkan pola perilaku, bukan hanya tanda tangan (signature).
* **Automated Response** – Mengisolasi (Quarantine), memblokir(Kill), dan memperbaiki sistem tanpa intervensi manual.
* **Cross-platform Support** – Mendukung Windows, macOS, dan Linux.
* **Ransomware Rollback** – Mengembalikan file yang terenkripsi ransomware ke kondisi sebelum serangan.
* **Threat Hunting** – Memungkinkan analisis forensik mendalam.
* **Network Discovery -** Mendeteksi dan Memetakkan jaringan, layanan, dan koneksi yang ada dalam segementasi jaringan yang sama.
* &#x20;**Event Search -** Menelurusi semua proses dan kejadian (event) yang ada di endpoint dan menggabungkannya kedalam console

### 2. Arsitektur & Komponen

SentinelOne terdiri dari beberapa komponen utama:

```mermaid

flowchart TD

sentinelconsole[SentinelOne Console]
endpoint[Endpoint Windows / Linux / macOS]
event[Event Search]
vuln[Vulnerability Scan]
hunting[Threat Hunting]
protection[Kill & Quarantine]
network[Network Discovery]
rollback[Rollback]

sentinelconsole --> endpoint
endpoint --> event
endpoint --> vuln
endpoint --> hunting
endpoint --> protection
endpoint --> network
endpoint -->|Only Windows| rollback

%% Style untuk warna node
style sentinelconsole fill:#0366d6,stroke:#fff,stroke-width:2px,color:#fff
style endpoint fill:#fee597,stroke:#fff,stroke-width:2px,color:#fff

%% Monitoring
style event fill:#1f77b4,stroke:#fff,stroke-width:2px,color:#fff
style vuln fill:#1f77b4,stroke:#fff,stroke-width:2px,color:#fff
style network fill:#1f77b4,stroke:#fff,stroke-width:2px,color:#fff

%% Threat Hunting
style hunting fill:#ff7f0e,stroke:#fff,stroke-width:2px,color:#fff

%% Protection
style protection fill:#d62728,stroke:#fff,stroke-width:2px,color:#fff

%% Recovery
style rollback fill:#2ca02c,stroke:#fff,stroke-width:2px,color:#fff

```

* **Node biru** → fitur observasi & analisis (Event Search, Vulnerability Scan, Network Discovery)
* **Node oranye** → fitur hunting ancaman
* **Node merah** → tindakan proteksi langsung
* **Node hijau** → pemulihan sistem

### 3. Alur Proses SentinelOne

```mermaid

sequenceDiagram

participant M as Management Console
participant E as Endpoint
participant C as Cloud AI

M->>E: Aktivitas sistem (process, file, network)
E->>E: Analisis perilaku & deteksi ancaman
E-->>M: Kirim alert & log
M-->>C: Query threat intelligence
C-->>M: Hasil analisis
M-->>E: Instruksi tindakan (kill & quarantine / rollback)
E-->>M: Simpan dan Kirim Log Activitas

```

!!! info "Informasi"
    ini hanyalah analogi dasar dari cara kerja SentinelOne, mulai dari pemantauan aktivitas endpoint, analisis ancaman secara otomatis, hingga pengambilan tindakan respons dan pemulihan. Setiap komponen berperan dalam memastikan keamanan sistem secara menyeluruh dan terintegrasi.