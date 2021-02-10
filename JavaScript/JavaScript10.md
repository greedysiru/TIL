# [노마드코더]바닐라 JS로 크롬 앱 만들기 (4)(2021.1.19)



**상세 내용 [블로그](https://greedysiru.tistory.com/123) 참고**



# Making My First JS APP

## 1. Making a To Do List part One

### HTML

* index.html에 To Do List를 만들기 위한 **form을 만들고  class를 지정**

```HTML
    <form class="js-toDoForm">                       <!-- 입력을 받기 위한 form -->
      <input type="text" placeholder="Write a to do" />
    </form>
    <ul class="js-toDoList"> <!-- JavaScript로 생성된 elements를 넣을 class -->
    </ul>
    <script src="todo.js"></script>
```



### JavaScript

```JavaScript
const toDoform = document.querySelector(".js-toDoForm"),
    toDoInput = toDoform.querySelector("input"),
    toDoList = document.querySelector(".js-toDoList");

const TODOS_LS = 'toDos';

function paintToDo(text){
    const li = document.createElement("li"); //비어있는 li element 생성
    const delBtn = document.createElement("button"); //button 생성
    delBtn.innerText = "❌";
    const span = document.createElement("span"); //span 생성
    span.innerText = text;
    li.appendChild(delBtn);
    li.appendChild(span);  //부모 element에 넣기 생성된 li에 span과 button을 넣는다.
    toDoList.appendChild(li); // 이들을 toDoList에 넣는다.
}
function handleSubmit(event){
    event.preventDefault();
    const currentValue = toDoInput.value; // input에 입력한 value를 currentValue로 선언
    paintToDo(currentValue);
    toDoInput.value=""; // input을 비운다.
}
function loadTodos(){
    const toDos = localStorage.getItem(TODOS_LS);
    if(toDos !== null){
    } else{
    }
}
function init(){
    toDoform.addEventListener("submit" , handleSubmit); // submit할 시 함수 호출
}
init();
```





## 2. Making a To Do List part Two

* To Do List에 저장 기능을 추가
* 해야할 것
  1. **To Do List를 array로 저장**
  2. **JSON을 사용해서, 데이터를 전달**.
  3. **Local Storage에 데이터를 저장**



### JSON

* **JavaScript Object Notation**
* 데이터를 전달할 때, 자바스크립트가 그것을 다룰 수 있도록 Object로 바꾸거나 Object를 String으로 바꾸는 역할
* **Local Storage는 string만 저장** 할 수 있으므로 JSON이 필수
* **JSON.stringify()** : Object를 Stirng으로 변환
* **JSON.parse()** : String을 Object로 변환



### JavaScript

```JavaScript
const toDoform = document.querySelector(".js-toDoForm"),
    toDoInput = toDoform.querySelector("input"),
    toDoList = document.querySelector(".js-toDoList");

const TODOS_LS = 'toDos';

const toDos =[]; // 해야할 일을 생성할 때 마다 toDos에 array로 입력

function saveToDos(){ //toDos local 저장
    localStorage.setItem(TODOS_LS, JSON.stringify(toDos)); //string으로 바꿔주기
}
function paintToDo(text){
    const li = document.createElement("li"); 
    const delBtn = document.createElement("button"); 
    const span = document.createElement("span");
    const newId = toDos.length + 1; // 생성된 to do에 ID를 번호로 부여
    delBtn.innerText = "❌";   
    span.innerText = text;
    li.appendChild(delBtn);
    li.appendChild(span); 
    li.id = newId;
    toDoList.appendChild(li);
    const toDoObj = {
        text: text,           
        id: newId // 입력한 텍스트와 배열의 길이 + 1(1부터 카운트)을 toDoObj에 넣는다.
    };
    toDos.push(toDoObj); // toDoObj를 선언한 배열 toDos에 넣어준다.
    saveToDos()
}
function handleSubmit(event){
    event.preventDefault();
    const currentValue = toDoInput.value;
    paintToDo(currentValue);
    toDoInput.value="";
}
function loadTodos(){
    const loadedToDos = localStorage.getItem(TODOS_LS);  // local Storage 저장
    if(loadedToDos !== null){
        const parsedToDos = JSON.parse(loadedToDos); // object 변환
        parsedToDos.forEach(function(toDo){
            paintToDo(toDo.text); // toDo의 text 하나씩 paintToDo 실행
        }) // array 각각에 한 번씩 함수를 실행, 안에서 선언할 수 있다.
    } else{

    }
}
function init(){
    loadTodos();
    toDoform.addEventListener("submit" , handleSubmit);
}
init();
```

* toDos에 toDoObj로 인해서 Object가 array의 형태로 입
* Local Storage에 저장할 때는 **JSON.stringify()**로 string으로 변환
* string형태의 array 각각에 함수를 실행할 때는 **JSON.parse() d**로 Object로 다시 변환
* **.forEach()**: array의 원소 하나하나를 함수 실행
* **const newId = toDos.length + 1;** : id값을 1부터 카운트 하기 위해서 toDos의 길이의 +1을 더함



## 3. Making a To Do List part Three

* 버튼에 삭제하는 기능 추가

```JavaScript
const toDoform = document.querySelector(".js-toDoForm"),
    toDoInput = toDoform.querySelector("input"),
    toDoList = document.querySelector(".js-toDoList");

const TODOS_LS = 'toDos';

let toDos =[]; 

//li에 없는 id인 toDos를 체크 - 지울것

function deleteToDo(event){
   const btn = event.target;
   const li = btn.parentNode;      //parent node
   toDoList.removeChild(li);     // 삭제버튼 누른 해당 li 지우기
   const cleanToDos = toDos.filter(function(toDo){       // 삭제후 목록을 cleanToDos 변수에 넣기
       return toDo.id !== parseInt(li.id); // 숫자 변환하여 비교하기
   });
   toDos = cleanToDos            //이전 것과 바꾸기
   saveToDos();
}

function saveToDos(){ 
    localStorage.setItem(TODOS_LS, JSON.stringify(toDos)); 
}

function paintToDo(text){
    const li = document.createElement("li"); 
    const delBtn = document.createElement("button"); 
    const span = document.createElement("span"); 
    const newId = toDos.length + 1; 
    delBtn.innerText = "❌";
    delBtn.addEventListener("click", deleteToDo);   
    span.innerText = text;
    li.appendChild(delBtn);
    li.appendChild(span); 
    li.id = newId;
    toDoList.appendChild(li);
    const toDoObj = {
        text: text,           
        id: newId
    };
    toDos.push(toDoObj); 
    saveToDos()
}

function handleSubmit(event){
    event.preventDefault();
    const currentValue = toDoInput.value;
    paintToDo(currentValue);
    toDoInput.value="";
}
function loadTodos(){
    const loadedToDos = localStorage.getItem(TODOS_LS); 
    if(loadedToDos !== null){
        const parsedToDos = JSON.parse(loadedToDos); 
        parsedToDos.forEach(function(toDo){
            paintToDo(toDo.text); 
        }) 
    } else{
    }
}

function init(){
    loadTodos();
    toDoform.addEventListener("submit" , handleSubmit);
}

init();
```

* **btn.parentNode** : btn의 parents node를 찾는다.
* **.filter** : array의 모든 item을 통해 함수를 실행하고 true인 item들만 가지고 새로운 array를 만든다. 

