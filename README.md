<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8">
  <title>Otobüs Takip Demo</title>
  <style>
    body { font-family: Arial; padding: 20px; }
    select, button { padding: 10px; margin: 10px 0; }
    #sonuc { font-size: 20px; margin-top: 20px; }
  </style>
</head>
<body>

<h2>🚌 Otobüs Takip Sistemi</h2>

<label>Durak Seç:</label><br>
<select id="durakSec">
  <option value="0">Başlangıç</option>
  <option value="1">Hal Durağı</option>
  <option value="2">Merkez</option>
  <option value="3">Son Durak</option>
</select>

<br>
<button onclick="hesapla()">Kaç Dakika?</button>

<div id="sonuc"></div>

<script>
// Duraklar (sıralı)
const duraklar = [
  {ad: "Başlangıç", mesafe: 0},
  {ad: "Hal Durağı", mesafe: 2},
  {ad: "Merkez", mesafe: 5},
  {ad: "Son Durak", mesafe: 8}
];

// Otobüs başlangıçta 0 km'de
let busMesafe = 0;

// Her saniye otobüs ilerlesin (simülasyon)
setInterval(() => {
  busMesafe += 0.05; // km
  if (busMesafe > 8) busMesafe = 0;
}, 1000);

function hesapla() {
  const secilenIndex = document.getElementById("durakSec").value;
  const hedef = duraklar[secilenIndex];

  if (busMesafe >= hedef.mesafe) {
    document.getElementById("sonuc").innerText = "Otobüs durağı geçti 🚫";
    return;
  }

  let kalanMesafe = hedef.mesafe - busMesafe;

  let hiz = 30; // km/h

  let sure = (kalanMesafe / hiz) * 60;

  document.getElementById("sonuc").innerText =
    hedef.ad + " → " + Math.round(sure) + " dk";
}
</script>

</body>
</html>