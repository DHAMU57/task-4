index.html:

<html>
<head>
  <title>To-Do WebApp</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <h1>To-Do List</h1>
    <div class="input-group">
      <input type="text" id="taskInput" placeholder="Add a new task..." />
      <button onclick="addTask()">Add</button>
    </div>
    <div class="tasks-section">
      <h2>Pending Tasks</h2>
      <ul id="pendingList"></ul>
      <h2>Completed Tasks</h2>
      <ul id="completedList"></ul>
    </div>
  </div>
  <script src="script.js"></script>
</body>
</html>

style.css:
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: 'Poppins', sans-serif;
  background: linear-gradient(135deg, #667eea, #764ba2);
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}
.container {
  background: #ffffff10;
  backdrop-filter: blur(15px);
  border-radius: 20px;
  padding: 30px;
  width: 90%;
  max-width: 500px;
  color: #fff;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
}
h1 {
  text-align: center;
  margin-bottom: 20px;
}
.input-group {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}
.input-group input {
  flex: 1;
  padding: 12px;
  font-size: 16px;
  border: none;
  border-radius: 10px;
  outline: none;
}
.input-group button {
  padding: 12px 18px;
  background-color: #28a745;
  color: #fff;
  font-weight: bold;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  transition: background 0.2s;
}

.input-group button:hover {
  background-color: #218838;
}

.tasks-section h2 {
  margin-top: 20px;
  margin-bottom: 10px;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  background-color: #ffffff20;
  padding: 12px;
  border-radius: 8px;
  margin-bottom: 10px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

li.completed {
  text-decoration: line-through;
  color: #c8e6c9;
}

.task-buttons button {
  margin-left: 8px;
  padding: 5px 10px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-size: 0.9rem;
}

.complete-btn {
  background-color: #007bff;
  color: white;
}

.delete-btn {
  background-color: #dc3545;
  color: white;
}

script.js:

function addTask() {
  const taskInput = document.getElementById("taskInput");
  const taskText = taskInput.value.trim();
  if (taskText === "") return;

  const li = createTaskElement(taskText);
  document.getElementById("pendingList").appendChild(li);
  taskInput.value = "";
}

function createTaskElement(taskText) {
  const li = document.createElement("li");
  li.textContent = taskText;

  const btnGroup = document.createElement("div");
  btnGroup.classList.add("task-buttons");

  const completeBtn = document.createElement("button");
  completeBtn.textContent = "✔";
  completeBtn.classList.add("complete-btn");
  completeBtn.onclick = () => {
    document.getElementById("completedList").appendChild(li);
    completeBtn.remove(); // remove complete button
    li.classList.add("completed");
  };

  const deleteBtn = document.createElement("button");
  deleteBtn.textContent = "🗑";
  deleteBtn.classList.add("delete-btn");
  deleteBtn.onclick = () => li.remove();

  btnGroup.appendChild(completeBtn);
  btnGroup.appendChild(deleteBtn);
  li.appendChild(btnGroup);

  return li;
}
