<!DOCTYPE html>
<html lang="lv">
<head>
<meta charset="UTF-8">
<title>Mani darbi</title>
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
</head>

<body class="bg-light">

<div class="container mt-5">
<div class="card p-4 shadow">

<h3 class="text-center mb-4">Mani darbi</h3>

<div class="input-group mb-3">

<select id="prioritate" class="form-select">
<option value="low">zema</option>
<option value="medium">videja</option>
<option value="high">svarigi</option>
</select>

<input id="task-input" type="text" class="form-control" placeholder="Ieraksti darbu...">

<button id="add-btn" class="btn btn-primary">Pievienot</button>

</div>
<button

<ul id="task-list" class="list-group"></ul>

</div>
</div>

<script>

const input = document.getElementById("task-input");
const button = document.getElementById("add-btn");
const list = document.getElementById("task-list");
const priority = document.getElementById("prioritate");

let tasks = [];

function saveData(){
localStorage.setItem("tasks", JSON.stringify(tasks));
}

function loadData(){
let data = localStorage.getItem("tasks");

if(data){
tasks = JSON.parse(data);
tasks.forEach(task => createTask(task));
}
}
function createTask(task){

let li = document.createElement("li");
li.className = "list-group-item d-flex justify-content-between align-items-center";

let left = document.createElement("div");

let badge = document.createElement("span");
badge.classList.add("badge","me-2");

if(task.priority === "high"){
badge.classList.add("bg-danger");
badge.textContent = "svarigi";
}

else if(task.priority === "medium"){
badge.classList.add("bg-warning","text-dark");
badge.textContent = "videja";
}

else{
badge.classList.add("bg-secondary");
badge.textContent = "zema";
}

let span = document.createElement("span");
span.textContent = task.text;

if(task.done){
span.classList.add("text-decoration-line-through");
}

span.onclick = function(){
span.classList.toggle("text-decoration-line-through");
task.done = !task.done;
saveData();
};

left.appendChild(badge);
left.appendChild(span);

let deleteBtn = document.createElement("button");
deleteBtn.className = "btn btn-outline-danger btn-sm";
deleteBtn.textContent = "Dzēst";

deleteBtn.onclick = function(){
tasks = tasks.filter(t => t !== task);
li.remove();
saveData();
};

li.appendChild(left);
li.appendChild(deleteBtn);

list.appendChild(li);
}
button.onclick = function(){
let text = input.value.trim();
let pr = priority.value;
if(text === "") return;
let task = {
text: text,
priority: pr,
done: false
};

tasks.push(task);
createTask(task);
saveData();
input.value = "";
};
loadData();
</script>

</body>
</html>
