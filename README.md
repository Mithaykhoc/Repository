<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tài Xỉu Sunwin</title>
    <style>
        body { text-align: center; font-family: Arial, sans-serif; background-color: #f0f0f0; }
        .dice { font-size: 100px; display: none; }
        .result { font-size: 30px; font-weight: bold; color: black; display: none; }
        .countdown { font-size: 25px; color: red; }
        .button { font-size: 20px; padding: 10px 20px; background-color: blue; color: white; border: none; cursor: pointer; }
    </style>
</head>
<body>
    <h1>🎲 Tài Xỉu Sunwin 🎲</h1>
   
    <button class="button" onclick="startGame()">Quay Tài Xỉu!</button>
   
    <p class="countdown">Nhấn "Quay Tài Xỉu" để bắt đầu...</p>
    <p class="dice">🎲🎲🎲</p>
    <p class="result">Kết quả: ...</p>
    <script>
        let predefinedResults = [8, 13, 5, 16, 10, 12, 7, 14, 9, 11];  
        let currentIndex = 0;
        function generateValidDiceSum(hiddenTotal) {
            let firstDice, secondDice, thirdDice;
            do {
                firstDice = Math.floor(Math.random() * 6) + 1;
                secondDice = Math.floor(Math.random() * 6) + 1;
                thirdDice = hiddenTotal - firstDice - secondDice;
            } while (thirdDice < 1 || thirdDice > 6);
            return [firstDice, secondDice, thirdDice];
        }
        function startGame() {
            let countdownElement = document.querySelector(".countdown");
            let diceElement = document.querySelector(".dice");
            let resultElement = document.querySelector(".result");
            diceElement.style.display = "none";
            resultElement.style.display = "none";
            countdownElement.style.color = "red";
            let timeLeft = 10;
            let countdown = setInterval(() => {
                countdownElement.textContent = `Mở bát sau: ${timeLeft} giây`;
                timeLeft--;
                if (timeLeft < 0) {
                    clearInterval(countdown);
                    let hiddenTotal = predefinedResults[currentIndex];  
                    currentIndex = (currentIndex + 1) % predefinedResults.length;
                    let [firstDice, secondDice, thirdDice] = generateValidDiceSum(hiddenTotal);
                    let result = hiddenTotal > 10 ? "Tài" : "Xỉu";
                    countdownElement.textContent = "Kết quả đã có!";
                    countdownElement.style.color = "green";
                    diceElement.innerHTML = getDiceSymbol(firstDice) + " " + getDiceSymbol(secondDice) + " " + getDiceSymbol(thirdDice);
                    diceElement.style.display = "block";
                    resultElement.textContent = `Kết quả: ${result} (${hiddenTotal})`;
                    resultElement.style.color = result === "Tài" ? "red" : "green";
                    resultElement.style.display = "block";
                }
            }, 1000);
        }
        function getDiceSymbol(number) {
            const diceFaces = ["⚀", "⚁", "⚂", "⚃", "⚄", "⚅"];
            return diceFaces[number - 1];
        }
    </script>
</body>
</html>
