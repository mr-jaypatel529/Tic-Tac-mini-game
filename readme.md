# First create index.HTML file
# Second step create Style.CSS file
# Third step Create script.JS file
# If you like to add who's winning and losing message, you can edit from script.JS file
# If you like to change colour anything in this game, you can edit it by Using style.CSS file

# index.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic Tac mini game | JayPatel</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Raleway:wght@700&display=swap" rel="stylesheet">

    <link rel="stylesheet" href="style.css">
</head>
<body>
   <div class="JayPatel">
       <div class="JayPatel1">
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


# style.css 

/* Import Raleway font */
@import url('https://fonts.googleapis.com/css2?family=Raleway:wght@700&display=swap');

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: "Raleway", sans-serif;
}

body {
  height: 100vh;
  background: linear-gradient(105deg, #00f2ff, rgb(0, 16, 197));
}

html {
  font-size: 16px;
}

.JayPatel {
  position: absolute;
  transform: translate(-50%, -50%);
  top: 50%;
  left: 50%;
}

.JayPatel1 {
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
  color: rgb(11, 13, 118);
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
}

#restart {
  font-size: 1.3em;
  padding: 1em;
  border-radius: 8px;
  background-color: #0a0027;
  color: #ffffff;
  border: none;
  position: relative;
  margin: 1.5em auto 0 auto;
  display: block;
}

.popup {
  background: linear-gradient(105deg, #00f2ff, rgb(0, 16, 197));
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
  font-size: 0.6em;
  padding: 0.5em 1em;
  background-color: #0a0027;
  color: #ffffff;
  border-radius: 0.2em;
  border: none;
}

#message {
  color: #ffffff;
  text-align: center;
  font-size: 1em;
}

.popup.hide {
  display: none;
}

# script.js

let btnRef = document.querySelectorAll(".button-option");
let popupRef = document.querySelector(".popup");
let newgameBtn = document.getElementById("new-game");
let restartBtn = document.getElementById("restart");
let msgRef = document.getElementById("message");

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

let xTurn = true;
let count = 0;

const disableButtons = () => {
  btnRef.forEach((element) => (element.disabled = true));

  popupRef.classList.remove("hide");
};

const enableButtons = () => {
  btnRef.forEach((element) => {
    element.innerText = "";
    element.disabled = false;
  });

  popupRef.classList.add("hide");
};

const winFunction = (letter) => {
  disableButtons();
  if (letter == "X") {
    msgRef.innerHTML = "<br> 1st player X Wins";
  } else {
    msgRef.innerHTML = "<br> 2nd player O Wins";
  }
};

const drawFunction = () => {
  disableButtons();
  msgRef.innerHTML = "<br> It's a Draw";
};

newgameBtn.addEventListener("click", () => {
  count = 0;
  enableButtons();
});
restartBtn.addEventListener("click", () => {
  count = 0;
  enableButtons();
});

const winChecker = () => {
  for (let i of winningPattern) {
    let [element1, element2, element3] = [
      btnRef[i[0]].innerText,
      btnRef[i[1]].innerText,
      btnRef[i[2]].innerText,
    ];
    // Check if elements are filled
    // If 3 empty elements are the same and would give win as would
    if (element1 !== "" && element2 !== "" && element3 !== "") {
      if (element1 === element2 && element2 === element3) {
        // If all 3 buttons have the same values then pass the value to winFunction
        winFunction(element1);
      }
    }
  }
};

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
    if (count === 9) {
      drawFunction();
    }

    winChecker();
  });
});

window.onload = enableButtons;

