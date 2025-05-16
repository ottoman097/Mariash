# Mariash
calculator for a popular europian card game Mariáš
<!DOCTYPE html>
<html lang="cs">
<head>
  <meta charset="UTF-8">
  <title>Mariáš kalkulačka</title>
  <style>
    body { font-family: Arial; max-width: 600px; margin: auto; padding: 20px; }
    label, select, input, button { margin: 10px 0; display: block; }
    h1, h2, h3 { margin-top: 20px; }
  </style>
</head>
<body>
  <h1>Kalkulačka pro licitovaný mariáš</h1>

  <!-- Výběr tarifu -->
  <label for="tarif">Typ mariáše:</label>
  <select id="tarif">
    <option value="10">Desetníkový (10 haléřů)</option>
    <option value="25">Čtvrtkový (25 haléřů)</option>
    <option value="50">Půlkový (50 haléřů)</option>
    <option value="100">Korunový (1 Kč)</option>
  </select>

  <!-- Výběr trumfů (německé barvy) -->
  <label for="trumf">Trumfová barva (německý typ):</label>
  <select id="trumf">
    <option value="none">Bez trumfů</option>
    <option value="zaludy">Žaludy 🌰</option>
    <option value="zelene">Zelené 🍃</option>
    <option value="cervene">Červené ❤️</option>
    <option value="kulove">Kulové ⚪</option>
  </select>

  <!-- Typy her -->
  <label>Typy her (zaškrtněte vše, co hráč hrál):</label>
  <input type="checkbox" id="hra" /> Hra
  <input type="checkbox" id="stovka" /> Stovka
  <input type="checkbox" id="sedma" /> Sedma
  <input type="checkbox" id="lepsiSedma" /> Lepší sedma
  <input type="checkbox" id="stoSedm" /> Sto sedm
  <input type="checkbox" id="lepsiStoSedm" /> Lepší sto sedm
  <input type="checkbox" id="betl" /> Betl
  <input type="checkbox" id="durch" /> Durch

  <!-- Fleky -->
  <label for="flekHra">Flek na hru:</label>
  <select id="flekHra">
    <option value="1">Bez fleku</option>
    <option value="2">Flek</option>
    <option value="4">Re</option>
    <option value="8">Tutti</option>
  </select>

  <label for="flekStovka">Flek na stovku:</label>
  <select id="flekStovka">
    <option value="1">Bez fleku</option>
    <option value="2">Flek</option>
    <option value="4">Re</option>
    <option value="8">Tutti</option>
  </select>

  <label for="flekBonus">Flek na sedmu/107:</label>
  <select id="flekBonus">
    <option value="1">Bez fleku</option>
    <option value="2">Flek</option>
    <option value="4">Re</option>
    <option value="8">Tutti</option>
  </select>

  <label for="flekBetlDurch">Flek na betl/durch:</label>
  <select id="flekBetlDurch">
    <option value="1">Bez fleku</option>
    <option value="2">Flek</option>
    <option value="4">Re</option>
    <option value="8">Tutti</option>
  </select>

  <button onclick="spocitej()">Spočítej</button>

  <h2>Výsledek: <span id="vysledek">-</span></h2>
  <h3>Trumf: <span id="trumfZobrazit">-</span></h3>

  <script>
    function spocitej() {
      const tarif = parseInt(document.getElementById("tarif").value);

      // Hry
      const hra = document.getElementById("hra").checked;
      const stovka = document.getElementById("stovka").checked;
      const sedma = document.getElementById("sedma").checked;
      const lepsiSedma = document.getElementById("lepsiSedma").checked;
      const stoSedm = document.getElementById("stoSedm").checked;
      const lepsiStoSedm = document.getElementById("lepsiStoSedm").checked;
      const betl = document.getElementById("betl").checked;
      const durch = document.getElementById("durch").checked;

      // Fleky
      const flekHra = parseInt(document.getElementById("flekHra").value);
      const flekStovka = parseInt(document.getElementById("flekStovka").value);
      const flekBonus = parseInt(document.getElementById("flekBonus").value);
      const flekBetlDurch = parseInt(document.getElementById("flekBetlDurch").value);

      let celkem = 0;

      if (hra) celkem += tarif * 1 * flekHra;
      if (stovka) celkem += tarif * 2 * flekStovka;
      if (sedma) celkem += tarif * 1 * flekBonus;
      if (lepsiSedma) celkem += tarif * 2 * flekBonus;
      if (stoSedm) celkem += tarif * 3 * flekBonus;
      if (lepsiStoSedm) celkem += tarif * 4 * flekBonus;
      if (betl) celkem += tarif * 5 * flekBetlDurch;
      if (durch) celkem += tarif * 10 * flekBetlDurch;

      document.getElementById("vysledek").textContent = celkem + " haléřů";

      // Zobrazení trumfu
      const trumf = document.getElementById("trumf").value;
      let trumfText = "-";
      if (trumf === "zaludy") trumfText = "Žaludy 🌰";
      else if (trumf === "zelene") trumfText = "Zelené 🍃";
      else if (trumf === "cervene") trumfText = "Červené ❤️";
      else if (trumf === "kulove") trumfText = "Kulové ⚪";
      else trumfText = "Bez trumfů";

      document.getElementById("trumfZobrazit").textContent = trumfText;
    }
  </script>
</body>
</html>
