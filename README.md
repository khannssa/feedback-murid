<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Feedback Murid</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; }
    label { display: block; margin-top: 10px; }
    select, input, button { padding: 5px; margin-top: 5px; }
    table {
      width: 100%; 
      border-collapse: collapse; 
      margin-top: 20px;
    }
    table, th, td {
      border: 1px solid #ccc; 
      padding: 10px;
    }
    th { background: #f4f4f4; }
    #feedback { margin-top: 20px; }
  </style>
</head>
<body>
  <h2>Program Feedback Murid</h2>

  <!-- Pilih Nama Siswa -->
  <label for="nama">Pilih Nama Siswa:</label>
  <select id="nama">
    <option value="">-- pilih siswa --</option>
    <option value="Inara">Inara</option>
    <option value="Kenar">Kenar</option>
    <option value="Davi">Davi</option>
  </select>

  <!-- Pilih Tanggal -->
  <label for="tanggal">Pilih Tanggal Kelas:</label>
  <input type="date" id="tanggal">

  <button onclick="tampilkanFeedback()">Lihat Feedback</button>

  <div id="feedback"></div>

  <script>
    // Database feedback sederhana
    const feedbackData = {
      "Inara": {
        "2025-08-25": {
          materi: "Belajar Nested Conditional (Berkondisi Bersarang) di Python",
          catatan: "Jennifer sudah memahami nested conditional, hanya perlu perbaikan indentasi.",
          skor: "4/5",
          youtube: "https://www.youtube.com/watch?v=rfscVS0vtbw"
        },
        "2025-08-23": {
          materi: "Membuat desain balapan dengan scripting tombol mobil",
          catatan: "Inara sudah bisa membuat tombol muncul mobil dengan scripting.",
          skor: "3.5/5",
          youtube: "https://www.youtube.com/watch?v=apACNr7DC_s"
        }
      },
      "Kenar": {
        "2025-08-25": {
          materi: "Membuat NPC bergerak ke beberapa titik",
          catatan: "Kenar berhasil scripting NPC dengan jalur berbeda.",
          skor: "4/5",
          youtube: "https://www.youtube.com/watch?v=j9_2J1k46s0"
        }
      },
      "Davi": {
        "2025-08-25": {
          materi: "Arcade Simulator dengan pesawat bergerak",
          catatan: "Pesawat bisa bergerak, perlu perbaikan kontrol.",
          skor: "3.5/5",
          youtube: "https://www.youtube.com/watch?v=ZnuwB35GYMY"
        }
      }
    };

    function tampilkanFeedback() {
      const nama = document.getElementById("nama").value;
      const tanggal = document.getElementById("tanggal").value;
      const feedbackDiv = document.getElementById("feedback");

      if (!nama || !tanggal) {
        feedbackDiv.innerHTML = "⚠️ Silakan pilih nama siswa dan tanggal kelas.";
        return;
      }

      // Cegah akses tanggal ke depan
      const today = new Date().toISOString().split("T")[0];
      if (tanggal > today) {
        feedbackDiv.innerHTML = "⛔ Feedback untuk tanggal kedepan belum tersedia.";
        return;
      }

      const feedback = feedbackData[nama]?.[tanggal];
      if (feedback) {
        feedbackDiv.innerHTML = `
          <table>
            <tr><th>Nama Siswa</th><td>${nama}</td></tr>
            <tr><th>Tanggal</th><td>${tanggal}</td></tr>
            <tr><th>Materi</th><td>${feedback.materi}</td></tr>
            <tr><th>Catatan</th><td>${feedback.catatan}</td></tr>
            <tr><th>Skor</th><td>${feedback.skor}</td></tr>
            <tr><th>Video Pembelajaran</th>
              <td><a href="${feedback.youtube}" target="_blank">📺 Lihat di YouTube</a></td>
            </tr>
          </table>
        `;
      } else {
        feedbackDiv.innerHTML = `❌ Tidak ada feedback untuk ${nama} pada tanggal ${tanggal}.`;
      }
    }
  </script>
</body>
</html>
