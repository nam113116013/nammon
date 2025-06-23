<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <title>เกมจับคู่ระบบต่อมไร้ท่อ</title>
  <link href="https://fonts.googleapis.com/css2?family=Sarabun:wght@400;700&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Sarabun', sans-serif;
      background: linear-gradient(to right, #a1c4fd, #c2e9fb);
      text-align: center;
      margin: 0;
      padding: 0;
    }
    h1 {
      color: #2b4c7e;
      margin: 30px 0;
    }
    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
      gap: 15px;
      max-width: 800px;
      margin: 0 auto 50px;
      padding: 0 20px;
    }
    .card {
      background: linear-gradient(to bottom, #ffffff, #d4e9f7);
      border: 2px solid #0077b6;
      border-radius: 12px;
      height: 100px;
      cursor: pointer;
      font-size: 14px;
      font-weight: bold;
      color: transparent;
      display: flex;
      justify-content: center;
      align-items: center;
      transition: all 0.3s ease;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    }
    .card.revealed {
      background: #caf0f8;
      color: #03045e;
    }
    .card.matched {
      background: #90e0ef !important;
      color: #000;
      box-shadow: 0 0 10px 3px gold;
      cursor: default;
    }
    #message {
      font-size: 20px;
      font-weight: bold;
      margin-top: 20px;
      color: #007f5f;
    }
  </style>
</head>
<body>
  <h1>🧠 เกมจับคู่ต่อมไร้ท่อ: Endocrine Match!</h1>
  <div class="grid" id="gameBoard"></div>
  <div id="message"></div>

  <script>
    const pairs = [
      ['ต่อมใต้สมอง', 'ฮอร์โมนโปรแลคติน'],
      ['ต่อมหมวกไต', 'ฮอร์โมนอีพิเนฟริน'],
      ['ต่อมไทรอยด์', 'ฮอร์โมนไทรอกซิน'],
      ['ต่อมพาราไทรอยด์', 'ควบคุมแคลเซียม'],
      ['ต่อมไพเนียล', 'ฮอร์โมนเมลาโทนิน'],
      ['รก', 'ฮอร์โมนเอสโตรเจน'],
    ];

    let cards = [];
    pairs.forEach(pair => {
      cards.push({ text: pair[0], id: pair[1] });
      cards.push({ text: pair[1], id: pair[1] });
    });
    cards = cards.sort(() => 0.5 - Math.random());

    const board = document.getElementById('gameBoard');
    const message = document.getElementById('message');
    let selected = [];
    let matchedCount = 0;

    cards.forEach((card) => {
      const div = document.createElement('div');
      div.className = 'card';
      div.dataset.id = card.id;
      div.innerText = card.text;
      div.onclick = () => selectCard(div);
      board.appendChild(div);
    });

    function selectCard(card) {
      if (card.classList.contains('matched') || card.classList.contains('revealed') || selected.length >= 2) return;

      card.classList.add('revealed');
      selected.push(card);

      if (selected.length === 2) {
        setTimeout(() => {
          if (selected[0].dataset.id === selected[1].dataset.id) {
            selected.forEach(c => c.classList.add('matched'));
            matchedCount++;
            if (matchedCount === pairs.length) {
              message.innerText = '🎉 ยินดีด้วย! คุณจับคู่ได้ครบทั้งหมดแล้ว!';
            }
          } else {
            selected.forEach(c => c.classList.remove('revealed'));
          }
          selected = [];
        }, 800);
      }
    }
  </script>
</body>
</html>
