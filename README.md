# Museum Anniversary — Enrico & Nala

Museum 3D kecil untuk anniversary kami. Dibuka langsung di browser, bisa di laptop maupun HP.

## Isi folder
- `index.html` — seluruh game (Three.js dimuat dari CDN jsDelivr)
- `models/` — karakter (Quaternius Modular Men & Women, CC0), disimpan sebagai base64
- `photos/` — foto galeri (`foto-01` … `foto-11`) dan dua foto di samping kue (`kue-kiri`, `kue-kanan`)
- `audio/atap.mp3` — lagu rooftop
- `sfx/` — efek suara (langkah parket dari rekaman sendiri, sisanya Kenney, CC0)

## Menjalankan
Harus lewat server web, bukan dibuka langsung sebagai file (`file://`), karena foto, model, dan suara dimuat dengan `fetch`.

```bash
cd folder-ini
python3 -m http.server 8000
# buka http://localhost:8000
```

## GitHub Pages
Settings → Pages → Source: *Deploy from a branch* → `main` / root. Situs akan tersedia di `https://<username>.github.io/<nama-repo>/`.

## Mode online di luar Claude
Di claude.ai, mode online berdua dan papan pesan memakai fitur artifact Claude. Di GitHub Pages, Netlify, atau server lain, keduanya memakai **Firebase Realtime Database + Anonymous Auth**. Kalau Firebase belum diatur (atau tidak ada kode ruang), game tetap jalan sendiri (pasangan dikendalikan komputer).

1. Buat project di [console.firebase.google.com](https://console.firebase.google.com).
2. Aktifkan **Realtime Database** (lokasi `asia-southeast1`) dan **Authentication → Sign-in method → Anonymous**.
3. **Project settings → Your apps → Web app**, salin `firebaseConfig` ke `CONFIG.online.firebase` di bagian atas `index.html`, misalnya:
   ```js
   online: {
     firebase: { apiKey: '...', authDomain: '...', databaseURL: 'https://...asia-southeast1.firebasedatabase.app', projectId: '...', appId: '...' },
     room: ''
   }
   ```
   `databaseURL` wajib ada. (Config web Firebase memang publik; keamanannya dijaga oleh aturan di langkah 4.)
4. Buka **Realtime Database → Rules**, hapus isinya, tempel isi `database.rules.json`, lalu **Publish**.
5. Kalau pakai domain sendiri atau GitHub Pages, tambahkan domainnya (mis. `enrico-zd.github.io`) di **Authentication → Settings → Authorized domains**.
6. Bagikan link dengan kode ruang, misalnya `https://enrico-zd.github.io/Game-Anniversery/?ruang=enrico-nala-xxxx`. Kode ruang hanya boleh huruf kecil, angka, dan `-` (maks. 40 karakter). Tanpa `?ruang=`, dipakai `CONFIG.online.room`; kalau keduanya kosong, game jalan sendiri.

Siapa pun yang tahu kode ruang bisa masuk ke ruang itu dan membaca papan pesannya, jadi pakai kode yang sulit ditebak.

### Menguji
1. `python3 -m http.server 8000`
2. Buka `http://localhost:8000/?ruang=tes-123` di dua jendela (satu normal, satu incognito).
3. Pilih karakter berbeda; gerakan, duduk, makan/minum, potong kue, lagu rooftop, dan papan pesan akan tersinkron.

## Catatan
- Repo ini berisi foto pribadi. Jika repo dibuat **public**, siapa pun bisa melihat fotonya.
