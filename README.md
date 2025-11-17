<!DOCTYPE html>
<html lang="kk">
<head>
  <meta charset="UTF-8">
  <title>Ақпарат өлшемдерін түрлендіру</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      min-height: 100vh;
      background: #cce0ff;
      margin: 0;
      padding: 10px;
    }

    h1 {
      color: #003366;
      margin-bottom: 20px;
      text-align: center;
      font-size: 2rem;
    }

    div.calculator {
      background: #004080;
      padding: 30px 40px;
      border-radius: 20px;
      box-shadow: 0 8px 25px rgba(0,0,0,0.2);
      display: flex;
      flex-direction: column;
      align-items: center;
      color: #ffffff;
      width: 100%;
      max-width: 450px;
    }

    input, select, button {
      padding: 15px;
      margin: 10px 0;
      font-size: 1.2rem;
      border-radius: 10px;
      border: none;
      width: 100%;
      box-sizing: border-box;
    }

    button {
      background-color: #007BFF;
      color: white;
      cursor: pointer;
      font-weight: bold;
      transition: 0.3s;
    }

    button:hover {
      background-color: #0056b3;
    }

    p {
      margin-top: 20px;
      font-weight: bold;
      white-space: pre-line;
      text-align: left;
      font-size: 1.1rem;
    }

    @media (max-width: 500px) {
      h1 { font-size: 1.5rem; }
      input, select, button { font-size: 1rem; padding: 12px; }
      p { font-size: 1rem; }
      div.calculator { padding: 20px 25px; }
    }
  </style>
</head>
<body>

<h1>Ақпарат өлшемдерін түрлендіру</h1>

<div class="calculator">
  <input id="v" type="number" placeholder="Мәнді енгізіңіз">
  <select id="u">
    <option value="bit">бит</option>
    <option value="B">байт</option>
    <option value="KB">КБ</option>
    <option value="MB" selected>МБ</option>
    <option value="GB">ГБ</option>
  </select>
  <button onclick="c()">Есептеу</button>
  <p id="r"></p>
</div>

<script>
function c() {
  let v = parseFloat(document.getElementById('v').value),
      u = document.getElementById('u').value;

  if (isNaN(v) || v < 0) { r.innerText = 'Мәнді дұрыс енгізіңіз'; return; }

  let steps = '';
  let bytes;

  switch(u) {
    case 'bit':
      bytes = v / 8;
      steps += `${v} бит ÷ 8 = ${bytes} байт`;
      break;
    case 'B':
      bytes = v;
      steps += `${v} байт`;
      break;
    case 'KB':
      bytes = v * 1024;
      steps += `${v} КБ × 1024 = ${bytes} байт`;
      break;
    case 'MB':
      let kb = v * 1024;
      bytes = kb * 1024;
      steps += `${v} МБ × 1024 = ${kb} КБ\n`;
      steps += `${kb} КБ × 1024 = ${bytes} байт`;
      break;
    case 'GB':
      let mb = v * 1024;
      let kb2 = mb * 1024;
      bytes = kb2 * 1024;
      steps += `${v} ГБ × 1024 = ${mb} МБ\n`;
      steps += `${mb} МБ × 1024 = ${kb2} КБ\n`;
      steps += `${kb2} КБ × 1024 = ${bytes} байт`;
      break;
  }

  r.innerText = steps;
}
</script>

</body>
</html>
