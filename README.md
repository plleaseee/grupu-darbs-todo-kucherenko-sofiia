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
  <input id="task-input" type="text" class="form-control" placeholder="Jauns darbs">
  <button id="add-btn" class="btn btn-primary">Pievienot</button>
  </div>
  
  <ul id="task-list" class="list-group"></ul>
  </div>
  </div>
  
  <script>
    const input = document.getElementById("task-input");
    const button = document.getElementById("add-btn");
    const list = document.getElementById("task-list");

    button.onclick = function()
    {
      let text = input.value.trim();

        if (text === "")
        {
            return;
        }


        let li = document.createElement("li");
        li.className = "list-group-item d-flex justify-content-between align-items-center";
        li.innerHTML = text;

        let deleteBtn = document.createElement("button");
        deleteBtn.className = "btn btn-danger";
        deleteBtn.innerHTML = "Dzēst";

        deleteBtn.onclick = function()
        {
            li.remove();
        };

        li.appendChild(deleteBtn);
        list.appendChild(li);

        input.value = "";
    };
</script>

</body>
</html>
