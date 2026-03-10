# Ex03 To-Do List using JavaScript

## Date: 10/03/2026

## AIM
To create a To-do Application with all features using JavaScript.

## ALGORITHM
### STEP 1
Build the HTML structure (index.html).

### STEP 2
Style the App (style.css).

### STEP 3
Plan the features the To-Do App should have.

### STEP 4
Create a To-do application using Javascript.

### STEP 5
Add functionalities.

### STEP 6
Test the App.

### STEP 7
Open the HTML file in a browser to check layout and functionality.

### STEP 8
Fix styling issues and refine content placement.

### STEP 9
Deploy the website.

### STEP 10
Upload to GitHub Pages for free hosting.

## PROGRAM

# HTML

```html
<!DOCTYPE html>
<html lang="en">

<head>
<meta charset="UTF-8">
<title>Advanced Todo</title>
<link rel="stylesheet" href="style.css">
</head>

<body>

<div class="app">

<header>
<h1>Smart Todo 🚀</h1>
<button id="themeToggle">🌙</button>
</header>

<div class="taskInput">

<input type="text" id="taskInput" placeholder="Enter task">

<input type="date" id="dueDate">

<select id="category">
<option value="Work">Work</option>
<option value="Study">Study</option>
<option value="Personal">Personal</option>
</select>

<button onclick="addTask()">Add</button>

</div>

<input type="text" id="search" placeholder="Search tasks...">

<div class="progressContainer">
<div id="progressBar"></div>
</div>

<ul id="taskList"></ul>

</div>

<script src="script.js"></script>

</body>
</html>
```
# CSS

```css
body{
font-family:Arial;
background:#f5f5f5;
display:flex;
justify-content:center;
padding-top:40px;
transition:0.3s;
}

.dark{
background:#1e1e1e;
color:white;
}

.app{
width:500px;
background:white;
padding:25px;
border-radius:10px;
box-shadow:0 10px 30px rgba(0,0,0,0.2);
}

.dark .app{
background:#2b2b2b;
}

header{
display:flex;
justify-content:space-between;
align-items:center;
}

.taskInput{
display:flex;
gap:5px;
margin:15px 0;
}

input,select{
padding:8px;
border-radius:5px;
border:1px solid #ccc;
}

button{
padding:8px 12px;
border:none;
background:#0077ff;
color:white;
border-radius:5px;
cursor:pointer;
}

button:hover{
background:#005fd1;
}

ul{
list-style:none;
padding:0;
}

li{
display:flex;
justify-content:space-between;
align-items:center;
background:#eee;
margin-top:8px;
padding:10px;
border-radius:6px;
cursor:grab;
}

.completed{
text-decoration:line-through;
opacity:0.6;
}

.progressContainer{
width:100%;
height:10px;
background:#ddd;
border-radius:10px;
margin-bottom:10px;
}

#progressBar{
height:10px;
width:0%;
background:#4caf50;
border-radius:10px;
}
```

# JS

```js
let tasks = JSON.parse(localStorage.getItem("tasks")) || [];

function save(){
localStorage.setItem("tasks",JSON.stringify(tasks));
}

function addTask(){

let text=document.getElementById("taskInput").value;
let date=document.getElementById("dueDate").value;
let category=document.getElementById("category").value;

if(text==="") return;

tasks.push({
text,
date,
category,
completed:false
});

render();
}

function render(){

let list=document.getElementById("taskList");
list.innerHTML="";

tasks.forEach((task,index)=>{

let li=document.createElement("li");

li.draggable=true;

li.innerHTML=`
<span class="${task.completed?'completed':''}" onclick="toggle(${index})">
${task.text} (${task.category}) - ${task.date}
</span>

<div>
<button onclick="edit(${index})">✏</button>
<button onclick="removeTask(${index})">🗑</button>
</div>
`;

list.appendChild(li);

li.addEventListener("dragstart",dragStart);
li.addEventListener("dragover",dragOver);
li.addEventListener("drop",drop);

});

updateProgress();
save();
}

function toggle(i){
tasks[i].completed=!tasks[i].completed;
render();
}

function removeTask(i){
tasks.splice(i,1);
render();
}

function edit(i){

let newText=prompt("Edit Task",tasks[i].text);

if(newText){
tasks[i].text=newText;
render();
}
}

function updateProgress(){

let completed=tasks.filter(t=>t.completed).length;

let percent=(completed/tasks.length)*100 || 0;

document.getElementById("progressBar").style.width=percent+"%";
}

function dragStart(e){
dragIndex=[...e.target.parentNode.children].indexOf(e.target);
}

function dragOver(e){
e.preventDefault();
}

function drop(e){

let dropIndex=[...e.target.parentNode.children].indexOf(e.target);

let temp=tasks[dragIndex];
tasks.splice(dragIndex,1);
tasks.splice(dropIndex,0,temp);

render();
}

document.getElementById("themeToggle").onclick=function(){

document.body.classList.toggle("dark");

};

document.getElementById("search").addEventListener("keyup",function(){

let value=this.value.toLowerCase();

document.querySelectorAll("#taskList li").forEach(li=>{

if(li.innerText.toLowerCase().includes(value))
li.style.display="flex";
else
li.style.display="none";

});

});

render();
```
## OUTPUT

<img width="1919" height="1043" alt="image" src="https://github.com/user-attachments/assets/9788144e-2d28-4e65-933a-081b7aee8f87" />

## RESULT
The program for creating To-do list using JavaScript is executed successfully.
