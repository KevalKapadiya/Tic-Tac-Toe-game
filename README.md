#JavaScript Code

let boxes = document.querySelectorAll(".box");
let resetBtn = document.querySelector("#reset-btn");
let newGameBtn = document.querySelector("#new-btn");
let msgContainer = document.querySelector(".msg-container");
let msg = document.querySelector("#msg");

let turnO = true; //playerX, playerO
let count = 0; //To Track Draw

const winPatterns = [
  [0, 1, 2],
  [0, 3, 6],
  [0, 4, 8],
  [1, 4, 7],
  [2, 5, 8],
  [2, 4, 6],
  [3, 4, 5],
  [6, 7, 8],
];

const resetGame = () => {
  turnO = true;
  count = 0;
  enableBoxes();
  msgContainer.classList.add("hide");
};

boxes.forEach((box) => {
  box.addEventListener("click", () => {
    if (turnO) {
      //playerO
      box.innerText = "O";
      turnO = false;
    } else {
      //playerX
      box.innerText = "X";
      turnO = true;
    }
    box.disabled = true;
    count++;

    let isWinner = checkWinner();

    if (count === 9 && !isWinner) {
      gameDraw();
    }
  });
});

const gameDraw = () => {
  msg.innerText = `Game was a Draw.`;
  msgContainer.classList.remove("hide");
  disableBoxes();
};

const disableBoxes = () => {
  for (let box of boxes) {
    box.disabled = true;
  }
};

const enableBoxes = () => {
  for (let box of boxes) {
    box.disabled = false;
    box.innerText = "";
  }
};

const showWinner = (winner) => {
  msg.innerText = `Congratulations, Winner is ${winner}`;
  msgContainer.classList.remove("hide");
  disableBoxes();
};

const checkWinner = () => {
  for (let pattern of winPatterns) {
    let pos1Val = boxes[pattern[0]].innerText;
    let pos2Val = boxes[pattern[1]].innerText;
    let pos3Val = boxes[pattern[2]].innerText;

    if (pos1Val != "" && pos2Val != "" && pos3Val != "") {
      if (pos1Val === pos2Val && pos2Val === pos3Val) {
        showWinner(pos1Val);
        return true;
      }
    }
  }
};

newGameBtn.addEventListener("click", resetGame);
resetBtn.addEventListener("click", resetGame);






#CSS Code

* {
    margin: 0;
    padding: 0;
  }
  
  body {
    background-color: #548687;
    text-align: center;
  }
  
  .container {
    height: 70vh;
    display: flex;
  
    justify-content: center;
    align-items: center;
  }
  
  .game {
    height: 60vmin;
    width: 60vmin;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    gap: 1.5vmin;
  }
  
  .box {
    height: 18vmin;
    width: 18vmin;
    border-radius: 1rem;
    border: none;
    box-shadow: 0 0 1rem rgba(0, 0, 0, 0.3);
    font-size: 8vmin;
    color: #b0413e;
    background-color: #ffffc7;
  }
  
  #reset-btn {
    padding: 1rem;
    font-size: 1.25rem;
    background-color: #191913;
    color: #fff;
    border-radius: 1rem;
    border: none;
  }
  
  #new-btn {
    padding: 1rem;
    font-size: 1.25rem;
    background-color: #191913;
    color: #fff;
    border-radius: 1rem;
    border: none;
  }
  
  #msg {
    color: #ffffc7;
    font-size: 5vmin;
  }
  
  .msg-container {
    height: 100vmin;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    gap: 4rem;
  }
  
  .hide {
    display: none;
  }


