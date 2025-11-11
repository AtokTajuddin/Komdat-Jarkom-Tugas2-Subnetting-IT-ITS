# LAPORAN TUGAS2 Subnetting Komdat & Jarkom

| Nama                    | NRP        |
| ----------------------- | ---------- |
| Mochammad Atha Tajuddin | 5027241093 |

---

# Jaringan LAN & WAN dengan VLSM dan Supernetting

## Deskripsi Proyek

IP Prefix : 10.(NRP mod 256).0.0.
IP Saya : 10.133.0.0

Repository ini berisi Tugas2 Subnetting Mata Kuliah Komdat&Jarkom dan simulasi topologi jaringan **Kantor Pusat dan Cabang** menggunakan **Cisco Packet Tracer (CPT)**.  
Topologi ini menerapkan konsep **VLSM (Variable Length Subnet Mask)** dan **CIDR/Supernetting** untuk mengoptimalkan penggunaan IP Address dalam jaringan LAN dan WAN.

Tujuan utama:

- Membuat segmentasi jaringan berdasarkan divisi.
- Mengimplementasikan koneksi antar-router dengan subnet efisien (/30).
- Melakukan routing dinamis menggunakan **OSPF**.
- Menerapkan **supernetting (CIDR)** untuk merangkum seluruh LAN ke dalam satu alamat agregat `10.133.0.0/22`.

---

## Topologi Jaringan

### Struktur Umum

![[Gambar_1.png]](images/Gambar_1.png)

Setiap router divisi terhubung ke **switch dan PC masing-masing** sebagai LAN lokal.

- Semua router berkomunikasi via **Switch Core (Switch1)** menggunakan subnet transit `10.133.254.0/24`.
- Koneksi WAN antara **Kantor Pusat ↔ Cabang** menggunakan subnet `10.133.255.0/30`.

---

## Alokasi IP Address

| Perangkat                | Interface | Alamat IP    | Subnet Mask     | Fungsi             |
| ------------------------ | --------- | ------------ | --------------- | ------------------ |
| Router_Sekretariat       | G0/0      | 10.133.0.1   | 255.255.254.0   | LAN Sekretariat    |
| Router_Kurikulum         | G0/0      | 10.133.2.1   | 255.255.255.0   | LAN Kurikulum      |
| Router_Guru_Tendik       | G0/0      | 10.133.3.1   | 255.255.255.128 | LAN Guru & Tendik  |
| Router_Sarpras           | G0/0      | 10.133.3.129 | 255.255.255.192 | LAN Sarpras        |
| Router_Pengawas          | G0/0      | 10.133.3.193 | 255.255.255.224 | LAN Pengawas       |
| Router_Server_Admin      | G0/0      | 10.133.3.225 | 255.255.255.248 | LAN Server & Admin |
| Edge_Router_Kantor_Pusat | S0/0/0    | 10.133.255.1 | 255.255.255.252 | Ke Router Cabang   |
| Router_Pool_Cabang       | S0/0/0    | 10.133.255.2 | 255.255.255.252 | Ke Kantor Pusat    |
| Router_Pool_Cabang       | G0/0      | 10.133.4.1   | 255.255.255.224 | LAN Cabang         |

### CIDR / Supernetting Summary

- Semua jaringan LAN diringkas menjadi **10.133.0.0/22**
- Jaringan WAN menggunakan **10.133.255.0/24 (pool /30 link)**

---
