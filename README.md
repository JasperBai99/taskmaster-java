// Java project: TaskMaster

// Project Structure: taskmaster-java
// - backend (Spring Boot)
// - frontend (React)
// - docker

// backend/src/main/java/com/taskmaster/controller/TaskController.java

@RestController
@RequestMapping("/api/tasks")
public class TaskController {
    @Autowired
    private TaskService taskService;

    @GetMapping
    public List<Task> getAllTasks() {
        return taskService.getAllTasks();
    }

    @PostMapping
    public Task createTask(@RequestBody Task task) {
        return taskService.createTask(task);
    }

    @PutMapping("/{id}")
    public Task updateTask(@PathVariable Long id, @RequestBody Task task) {
        return taskService.updateTask(id, task);
    }

    @DeleteMapping("/{id}")
    public void deleteTask(@PathVariable Long id) {
        taskService.deleteTask(id);
    }
}

// frontend/src/pages/Dashboard.jsx

import React, { useEffect, useState } from 'react';
import axios from 'axios';

const Dashboard = () => {
  const [tasks, setTasks] = useState([]);

  useEffect(() => {
    axios.get('/api/tasks')
      .then(res => setTasks(res.data))
      .catch(err => console.error(err));
  }, []);

  return (
    <div>
      <h2>Project Dashboard</h2>
      <ul>
        {tasks.map(task => (
          <li key={task.id}>{task.title} - {task.status}</li>
        ))}
      </ul>
    </div>
  );
};

export default Dashboard;

// README.md for taskmaster-java

# 📝 TaskMaster - Enterprise Task Management System

A full-stack task management platform built with Spring Boot and React.js. Suitable for small to mid-sized teams needing organized workflow.

## ✨ Features
- User authentication & role-based access (Admin, Manager, Member)
- Task CRUD operations with status transitions (To Do → In Progress → Done)
- Dashboard with task stats and filters
- RESTful API design

## 🧰 Tech Stack
- Backend: Java, Spring Boot, MySQL, JPA, Spring Security, JWT
- Frontend: React, Axios, Ant Design
- DevOps: Docker, GitHub Actions

## 🚀 Getting Started
```bash
cd backend
./mvnw spring-boot:run

cd ../frontend
npm install && npm start
```

---

// Python project: InsightX

# Project Structure: insightx-python
# - app (FastAPI)
# - templates (Jinja2)
# - static

# app/main.py

from fastapi import FastAPI, UploadFile, File
import pandas as pd
from fastapi.responses import HTMLResponse
from starlette.templating import Jinja2Templates
from starlette.requests import Request

app = FastAPI()
templates = Jinja2Templates(directory="templates")

@app.get("/", response_class=HTMLResponse)
def index(request: Request):
    return templates.TemplateResponse("index.html", {"request": request})

@app.post("/upload")
def upload(file: UploadFile = File(...)):
    df = pd.read_csv(file.file)
    summary = df.describe().to_html()
    return {"summary": summary}

# templates/index.html

<!DOCTYPE html>
<html>
<head>
    <title>InsightX - Upload CSV</title>
</head>
<body>
    <h2>Upload CSV file</h2>
    <form action="/upload" method="post" enctype="multipart/form-data">
        <input type="file" name="file">
        <input type="submit" value="Upload">
    </form>
</body>
</html>

// README.md for insightx-python

# 📊 InsightX - Data Analytics Web Platform

A FastAPI-based lightweight platform that allows users to upload CSV data and receive instant statistical summaries.

## 💡 Features
- Upload CSV files via a simple web interface
- Automatically parses and generates descriptive statistics
- Future scope: chart visualization, AI-generated report summary (OpenAI)

## 🧰 Tech Stack
- Backend: Python, FastAPI, Pandas, Jinja2
- Frontend: HTML, CSS
- Deployment: Docker, Gunicorn, Nginx

## 🚀 Getting Started
```bash
cd app
uvicorn main:app --reload
```

Access at: http://localhost:8000/
