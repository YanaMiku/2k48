# 🎮 Merge Puzzle Game

Game puzzle berbasis web dengan mekanik geser dan merge. Gabungkan ubin dengan angka yang sama untuk menciptakan nilai lebih besar dan raih skor tertinggi!

## 📋 Deskripsi Singkat

**Merge Puzzle** adalah game puzzle kasual yang terinspirasi dari mekanik 2048. Mainkan di grid 5×5 dengan menggeser ubin untuk membuatnya berpindah. Ketika dua ubin dengan nilai sama bertemu, mereka akan merge menjadi satu ubin dengan nilai dua kalinya. Tantang dirimu untuk mendapatkan skor setinggi mungkin sebelum grid penuh!

### Fitur Utama
- 🎯 Mekanik geser intuitif (swipe mobile / drag desktop)
- 🔄 Sistem merge otomatis dengan animasi smooth
- 📊 Tracking skor real-time dan penghitung gerakan
- ↩️ Fitur Undo untuk batalkan gerakan terakhir
- 🎨 Desain modern dengan warna gradient unik per nilai
- 📱 Fully responsive (mobile, tablet, desktop)
- ⌨️ Support keyboard (arrow keys)
- 🏁 Deteksi Game Over otomatis

---

## 🚀 Cara Memulai

### Persyaratan
- Browser modern (Chrome, Firefox, Safari, Edge)
- Tidak perlu instalasi atau setup tambahan

### Menjalankan Game
1. Buka file `index.html` di browser favorit, atau
2. Taruh file di web server dan akses melalui URL

```bash
# Jika menggunakan Python 3
python -m http.server 8000
# Lalu buka http://localhost:8000

# Atau menggunakan Node.js
npx http-server
```

---

## 🎮 Cara Bermain

### Kontrol

**Mobile / Touchscreen**
- Geser jari ke **atas** untuk memindahkan semua ubin naik
- Geser jari ke **bawah** untuk memindahkan semua ubin turun
- Geser jari ke **kiri** untuk memindahkan semua ubin ke kiri
- Geser jari ke **kanan** untuk memindahkan semua ubin ke kanan
- Sensitivitas: minimum 30px untuk register gerakan

**Desktop / Laptop**
- **Drag mouse**: Klik + tahan + geser ke arah yang diinginkan
- **Keyboard**: Gunakan tombol panah (↑ ↓ ← →)
- Geser minimum 20px untuk register

### Mekanik Game

1. **Pergerakan Ubin**
   - Semua ubin bergerak ke arah yang sama dalam satu gerakan
   - Ubin akan terus bergerak sampai menghantam tepi grid atau bertemu ubin lain
   - Tidak ada pergerakan per-ubin individual

2. **Merge Mechanic**
   - Ketika dua ubin dengan **nilai sama** bertemu, mereka merge
   - Hasil merge: nilai + nilai = nilai baru (contoh: 1+1→2, 2+2→4)
   - Setiap ubin hanya bisa merge **sekali per gerakan**
   - Merge akan memberikan poin = nilai hasil merge

3. **Spawn Ubin Baru**
   - Setiap gerakan yang valid, **1 ubin baru** akan muncul
   - Nilai baru random: 1 atau 2 (probabilitas sama)
   - Posisi: di slot kosong random
   - Animasi: fade in dengan scale effect

4. **Sistem Skor**
   - Skor bertambah sesuai nilai merge
   - Contoh: merge 4+4=8 menambah 8 poin
   - Skor tidak berkurang (hanya naik)

5. **Game Over**
   - Kondisi: Grid penuh (25/25 slot terisi) AND tidak ada merge possible
   - Deteksi otomatis setelah setiap gerakan
   - Modal akan muncul menampilkan skor akhir dan total gerakan

### Tombol & Fungsi

| Tombol | Fungsi |
|--------|--------|
| **Game Baru** | Reset grid dan mulai permainan baru (skor = 0) |
| **Undo** | Batalkan gerakan terakhir (restore state sebelumnya) |
| **Restart** | Tombol di modal game over untuk main lagi |

---

## 📊 Spesifikasi Teknis

### Grid
- Ukuran: **5 × 5 (25 slot)**
- Rasio: Square cells (aspect-ratio: 1:1)
- Spacing: 8px gap antar cell
- Layout: CSS Grid

### Animasi
- **Spawn**: 0.2s cubic-bezier (spring effect)
- **Merge**: 0.3s ease (bounce effect scale 1.15x)
- **Move**: 0.15s smooth transition

### Warna Per Nilai

| Nilai | Warna | Kontras |
|-------|-------|---------|
| 1 | Warm Tan/Gold | Dark Brown |
| 2 | Golden/Orange | Dark Orange |
| 4 | Light Orange | Dark Orange |
| 8 | Sky Blue | White |
| 16 | Lime Green | White |
| 32 | Pink/Magenta | White |
| 64 | Amber/Gold | White |
| 128 | Teal | White |
| 256 | Purple | White |
| 512 | Red | White |
| 1024 | Coral | White |
| 2048+ | Deep Coral | White |

### JavaScript Architecture

```
Game Class
├── init() - Inisialisasi grid & spawn awal
├── spawn() - Spawn ubin baru di posisi kosong
├── move(direction) - Handle gerakan (up/down/left/right)
├── moveLine(line, forward) - Logika compress → merge → compress
├── isGameOver() - Deteksi kondisi game over
├── showGameOver() - Tampilkan modal hasil akhir
├── undo() - Restore state sebelumnya
├── reset() - Reset game ke kondisi awal
└── render() - Update DOM dengan state terbaru
```

**State Management**
- `grid`: Array[25] nilai ubin (0 = kosong)
- `score`: Total poin akumulatif
- `moves`: Penghitung gerakan valid
- `history`: Stack state untuk undo
- `merged`: Set index ubin yang merge (untuk animasi)

---

## 🎯 Tips & Strategi

### Tips Bermain
1. **Pikirkan Arah** - Setiap gerakan berdampak pada seluruh grid, jadi rencanakan dengan hati-hati
2. **Prioritas Merge** - Fokus pada merge nilai kecil menjadi sedang terlebih dahulu
3. **Manage Empty Space** - Jangan biarkan grid penuh terlalu cepat, pertahankan slot kosong
4. **Undo Wisely** - Gunakan fitur Undo saat melakukan gerakan salah, tidak ada penalty
5. **Pattern Recognition** - Pelajari bagaimana ubin bergerak di setiap arah

### Strategi Lanjutan
- Gunakan undo untuk eksperimen tanpa risiko
- Cobalah buat "lines" (barisan ubin dengan nilai sama) untuk merge besar
- Monitor posisi kosong - jangan biarkan trap spawn di satu sudut
- Optimal skor: capai nilai 2048 atau lebih tinggi

---

## 📁 Struktur File

```
merge-puzzle-game/
├── index.html          # File utama (HTML + CSS + JS)
├── README.md           # Dokumentasi
└── (Opsional)
    ├── style.css       # CSS terpisah
    └── game.js         # JavaScript terpisah
```

**Catatan**: Game ini adalah single-file HTML dengan CSS & JS embedded. Bisa langsung dijalankan tanpa build process.

---

## 🛠️ Customization

### Mengubah Ukuran Grid
Edit pada baris awal JavaScript:
```javascript
const GRID_SIZE = 5;  // Ubah ke 4 atau 6 untuk ukuran lain
```

### Mengubah Nilai Spawn Awal
```javascript
const SPAWN_VALUES = [1, 2];  // Ubah ke nilai yang diinginkan
```

### Mengubah Warna
Edit class CSS `.tile-{value}`:
```css
.tile-8 { 
  background: linear-gradient(135deg, #85B7EB, #378ADD); 
  color: white; 
}
```

### Mengubah Sensitivitas Gesture
**Mobile swipe**:
```javascript
if (Math.abs(dx) > 30) {  // Ubah 30 ke angka lain (pixel)
```

**Desktop drag**:
```javascript
if (Math.abs(dx) > 20 || Math.abs(dy) > 20) {  // Ubah threshold
```

---

## 🐛 Troubleshooting

| Masalah | Solusi |
|---------|--------|
| Swipe tidak terdeteksi | Geser minimal 30px, tunggu event touchend selesai |
| Drag mouse tidak responsif | Pastikan drag minimal 20px sebelum release |
| Layout berantakan | Clear browser cache (Ctrl+Shift+R) |
| Touch events bentrok | Pastikan tidak ada `pointer-events: none` di parent |
| Animasi lambat | Non-critical: buka DevTools, cek GPU acceleration |

---

## 📱 Kompatibilitas

✅ **Browser yang didukung**
- Chrome 60+
- Firefox 55+
- Safari 12+
- Edge 79+
- Opera 47+

✅ **Device**
- Desktop (Windows, Mac, Linux)
- Mobile (iOS, Android)
- Tablet (iPad, Android tablets)

✅ **Input Method**
- Touch (swipe)
- Mouse (drag & click)
- Keyboard (arrow keys)

---

## 📊 Fitur Advanced (Opsional untuk Ekspansi)

Ide untuk development lebih lanjut:
- 🔐 Local Storage - Simpan high score & recent games
- 🏆 Leaderboard - Kompetisi dengan pemain lain
- 🎵 Sound Effects - Audio feedback untuk merge & game over
- ✨ Particle Effects - Visual feedback yang lebih fancy
- 🎨 Themes - Dark mode, light mode, custom theme
- ⏱️ Time Attack - Mode permainan terbatas waktu
- 🤖 AI Bot - AI yang bisa bermain otomatis
- 🌍 Multiplayer - Competitive mode

---

## 📝 Lisensi

Free to use & modify untuk keperluan pribadi maupun komersial.

---

## 🤝 Kontribusi

Punya ide peningkatan? Feel free untuk fork & modify!

**Saran untuk improvement**:
1. Optimize untuk device dengan refresh rate tinggi (120fps)
2. Tambah haptic feedback untuk mobile
3. Implement touch drag visual feedback (preview arah)
4. Optimize memory usage untuk session panjang

---

## 📧 Support & Feedback

Jika menemukan bug atau punya saran, silakan share feedback melalui:
- Testing di berbagai device
- Melaporkan masalah dengan detail
- Saran fitur baru yang menarik

---

**Selamat bermain! Raih skor tertinggi mu!** 🚀🎮

*Last Updated: April 2026*
