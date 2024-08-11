# 박스 잡기 게임
움직이는 박스를 클릭하면 점수가 올라가고 5번 놓치면 게임오버

# 실행 사진
![image](https://github.com/user-attachments/assets/23524aef-13d7-4758-b648-9aad20e219e0)
![image](https://github.com/user-attachments/assets/ad9741b2-d8dd-44d0-aa24-e02770b54ccf)

# 코드
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Catch the Moving Box</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <style>
        body {
            margin: 0;
            overflow: hidden; /* 박스가 화면 밖으로 벗어나지 않도록 스크롤바 제거 */
            font-family: Arial, sans-serif;
        }
        .box {
            position: absolute;
            left: 50px;
            top: 50px;
            width: 100px;
            height: 100px;
            box-sizing: border-box;
            border: 3px solid black;
            background-color: skyblue;
            cursor: pointer;
        }
        #scoreboard {
            position: absolute;
            top: 10px;
            left: 10px;
            font-size: 24px;
        }
        #misses {
            position: absolute;
            top: 50px;
            left: 10px;
            font-size: 24px;
            color: red;
        }
        #gameover {
            display: none;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 48px;
            color: black;
        }
        #restartBtn {
            display: none;
            position: absolute;
            top: 60%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 24px;
            padding: 10px 20px;
            background-color: lightgreen;
            border: none;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div id="scoreboard">Score: 0</div>
    <div id="misses">Misses: 0</div>
    <div id="gameover">Game Over</div>
    <button id="restartBtn">Restart</button>
    <div class="box"></div>
    <script>
        let score = 0;
        let misses = 0;
        let speedX = 5;
        let speedY = 5; 
        let interval;
        const maxMisses = 5;

        // 박스 자동 이동 함수
        function moveBox() {
            const box = $('.box');
            const windowWidth = $(window).width();
            const windowHeight = $(window).height();
            const boxWidth = box.width();
            const boxHeight = box.height();

            let newLeft = parseInt(box.css('left')) + speedX;
            let newTop = parseInt(box.css('top')) + speedY;

            // 화면 경계에 닿으면 반대 방향으로 움직임
            if (newLeft <= 0 || newLeft + boxWidth >= windowWidth) {
                speedX = -speedX;
            }
            if (newTop <= 0 || newTop + boxHeight >= windowHeight) {
                speedY = -speedY;
            }

            box.css({
                left: newLeft + 'px',
                top: newTop + 'px'
            });
        }

        // 자동 이동 시작
        interval = setInterval(moveBox, 50);

        // 박스를 클릭할 때 점수 증가 및 속도 증가
        $('.box').mousedown(function() {
            score++;
            $('#scoreboard').text('Score: ' + score);
            speedX *= 1.2; // X축 속도를 20% 증가시킴
            speedY *= 1.2; // Y축 속도를 20% 증가시킴
        });

        // 박스를 놓치면 미스 증가
        $(window).mousedown(function(e) {
            if (!$(e.target).hasClass('box')) {
                misses++;
                $('#misses').text('Misses: ' + misses);

                if (misses >= maxMisses) {
                    clearInterval(interval);
                    $('#gameover').show();
                    $('.box').hide(); // 박스를 숨김
                    $('#restartBtn').show(); // 재시작 버튼을 표시
                }
            }
        });

        // 재시작 버튼 클릭 시 게임을 초기화
        $('#restartBtn').click(function() {
            // 초기 상태로 되돌림
            score = 0;
            misses = 0;
            speedX = 5;
            speedY = 5;

            $('#scoreboard').text('Score: ' + score);
            $('#misses').text('Misses: ' + misses);
            $('#gameover').hide();
            $('#restartBtn').hide();
            $('.box').show();
            $('.box').css({ left: '50px', top: '50px' });

            // 박스 이동 재시작
            interval = setInterval(moveBox, 50);
        });
    </script>
    
</body>
</html>

```
