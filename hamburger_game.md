# 햄버거게임

![image](https://github.com/user-attachments/assets/81fb4b6a-488b-48c4-a873-2a63406424d9)
## 변경사항
숫자 부분을 koreanNumbers 배열을 만들어서 한글을 넣어 보았습니다.

## 소스코드

```
 function Box() { }
    // Box의 프로토타입을 HTMLDivElement의 프로토타입으로 설정
    Box.prototype = Object.create(HTMLDivElement.prototype);
    Box.prototype.constructor = Box;
    // Box 초기화 메서드
    Box.prototype.init = function(text) {
        this.newBox = document.createElement("Box");
        this.elementUl = document.createElement("ul");
        
        // 한글 숫자 배열
        const koreanNumbers = ["일", "이", "삼", "사", "오", "육", "칠", "팔", "구", "십"];
        
        for(var i=0; i<10; i++) {
            this.elementLi = document.createElement("li");
            this.elementLi.innerText = koreanNumbers[i]; // 한글 숫자 설정
            this.elementUl.appendChild(this.elementLi);
        }
        this.newBox.appendChild(this.elementUl);
        this.newBox.setAttribute("class", "newBox");
        return this.newBox;
    }
    // Box 시작 메서드
    Box.prototype.start = function(speed) {
        this.elementUl.style.position = "absolute";
        this.elementUl.style.left = "0px";
        this.elementUl.style.top = "0px";
        this.y = 0;
        this.intervalRef = setInterval(() => {
            this.y -= 10;
            this.elementUl.style.top = this.y + "px";
            if(this.y <= -900) {
                this.y = 0;
            }
        }, speed);
    }

```
