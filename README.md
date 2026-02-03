# Soalan
Hasil produksi dan capaian
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <title>Pencapaian Karyawan</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            padding: 20px;
        }
        table {
            border-collapse: collapse;
            width: 100%;
            margin-bottom: 40px;
        }
        th, td {
            border: 1px solid #ccc;
            padding: 8px;
            text-align: center;
        }
        th {
            background: #f0f0f0;
        }
        .warning {
            color: red;
            font-weight: bold;
        }
    </style>
</head>
<body>

<h2>Tabel Pencapaian Karyawan</h2>

<table id="tabel">
    <thead>
        <tr>
            <th>Nama</th>
            <th>Target</th>
            <th>Output</th>
            <th>Pencapaian (%)</th>
        </tr>
    </thead>
    <tbody></tbody>
</table>

<h2>Grafik Pencapaian</h2>
<canvas id="grafik"></canvas>

<h2>Notifikasi (≤ 50%)</h2>
<ul id="notif"></ul>

<script>
// ================= DATA =================
const data = [
    { nama: "Abdul", target: 1000000, output: 960000 },
    { nama: "Budi", target: 1000000, output: 420000 },
    { nama: "Beni", target: 1000000, output: 1100000 },
    { nama: "Rian", target: 1000000, output: 950000 },
    { nama: "Romi", target: 1000000, output: 1000500 },
    { nama: "Farhan", target: 1000000, output: 550000 },
    { nama: "Krisna", target: 1000000, output: 953000 },
    { nama: "Fajar", target: 1000000, output: 1053000 },
    { nama: "Heri", target: 1000000, output: 876300 },
    { nama: "Nopri", target: 1000000, output: 300000 },
    { nama: "Dermawan", target: 1000000, output: 989000 }
];

// ================= HITUNG & SORT =================
data.forEach(d => {
    d.persen = ((d.output / d.target) * 100).toFixed(2);
});

data.sort((a, b) => b.persen - a.persen);

// ================= TABEL =================
const tbody = document.querySelector("#tabel tbody");

data.forEach(d => {
    const tr = document.createElement("tr");
    tr.innerHTML = `
        <td>${d.nama}</td>
        <td>${d.target.toLocaleString()}</td>
        <td>${d.output.toLocaleString()}</td>
        <td>${d.persen}%</td>
    `;
    tbody.appendChild(tr);
});

// ================= GRAFIK =================
new Chart(document.getElementById("grafik"), {
    type: "bar",
    data: {
        labels: data.map(d => d.nama),
        datasets: [{
            label: "Pencapaian (%)",
            data: data.map(d => d.persen)
        }]
    }
});

// ================= NOTIFIKASI =================
const notif = document.getElementById("notif");

data.forEach(d => {
    if (d.persen <= 50) {
        const li = document.createElement("li");
        li.className = "warning";
        li.innerText = `⚠ ${d.nama} hanya mencapai ${d.persen}% (Kirim Email/SMS)`;
        notif.appendChild(li);
    }
});
</script>

</body>
</html>
