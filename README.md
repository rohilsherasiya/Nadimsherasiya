Er Rohil sheasiya
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>To-Do List</title>
    <style>
        body {
            font-family: sans-serif;
            background: #f7e6d0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        .todo {
            background: #fff;
            padding: 20px;
            border-radius: 10px;
            width: 97%;
            max-width: 400px;
            box-shadow: 0 0 10px #aaa;
        }

        .todo h2 {
            margin: 0 0 10px;
            text-align: center;
        }

        .input-row {
            display: flex;
            gap: 10px;
        }

        input[type=text] {
            flex: 1;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        button {
            padding: 10px;
            background: #f78f1e;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        ul {
            padding: 0;
            list-style: none;
            margin-top: 15px;
        }

        li {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: #f1f1f1;
            margin-bottom: 8px;
            padding: 8px 10px;
            border-radius: 6px;
        }

        .edit,
        .del {
            margin-left: 5px;
            background: #ccc;
            padding: 5px 8px;
            font-size: 12px;
        }

        .edit {
            background: #4caf50;
            color: white;
        }

        .del {
            background: #e74c3c;
            color: white;
        }
    </style>
</head>

<body>
    <div class="todo">
        <h2>📝 To-Do</h2>
        <div class="input-row">
            <input id="taskInput" type="text" placeholder="New task">
            <button onclick="addTask()">Add</button>
        </div>
        <ul id="list"></ul>
    </div>

    <script>
        const input = document.getElementById('taskInput');
        const list = document.getElementById('list');
        let tasks = JSON.parse(localStorage.getItem('tasks')) || [];

        function render() {
            list.innerHTML = '';
            tasks.forEach((t, i) => {
                let li = document.createElement('li');
                li.innerHTML = `<span>${t}</span>
          <div>
            <button class="edit" onclick="editTask(${i})">Edit</button>
            <button class="del" onclick="deleteTask(${i})">Delete</button>
          </div>`;
                list.appendChild(li);
            });
            localStorage.setItem('tasks', JSON.stringify(tasks));
        }

        function addTask() {
            if (input.value.trim()) {
                tasks.unshift(input.value.trim());
                input.value = '';
                render();
            }
        }

        function editTask(i) {
            let newText = prompt("Edit task:", tasks[i]);
            if (newText !== null && newText.trim()) {
                tasks[i] = newText.trim();
                render();
            }
        }

        function deleteTask(i) {
            if (confirm("Delete this task?")) {
                tasks.splice(i, 1);
                render();
            }
        }

        render();
    </script>
</body>

</html>
