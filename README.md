<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Barcode & QR Code Scanner</title>
</head>
<body>
<h2>Scan Barcode / QR Code or Enter Manually</h2>

<!-- Video for scanning -->
<video id="preview" width="400" height="300"></video>
<p id="result">Scanning...</p>

<!-- Manual input -->
<input type="text" id="manualInput" placeholder="Enter text or number">
<button id="submitBtn">Submit</button>
<p id="status"></p>

<script type="module">
import QrScanner from "https://cdn.jsdelivr.net/npm/qr-scanner@1.4.2/qr-scanner.min.js";

const video = document.getElementById('preview');
const resultElement = document.getElementById('result');
const manualInput = document.getElementById('manualInput');
const submitBtn = document.getElementById('submitBtn');
const statusElement = document.getElementById('status');

const googleSheetURL = 'https://script.google.com/macros/s/AKfycbzPhyKe0d9FpBvp7qp_0eBiE9f58oU_BBj6kq_LDXnV2KtH5qyiYOthBQciJZHtpEiT/exec';

// Function to send data to Google Sheet
function sendToSheet(data) {
    fetch(googleSheetURL, {
        method: 'POST',
        body: JSON.stringify({ code: data }),
        headers: { 'Content-Type': 'application/json' }
    })
    .then(res => res.json())
    .then(resp => {
        console.log(resp);
        statusElement.textContent = "Sent: " + data;
    })
    .catch(err => {
        console.error(err);
        statusElement.textContent = "Error sending data";
    });
}

// QR / Barcode Scanner
const scanner = new QrScanner(video, result => {
    resultElement.textContent = "Scanned Code: " + result;
    sendToSheet(result);
});
scanner.start();

// Manual input submit
submitBtn.addEventListener('click', () => {
    const value = manualInput.value.trim();
    if (value) {
        sendToSheet(value);
        manualInput.value = ""; // clear input
    } else {
        statusElement.textContent = "Please enter a value";
    }
});
</script>
</body>
</html>
