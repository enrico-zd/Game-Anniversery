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

## Catatan
- Mode online berdua dan papan pesan memakai fitur artifact Claude, jadi hanya aktif saat dibuka sebagai artifact di claude.ai. Di GitHub Pages atau server lain, game tetap bisa dimainkan sendiri (pasangan dikendalikan komputer), tapi tanpa mode online dan tanpa papan pesan bersama.
- Repo ini berisi foto pribadi. Jika repo dibuat **public**, siapa pun bisa melihat fotonya.
