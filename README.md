<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <title>Warehouse QR Scanner</title>
    <script src="https://unpkg.com/html5-qrcode"></script>

    <style>
        body {
            margin: 0;
            font-family: 'Segoe UI', sans-serif;
            background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
            color: white;
        }

        header {
            background: #111;
            padding: 20px;
            text-align: center;
            font-size: 24px;
            letter-spacing: 2px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.6);
        }

        .container {
            display: flex;
            justify-content: center;
            gap: 30px;
            padding: 30px;
            flex-wrap: wrap;
        }

        .scanner, .result {
            background: #1c1c1c;
            border-radius: 15px;
            padding: 25px;
            width: 350px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.7);
        }

        .scanner h2, .result h2 {
            text-align: center;
            margin-bottom: 20px;
            border-bottom: 1px solid #333;
            padding-bottom: 10px;
        }

        #reader {
            width: 100%;
        }

        .item {
            margin: 12px 0;
            font-size: 18px;
        }

        .label {
            color: #aaa;
        }

        .status-ok {
            color: #00ff99;
            font-weight: bold;
        }

        .status-reject {
            color: #ff4d4d;
            font-weight: bold;
        }

        footer {
            text-align: center;
            padding: 15px;
            color: #aaa;
            font-size: 14px;
        }
    </style>
</head>

<body>

<header>
    WAREHOUSE QR SCAN SYSTEM
</header>

<div class="container">
    <!-- SCANNER -->
    <div class="scanner">
        <h2>Scan QR Code</h2>
        <div id="reader"></div>
    </div>

    <!-- RESULT -->
    <div class="result">
        <h2>Detail Produk</h2>
        <div class="item"><span class="label">Nama Produk:</span> <span id="nama">-</span></div>
        <div class="item"><span class="label">Berat (KG):</span> <span id="berat">-</span></div>
        <div class="item"><span class="label">Status:</span> <span id="status">-</span></div>
    </div>
</div>

<footer>
    © 2026 Warehouse System | Test Programmer
</footer>

<script>
    function onScanSuccess(decodedText) {
        // Format QR: NAMA|BERAT|STATUS
        const data = decodedText.split("|");

        document.getElementById("nama").innerText = data[0];
        document.getElementById("berat").innerText = data[1] + " KG";

        const statusEl = document.getElementById("status");
        statusEl.innerText = data[2];

        statusEl.className = "";
        if (data[2].toUpperCase() === "OKE") {
            statusEl.classList.add("status-ok");
        } else {
            statusEl.classList.add("status-reject");
        }
    }

    const html5QrCode = new Html5Qrcode("reader");
    html5QrCode.start(
        { facingMode: "environment" },
        { fps: 10, qrbox: 250 },
        onScanSuccess
    );
</script>

</body>
</html>

