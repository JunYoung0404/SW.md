# 업 다운 게임

## 수정 사항
재시작 버튼 추가

정답에 대한 힌트를 정답값에 대한 up,down으로 표기

남은 기회를 알려줌

정답을 색상으로 표기

## 실행 화면
![image](https://github.com/user-attachments/assets/ac4b16ef-8ec1-497d-82a3-6a62a802165f)

![image](https://github.com/user-attachments/assets/73906844-3d21-4d7c-859d-53eda2921103)

### 소스코드
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

    <p>다음에서 시스템이 만든 숫자를 선택하세요.</p>
    <p id="status">결과: </p>
    <button id="resetBtn">재시작</button>
    <div id="btns"></div>
    
    <script>
        function getRandInt(min, max) {
            return min + Math.floor(Math.random() * (max - min + 1));
        }
        
        let min = 1;
        let max = 100;
        let num = getRandInt(min, max);
        let cnt = 3;
        console.log("num =>", num);

        let btns = document.querySelector("#btns");
        let status = document.querySelector("#status");
        let resetBtn = document.querySelector('#resetBtn');

        function resetGame() {
            min = 1;
            max = 100;
            num = getRandInt(min, max);
            cnt = 3;
            console.log("재시작 num =>", num);
            status.innerText = "결과: 재시작";
            draw();
        }

        resetBtn.onclick = function() {
            resetGame();
        };

        function draw() {
            btns.innerHTML = "";
            for (let i = min; i <= max; i++) {
                let newBtn = document.createElement("button");
                newBtn.innerText = i;
                btns.appendChild(newBtn);

                newBtn.onclick = function(e) {
                    cnt--;
                    let choiceNum = Number(e.target.innerText);
                    console.log(choiceNum);

                    if (num < choiceNum) {
                        status.innerText = `결과: ${choiceNum}보다 DOWN | `;
                    } else if (num > choiceNum) {
                        status.innerText = `결과: ${choiceNum}보다 UP | `;
                    }

                    if (num !== choiceNum && cnt > 0) {
                        status.innerText += "남은 기회: " + cnt;
                    }

                    if (num !== choiceNum && cnt <= 0) {
                        status.innerText = `정답은 ${num}이였습니다. 정답은 아래에서 확인하세요.`;
                        highlightCorrectAnswer();
                        return;
                    }

                    if (num === choiceNum) {
                        status.innerText = "결과: 정답입니다. 바로 새로운 게임이 시작되었습니다.";
                        resetGame();
                    }
                }
            }
        }

        function highlightCorrectAnswer() {
            let buttons = btns.querySelectorAll("button");
            buttons.forEach(button => {
                if (Number(button.innerText) === num) {
                    button.style.backgroundColor = "lightgreen";
                }
            });
        }

        draw();
    </script>
</body>
</html>
```
