# Tic Tac Toe Game

## Deskripsi

Tic Tac Toe adalah permainan sederhana yang diimplementasikan menggunakan HTML, CSS, dan JavaScript. Permainan ini memungkinkan dua pemain untuk bergiliran menandai ruang dalam grid 3x3. Pemain pertama yang berhasil menyusun tiga tanda mereka (baik 'X' atau 'O') secara horizontal, vertikal, atau diagonal akan memenangkan permainan.

## Fitur

- **Desain Responsif**: Permainan dirancang agar responsif dan dapat berfungsi dengan baik di berbagai ukuran layar.
- **Antarmuka Pengguna**: Antarmuka pengguna yang bersih dan sederhana dengan tombol untuk setiap ruang grid dan opsi untuk memulai ulang atau memulai permainan baru.
- **Logika Menang dan Seri**: Permainan memeriksa kondisi kemenangan dan seri, menampilkan pesan yang sesuai.

## Teknologi yang Digunakan

- **HTML**: Untuk struktur permainan.
- **CSS**: Untuk styling antarmuka permainan.
- **JavaScript**: Untuk logika permainan dan interaktivitas.

## Instalasi

1. Clone repositori atau unduh file.
2. Buka `index.html` di browser web Anda.

## Penggunaan

- Klik pada tombol di grid untuk menempatkan tanda Anda ('X' atau 'O').
- Permainan bergiliran antara dua pemain.
- Jika seorang pemain menang, pesan akan ditampilkan yang menunjukkan pemenangnya.
- Anda dapat memulai ulang permainan atau memulai permainan baru menggunakan tombol yang disediakan.

## Kode Sumber

Berikut adalah kode sumber untuk proyek ini:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic Tac Toe</title>
    <link href="https://fonts.googleapis.com/css2?family=Raleway:wght@700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="style.css">
</head>
<body>
   <div class="wrapper">
       <div class="container">
           <button class="button-option"></button>
           <button class="button-option"></button>
           <button class="button-option"></button>
           <button class="button-option"></button>
           <button class="button-option"></button>
           <button class="button-option"></button>
           <button class="button-option"></button>
           <button class="button-option"></button>
           <button class="button-option"></button>
       </div>
       <button id="restart">Restart</button>
   </div>

   <div class="popup hide">
       <p id="message">Sample Message</p>
       <button id="new-game">New Game</button>
   </div>
   
    <script src="script.js"></script>
</body>
</html>

let btnRef = document.querySelectorAll(".button-option");
let popupRef = document.querySelector(".popup");
let newgameBtn = document.getElementById("new-game");
let restartBtn = document.getElementById("restart");
let msgRef = document.getElementById("message");

// Winning Pattern Array
let winningPattern = [
  [0, 1, 2],
  [0, 3, 6],
  [2, 5, 8],
  [6, 7, 8],
  [3, 4, 5],
  [1, 4, 7],
  [0, 4, 8],
  [2, 4, 6],
];

// Player 'X' plays first
let xTurn = true;
let count = 0;

// Disable All Buttons
const disableButtons = () => {
  btnRef.forEach((element) => (element.disabled = true));
  popupRef.classList.remove("hide");
};

// Enable all buttons (For New Game and Restart)
const enableButtons = () => {
  btnRef.forEach((element) => {
    element.innerText = "";
    element.disabled = false;
  });
  popupRef.classList.add("hide");
};

// This function is executed when a player wins
const winFunction = (letter) => {
  disableButtons();
  if (letter == "X") {
    msgRef.innerHTML = "&#x1F389; <br> 'X' Wins";
  } else {
    msgRef.innerHTML = "&#x1F389; <br> 'O' Wins";
  }
};

// Function for draw
const drawFunction = () => {
  disableButtons();
  msgRef.innerHTML = "&#x1F60E; <br> It's a Draw";
};

// New Game
newgameBtn.addEventListener("click", () => {
  count = 0;
  enableButtons();
});
restartBtn.addEventListener("click", () => {
  count = 0;
  enableButtons();
});

// Win Logic
const winChecker = () => {
  for (let i of winningPattern) {
    let [element1, element2, element3] = [
      btnRef[i[0]].innerText,
      btnRef[i[1]].innerText,
      btnRef[i[2]].innerText,
    ];
    if (element1 != "" && (element2 != "") & (element3 != "")) {
      if (element1 == element2 && element2 == element3) {
        winFunction(element1);
      }
    }
  }
};

// Display X/O on click
btnRef.forEach((element) => {
  element.addEventListener("click", () => {
    if (xTurn) {
      xTurn = false;
      element.innerText = "X";
      element.disabled = true;
    } else {
      xTurn = true;
      element.innerText = "O";
      element.disabled = true;
    }
    count += 1;
    if (count == 9) {
      drawFunction();
    }
    winChecker();
  });
});

// Enable Buttons and disable popup on page load
window.onload = enableButtons;

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: "Raleway", sans-serif;
}
body {
  height: 100vh;
  background: #00091f;
}
.wrapper {
  position: absolute;
  transform: translate(-50%, -50%);
  top: 50%;
  left: 50%;
}
.container {
  width: 70vmin;
  height: 70vmin;
  display: flex;
  flex-wrap: wrap;
  gap: 2vmin;
}
.button-option {
  background: #ffffff;
  height: 22vmin;
  width: 22vmin;
  border: none;
  border-radius: 8px;
  font-size: 12vmin;
  color: #00091f;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
}
#restart {
  font-size: 1.3em;
  padding: 1em;
  border-radius: 8px;
  background-color: #ffffff;
  color: #00091f;
  border: none;
  position: relative;
  margin: 1.5em auto 0 auto;
  display: block;
}
.popup {
  background: #00091f;
  height: 100%;
  width: 100%;
  position: absolute;
  display: flex;
  z-index: 2;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  gap: 1em;
  font-size: 12vmin;
}
#new-game {
  font-size: 0.6em
