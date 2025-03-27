# Task 04: To-Do Web Application

## Project Overview

A comprehensive to-do web application that enables users to add, organize, edit, and manage tasks. The application provides functionality to mark tasks as completed, set priority levels, and assign due dates and times to tasks.

## Features

- **Task Management**
  - Add new tasks with title and description
  - Mark tasks as completed
  - Edit existing tasks
  - Delete unwanted tasks
  - Set priority levels (Low, Medium, High)
  - Assign due dates and times to tasks

- **Organization & Filtering**
  - Filter tasks by status (All, Active, Completed)
  - Filter tasks by priority (High Priority)
  - Search functionality to find specific tasks
  - Automatic sorting by completion status, priority, and due date

- **User Interface**
  - Clean, intuitive design with modern aesthetics
  - Visual indicators for priority levels and completion status
  - Modal dialogs for editing tasks
  - Responsive design for all device sizes
  - Progress bars to visualize task completion

- **Data Persistence**
  - Local storage integration to save tasks between sessions
  - Tasks remain available after browser restart
  - Sample tasks added for demonstration on first use

## Technologies Used

- HTML5 for structure
- CSS3 for styling (flexbox, grid, custom properties, animations)
- Vanilla JavaScript for application logic
- LocalStorage API for data persistence
- No external libraries or frameworks

## Implementation Details

### Task Data Structure

Each task is represented as an object with the following properties:

```javascript
const task = {
    id: Date.now(),  // Unique identifier
    title: "Task title",
    description: "Task description",
    date: "2025-03-28",  // Due date in YYYY-MM-DD format
    time: "14:30",  // Due time in 24-hour format
    priority: "medium",  // low, medium, or high
    completed: false,
    createdAt: new Date().toISOString()
};
```

### Task Filtering System

The application implements a flexible filtering system:

```javascript
function renderTasks() {
    const searchTerm = searchInput.value.toLowerCase();
    let filteredTasks = [...tasks];
    
    // Apply search filter
    if (searchTerm) {
        filteredTasks = filteredTasks.filter(task => 
            task.title.toLowerCase().includes(searchTerm) || 
            task.description.toLowerCase().includes(searchTerm)
        );
    }
    
    // Apply status filter
    switch (currentFilter) {
        case 'active':
            filteredTasks = filteredTasks.filter(task => !task.completed);
            break;
        case 'completed':
            filteredTasks = filteredTasks.filter(task => task.completed);
            break;
        case 'high':
            filteredTasks = filteredTasks.filter(task => task.priority === 'high');
            break;
    }
    
    // Sort tasks by priority, due date, etc.
}
```

### Local Storage Integration

Tasks are preserved between sessions using browser localStorage:

```javascript
// Save tasks to localStorage
function saveTasks() {
    localStorage.setItem('tasks', JSON.stringify(tasks));
}

// Load tasks from localStorage on application startup
let tasks = JSON.parse(localStorage.getItem('tasks')) || [];
```

### Date and Time Formatting

The application formats dates and times for better readability:

```javascript
function formatDate(dateStr, timeStr) {
    if (!dateStr) return 'No due date';
    
    const date = new Date(dateStr);
    const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
    const formattedDate = date.toLocaleDateString('en-US', options);
    
    if (timeStr) {
        return `${formattedDate} at ${formatTime(timeStr)}`;
    }
    
    return formattedDate;
}

function formatTime(timeStr) {
    if (!timeStr) return '';
    
    const [hours, minutes] = timeStr.split(':');
    const h = parseInt(hours, 10);
    const period = h >= 12 ? 'PM' : 'AM';
    const hour = h % 12 || 12;
    
    return `${hour}:${minutes} ${period}`;
}
```

## How to Use

1. Clone this repository
2. Open `index.html` in any modern web browser

### Task Management

- **Adding Tasks:**
  - Fill in the task title (required)
  - Add an optional description
  - Set a due date and time if needed
  - Select a priority level (Low, Medium, High)
  - Click "Add Task"

- **Completing Tasks:**
  - Click the "Complete" button to mark a task as done
  - Click "Undo" to mark a completed task as active again

- **Editing Tasks:**
  - Click the "Edit" button on any task
  - Update any details in the modal dialog
  - Click "Save Changes" to update the task

- **Deleting Tasks:**
  - Click the "Delete" button to remove a task
  - Confirm the deletion when prompted

### Filtering and Searching

- Use the filter options to view specific groups of tasks:
  - "All" - Shows all tasks
  - "Active" - Shows only incomplete tasks
  - "Completed" - Shows only completed tasks
  - "High Priority" - Shows only high-priority tasks

- Type in the search box to find tasks by title or description

## Responsive Design

The application is fully responsive and works on all device sizes:

```css
@media screen and (max-width: 768px) {
    .date-time-container {
        flex-direction: column;
    }

    .task-filter {
        flex-direction: column;
    }
    
    /* Additional responsive styling */
}

@media screen and (max-width: 480px) {
    .app-title {
        font-size: 2rem;
    }
    
    /* More mobile-specific styles */
}
```

## Future Enhancements

- Add task categories/tags
- Implement recurring tasks
- Add notifications for upcoming due dates
- Create multiple task lists/projects
- Add task sharing capabilities
- Implement drag-and-drop for task reordering
- Add dark/light theme toggle

## Screenshots


## License

This project is part of the SkillCraft Technology internship program.
