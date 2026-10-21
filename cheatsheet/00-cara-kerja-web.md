# Cheat sheet: Cara kerja web

Fase 0 · lulus 2026-10-21

## Alur dari ketik URL sampai halaman muncul

```
① DNS        ubah nama domain jadi IP address
② Sambung    browser menyambung ke server di IP itu (https = sambungan dienkripsi)
③ Request    browser kirim permintaan: "GET /pesanan"
④ Response   server balas: status code + isi (HTML)
⑤ Tambahan   browser baca HTML, lalu request lagi untuk CSS, JS, gambar
⑥ Render     browser menyusun semuanya jadi halaman
```

Satu kalimat: **DNS → request → response → file tambahan → render.**

## Istilah + analogi depot air

| Istilah | Arti | Analogi |
|---|---|---|
| Browser | Program untuk membuka web (Chrome, dll.) | Pelanggan |
| Server | Komputer yang menyimpan dan mengirim halaman | Depot |
| DNS | Pengubah nama domain jadi IP | Buku kontak |
| IP address | Alamat asli server, berupa angka | Nomor HP depot |
| Request | Permintaan dari browser | Pesan WA "mau 2 galon" |
| Response | Jawaban dari server | Balasan + galon diantar |

## Bagian URL

```
https://tirta-agung.com/pesanan?id=12
└─┬─┘   └──────┬──────┘└──┬───┘└─┬──┘
protokol    domain       path   query
```

## Method HTTP

| Method | Arti | Contoh di Tirta Agung |
|---|---|---|
| `GET` | **Ambil** data | Melihat daftar pesanan |
| `POST` | **Kirim** data baru | Membuat pesanan baru |
| `PATCH` | Ubah sebagian | Ubah jumlah galon |
| `DELETE` | Hapus | Batalkan pesanan |

Jembatan keledai: **GET = ambil, POST = kirim.**

## Status code

| Kode | Arti | Analogi |
|---|---|---|
| 2xx (200) | Berhasil | Galon diantar |
| 3xx (301, 302) | Dialihkan | "Depot pindah ke jalan sebelah" |
| 4xx (404, 401, 403) | Salah di sisi peminta | "Barang itu tidak dijual" / "bukan pelanggan" |
| 5xx (500) | Salah di sisi server | Mesin depot rusak |

## Jangan tertukar

- **404** = server menjawab, tapi halamannya tidak ada.
- **Error DNS** (`DNS_PROBE_FINISHED_NXDOMAIN`) = domain tidak ditemukan, server tidak pernah dihubungi,
  jadi **tidak ada status code**.

## Cara melihatnya sendiri

Chrome → **F12** → tab **Network** → reload. Klik baris pertama → **Headers** (URL, method, status)
dan **Response** (HTML mentah). Kolom **Type** menunjukkan jenis file: `document`, `stylesheet`,
`script`, `png`/`jpeg`.
