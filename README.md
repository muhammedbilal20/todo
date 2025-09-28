<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mobile-Friendly To-Do List</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 10px;
            color: #333;
        }

        .container {
            background: white;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            margin: 0 auto;
            max-width: 600px;
            width: 100%;
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            text-align: center;
        }

        h1 {
            font-size: clamp(1.8rem, 4vw, 2.5rem);
            font-weight: 600;
            margin-bottom: 5px;
        }

        .subtitle {
            opacity: 0.9;
            font-size: 0.9rem;
        }

        .content {
            padding: 20px;
        }

        .input-section {
            display: flex;
            gap: 8px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        #taskInput {
            flex: 1;
            min-width: 200px;
            padding: 16px;
            border: 2px solid #e1e5e9;
            border-radius: 12px;
            font-size: 16px;
            outline: none;
            transition: all 0.3s ease;
            background: #f8f9fa;
        }

        #taskInput:focus {
            border-color: #667eea;
            background: white;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        #addBtn {
            padding: 16px 24px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            transition: all 0.3s ease;
            min-height: 56px;
            white-space: nowrap;
        }

        #addBtn:hover {
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
        }

        #addBtn:active {
            transform: translateY(0);
        }

        .task-stats {
            display: flex;
            justify-content: space-between;
            background: #f8f9fa;
            padding: 15px;
            border-radius: 12px;
            margin-bottom: 20px;
            flex-wrap: wrap;
            gap: 10px;
        }

        .stat-item {
            text-align: center;
            flex: 1;
            min-width: 80px;
        }

        .stat-number {
            font-size: 1.5rem;
            font-weight: 700;
            color: #667eea;
            display: block;
        }

        .stat-label {
            font-size: 0.8rem;
            color: #666;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .task-list {
            list-style: none;
            max-height: 60vh;
            overflow-y: auto;
            padding-right: 5px;
        }

        .task-list::-webkit-scrollbar {
            width: 6px;
        }

        .task-list::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 3px;
        }

        .task-list::-webkit-scrollbar-thumb {
            background: #c1c1c1;
            border-radius: 3px;
        }

        .task-item {
            background: white;
            border: 2px solid #e9ecef;
            margin-bottom: 12px;
            padding: 16px;
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            transition: all 0.3s ease;
            position: relative;
            min-height: 60px;
        }

        .task-item:hover {
            border-color: #667eea;
            box-shadow: 0 4px 12px rgba(102, 126, 234, 0.1);
        }

        .task-item.completed {
            background: #f8fff8;
            border-color: #28a745;
        }

        .task-content {
            display: flex;
            align-items: center;
            flex: 1;
            min-width: 0;
        }

        .task-checkbox {
            margin-right: 15px;
            width: 22px;
            height: 22px;
            cursor: pointer;
            accent-color: #667eea;
        }

        .task-text {
            font-size: 16px;
            line-height: 1.4;
            word-wrap: break-word;
            transition: all 0.3s ease;
            flex: 1;
        }

        .task-text.completed {
            text-decoration: line-through;
            color: #888;
        }

        .delete-btn {
            background: #dc3545;
            color: white;
            border: none;
            padding: 10px 16px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 14px;
            font-weight: 500;
            transition: all 0.3s ease;
            margin-left: 10px;
            min-height: 40px;
            flex-shrink: 0;
        }

        .delete-btn:hover {
            background: #c82333;
            transform: scale(1.05);
        }

        .delete-btn:active {
            transform: scale(0.95);
        }

        .empty-state {
            text-align: center;
            padding: 40px 20px;
            color: #888;
        }

        .empty-icon {
            font-size: 3rem;
            margin-bottom: 15px;
            opacity: 0.5;
        }

        .empty-text {
            font-size: 1.1rem;
            margin-bottom: 8px;
        }

        .empty-subtext {
            font-size: 0.9rem;
            opacity: 0.7;
        }

        .clear-completed {
            width: 100%;
            padding: 12px;
            background: transparent;
            color: #dc3545;
            border: 2px solid #dc3545;
            border-radius: 8px;
            cursor: pointer;
            font-size: 14px;
            margin-top: 15px;
            transition: all 0.3s ease;
        }

        .clear-completed:hover {
            background: #dc3545;
            color: white;
        }

        /* Mobile specific styles */
        @media (max-width: 768px) {
            body {
                padding: 5px;
            }

            .content {
                padding: 15px;
            }

            .input-section {
                flex-direction: column;
            }

            #taskInput {
                min-width: 100%;
                margin-bottom: 10px;
            }

            #addBtn {
                width: 100%;
                padding: 18px;
            }

            .task-item {
                padding: 12px;
                flex-direction: column;
                align-items: stretch;
            }

            .task-content {
                margin-bottom: 10px;
            }

            .delete-btn {
                margin-left: 0;
                align-self: flex-end;
                min-width: 80px;
            }

            .task-stats {
                flex-direction: column;
                text-align: center;
            }

            .stat-item {
                margin-bottom: 10px;
            }
        }

        @media (max-width: 480px) {
            .header {
                padding: 15px;
            }

            .content {
                padding: 12px;
            }

            h1 {
                font-size: 1.6rem;
            }

            .task-text {
                font-size: 15px;
            }
        }

        /* Touch friendly improvements */
        @media (pointer: coarse) {
            .task-checkbox {
                width: 24px;
                height: 24px;
            }

            .delete-btn {
                min-height: 44px;
                min-width: 44px;
            }

            #addBtn {
                min-height: 48px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>📱 My Tasks</h1>
            <div class="subtitle">Stay organized, stay productive</div>
        </div>
        
        <div class="content">
            <div class="input-section">
                <input type="text" id="taskInput" placeholder="What needs to be done?" maxlength="200">
                <button id="addBtn">➕ Add</button>
            </div>
            
            <div class="task-stats" id="taskStats" style="display: none;">
                <div class="stat-item">
                    <span class="stat-number" id="totalTasks">0</span>
                    <div class="stat-label">Total</div>
                </div>
                <div class="stat-item">
                    <span class="stat-number" id="activeTasks">0</span>
                    <div class="stat-label">Active</div>
                </div>
                <div class="stat-item">
                    <span class="stat-number" id="completedTasks">0</span>
                    <div class="stat-label">Done</div>
                </div>
            </div>
            
            <ul class="task-list" id="taskList">
                <li class="empty-state">
                    <div class="empty-icon">📝</div>
                    <div class="empty-text">No tasks yet!</div>
                    <div class="empty-subtext">Add your first task above to get started</div>
                </li>
            </ul>
            
            <button class="clear-completed" id="clearCompleted" style="display: none;">
                🗑️ Clear Completed Tasks
            </button>
        </div>
    </div>

    <script>
        let tasks = [];
        let taskIdCounter = 1;

        const taskInput = document.getElementById('taskInput');
        const addBtn = document.getElementById('addBtn');
        const taskList = document.getElementById('taskList');
        const taskStats = document.getElementById('taskStats');
        const totalTasksEl = document.getElementById('totalTasks');
        const activeTasksEl = document.getElementById('activeTasks');
        const completedTasksEl = document.getElementById('completedTasks');
        const clearCompletedBtn = document.getElementById('clearCompleted');

        // Event listeners
        addBtn.addEventListener('click', addTask);
        taskInput.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                addTask();
            }
        });
        clearCompletedBtn.addEventListener('click', clearCompletedTasks);

        // Prevent zoom on iOS when focusing input
        if (/iPad|iPhone|iPod/.test(navigator.userAgent)) {
            taskInput.addEventListener('focus', function() {
                taskInput.style.fontSize = '16px';
            });
        }

        function addTask() {
            const taskText = taskInput.value.trim();
            
            if (taskText === '') {
                taskInput.focus();
                taskInput.style.borderColor = '#dc3545';
                setTimeout(() => {
                    taskInput.style.borderColor = '#e1e5e9';
                }, 1000);
                return;
            }

            const task = {
                id: taskIdCounter++,
                text: taskText,
                completed: false,
                createdAt: new Date().toISOString()
            };

            tasks.unshift(task); // Add to beginning
            taskInput.value = '';
            renderTasks();
        }

        function deleteTask(taskId) {
            tasks = tasks.filter(task => task.id !== taskId);
            renderTasks();
        }

        function toggleTask(taskId) {
            const task = tasks.find(task => task.id === taskId);
            if (task) {
                task.completed = !task.completed;
                renderTasks();
            }
        }

        function clearCompletedTasks() {
            if (confirm('Are you sure you want to clear all completed tasks?')) {
                tasks = tasks.filter(task => !task.completed);
                renderTasks();
            }
        }

        function updateStats() {
            const total = tasks.length;
            const completed = tasks.filter(task => task.completed).length;
            const active = total - completed;

            totalTasksEl.textContent = total;
            activeTasksEl.textContent = active;
            completedTasksEl.textContent = completed;

            // Show/hide stats and clear button
            if (total > 0) {
                taskStats.style.display = 'flex';
                clearCompletedBtn.style.display = completed > 0 ? 'block' : 'none';
            } else {
                taskStats.style.display = 'none';
                clearCompletedBtn.style.display = 'none';
            }
        }

        function renderTasks() {
            updateStats();
            taskList.innerHTML = '';

            if (tasks.length === 0) {
                taskList.innerHTML = `
                    <li class="empty-state">
                        <div class="empty-icon">📝</div>
                        <div class="empty-text">No tasks yet!</div>
                        <div class="empty-subtext">Add your first task above to get started</div>
                    </li>
                `;
                return;
            }

            // Sort tasks: active first, then completed
            const sortedTasks = [...tasks].sort((a, b) => {
                if (a.completed !== b.completed) {
                    return a.completed - b.completed;
                }
                return new Date(b.createdAt) - new Date(a.createdAt);
            });

            sortedTasks.forEach(task => {
                const taskItem = document.createElement('li');
                taskItem.className = `task-item ${task.completed ? 'completed' : ''}`;
                
                taskItem.innerHTML = `
                    <div class="task-content">
                        <input type="checkbox" class="task-checkbox" ${task.completed ? 'checked' : ''} 
                               onchange="toggleTask(${task.id})">
                        <span class="task-text ${task.completed ? 'completed' : ''}">${escapeHtml(task.text)}</span>
                    </div>
                    <button class="delete-btn" onclick="deleteTask(${task.id})" aria-label="Delete task">
                        🗑️
                    </button>
                `;
                
                taskList.appendChild(taskItem);
            });
        }

        function escapeHtml(text) {
            const div = document.createElement('div');
            div.textContent = text;
            return div.innerHTML;
        }

        // Handle page visibility changes to maintain focus
        document.addEventListener('visibilitychange', function() {
            if (!document.hidden && tasks.length === 0) {
                setTimeout(() => taskInput.focus(), 100);
            }
        });

        // Initial render
        renderTasks();
        
        // Auto-focus input on desktop
        if (window.innerWidth > 768) {
            taskInput.focus();
        }
    </script>
</body>
</html>
