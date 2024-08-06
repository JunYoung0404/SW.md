# todolist

###실행결과
![image](https://github.com/user-attachments/assets/e5a17589-2b01-4f25-8a58-ed1fe2b3a06e)



## HTML
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        /* 완료된 할 일의 제목에 취소선을 그리는 스타일을 정의합니다 */
        span.okTitle {
            text-decoration: line-through;
        }
    </style>
</head>
<body>
    <h1>Todo List</h1>
    <p>
        할일: <input type="text" class="title">
        <button id="saveBtn">SAVE</button>
    </p>
    <ul class="resultArea">
    </ul>
</body>
</html>
```

## JavaScript
```
<script>
    var saveBtn = document.querySelector("#saveBtn"); // 저장 버튼을 선택
    var title = document.querySelector(".title"); // 할 일 제목 입력 필드를 선택

    //할일을 배열로 만듬
    var todoList = [
        {no:101, title:"hello", done:false},
        {no:102, title:"hello2", done:true},
        {no:103, title:"hello3", done:true},
        {no:104, title:"hello4", done:false}
    ];
    var todoSeq = 105;
    // 주어진 할 일을 todoList에서 찾는 함수
    function myFindIdx(todoList, todo) {
        var idx = todoList.findIndex(function(t) {
            return t.no === todo.no;
        });
        return idx;
    }

    // 할 일 목록을 화면에 나타냄
    function drawList() {
        var listArea = document.querySelector(".resultArea");
        listArea.innerHTML = ""; // 기존 목록을 비움
        todoList.forEach(function(todo) {
            var liTag = document.createElement("li");
            var checkBox = document.createElement("input");
            var delBtn = document.createElement("button");
            var spanTag = document.createElement("span");

            liTag.style.listStyle = "none"; // 목록 아이템의 스타일을 제거
            checkBox.setAttribute("type", "checkbox");
            spanTag.setAttribute("class", "");
            checkBox.removeAttribute("checked");
            if(todo.done) {
                checkBox.setAttribute("checked", "checked");
                spanTag.setAttribute("class", "okTitle");
            }
            spanTag.innerHTML = todo.title + " ";
            delBtn.innerText = "Delete";

            // 삭제 버튼 클릭 이벤트 
            delBtn.addEventListener('click', function(event) {
                var idx = myFindIdx(todoList, todo);
                if(idx != -1) {
                    todoList.splice(idx, 1); // 배열에서 할 일을 삭제
                    drawList(); 
                }
            });

            // 체크박스 변경 이벤트
            checkBox.addEventListener('change', function(event){
                var idx = myFindIdx(todoList, todo);
                if(idx != -1) {
                    todoList[idx].done = !todoList[idx].done; // 할 일 완료 상태를 변경
                    drawList(); 
                }
            });

            liTag.appendChild(checkBox); // li 요소에 체크박스를 추가
            liTag.appendChild(spanTag); // li 요소에 제목을 추가
            liTag.appendChild(delBtn); // li 요소에 삭제 버튼을 추가
            listArea.appendChild(liTag); // ul 요소에 li를 추가
        });
    }
    drawList(); 

    // 배열에 새 할 일을 추가하는 함수
    function append() {
        todoList.push({
            no:todoSeq++, title:title.value, done:false
        });
        drawList(); 
        title.value = ""; // 입력 필드를 비움
        title.focus(); .
    }

    saveBtn.onclick = function() {
        append(); // 저장 버튼 클릭 시 할 일을 추가
    }

    title.onkeydown = function(e) {
        if(e.keyCode === 13) { // 엔터 키를 눌렀을 때 할 일을 추가
            append();
        }
    }
</script>
```
