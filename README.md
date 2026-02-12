# grupu-darbs-todo-kucherenko-sofiia
Testa repozitorijs 1. kursa programmētajiem
<!DOCTYPE html>
<html lang="lv">
  <head>
    <meta charset="UTF-8">
    <title>Mani darbi</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
  </head>
  <body>
    <div class="container">
  <h3 class="text-center mb-3">Mani darbi</h3>
  <div class="card"></div>
<div class="input-group mb-3">
   <div class="card-body">
     <input type="text" class="form-control" placeholder=" Ieraksti darbu" id="teksts" name="etxt">
   </div>
      <button class="btn btn-dark" onclick="addTask()">Pievienot</button>
      </div>
      <ul id="task-list" class="list-group"></ul>
      </div>
  </body>
  <script>
  function addTask() {
    const input = document.getElementById("teksts");
    const tasklist = document.getElementById("task-list");
    const task = input.value.trim();
    if (task === "") return; 
    
  const li = document.createElement("li");
  li.innerHTML = task + " ";
  li.className = "list-group-item";
  tasklist.appendChild(li);
  input.value = "";
  const dltbtn = document.createElement("button");
  dltbtn.textContent = "Dzēst";
  dltbtn.className = "btn btn-dark float-end";
  dltbtn.onclick = function () {
    li.remove();
    saveTasks();
  };
   li.appendChild(dltbtn);
  }
</script>
  </html>
