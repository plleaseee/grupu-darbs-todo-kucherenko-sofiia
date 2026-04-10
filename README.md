<!DOCTYPE html>
<html lang="lv">
<head>
<meta charset="UTF-8">
<title>Mani darbi</title>
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body class="bg-light">
<div class="container mt-5">
  <div class="row justify-content-center">
  <div class="col-md-8">
  <div class="card shadow p-4">
  <h1 class="text-center mb-4">Mani darbi</h1>
  <div class="input-group mb-3"> 
    <select id="prioritate" class="form-select" style="max-width: 120px;">
      <option value="low">Zema</option>
      <option value="medium">Vidēja</option>
      <option value="high">Svarīgi</option>
   </select>
    <input type="text" class="form-control" placeholder="Ieraksti darbu..." id="teksts">
    <button class="btn btn-primary" onclick="addTask()">Pievienot</button>
  </div>
  <input type="text" class="form-control mb-3" placeholder="Meklēt uzdevumu..." id="teksts">
  <ul id="task-list" class="list-group"></ul>
  </div>
  </div>
  </div>
</div>

<script>
const tekstsInput = document.getElementById("teksts");
const priority = document.getElementById("prioritate");
const list = document.getElementById("task-list");

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
    badge.textContent = "svarīgi";
  }
  else if(task.priority === "medium"){
    badge.classList.add("bg-warning");
    badge.textContent = "vidēja";
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
  span.style.cursor = "pointer";
  span.onclick = function(){
    span.classList.toggle("text-decoration-line-through");
    task.done = !task.done;
    saveData();
  };

  left.appendChild(badge);
  left.appendChild(span);
  
  let editBtn = document.createElement("button");
  editBtn.className = "btn btn-outline-info btn-sm ms-auto me-2";
  editBtn.textContent = "Labot";

  editBtn.onclick = function(){
  let currentText = task.text;
  let newText = prompt("Mainit uzdevuma nosaukumu:", currentText)
  
  if (newText !== null && newText.trim() !== "") {
  task.text = newText.trim();
  span.textContent = task.text;
  saveData();
  }
  };
  
  let deleteBtn = document.createElement("button");
  deleteBtn.className = "btn btn-outline-danger btn-sm";
  deleteBtn.textContent = "Dzēst";

  deleteBtn.onclick = function(){
    tasks = tasks.filter(t => t !== task);
    li.remove();
    saveData();
  };

  li.appendChild(left);
  li.appendChild(editBtn);
  li.appendChild(deleteBtn);

  list.appendChild(li);
}

function addTask(){
  let text = tekstsInput.value.trim();
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
  tekstsInput.value = "";
}

loadData();
</script>
</body>
</html>
