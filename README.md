# Vue.js + Bootstrap Coding Assignment

This is a simple To-Do List web application using Vue.js for functionality and Bootstrap for
 styling. This application allows users to add, delete, and filter tasks. It also saves tasks in local storage for persistence.

## Features

### 1. **Local Storage Usage**
   - The app utilizes the browser’s `localStorage` to persist todos. This ensures that your tasks are saved even after the page is refreshed or the browser is closed. When the app is launched, it retrieves the saved tasks from `localStorage` and displays them.

### 2. **Add and Delete Tasks**
   - Users can easily add new tasks through an input field. Each task can also be deleted with a single click, removing it from the list and updating both the UI and local storage.

### 3. **Display Total Tasks**
   - The total number of tasks is dynamically displayed in the app header. This count updates automatically whenever tasks are added or removed, giving users a quick overview of how many tasks they have.

### 4. **Display Completed Tasks**
   - A counter shows how many tasks have been marked as completed. This feature helps users track their progress at a glance by comparing completed tasks to the total tasks.

### 5. **Mark Tasks as Complete**
   - Each task can be marked as completed with a checkbox. Completed tasks are visually distinguished (e.g., strikethrough) from pending tasks. The state of each task is stored in local storage to ensure persistence across sessions.

### 6. **Filter Tasks**
   - The app provides filtering options that allow users to display:
     - **All tasks**: Shows both completed and pending tasks.
     - **Pending tasks**: Displays only the tasks that are yet to be completed.
     - **Completed tasks**: Filters and shows only the tasks that have been marked as completed.
     
## Getting Started

1. **Clone the repository**:
   ```bash
   git clone https://github.com/Nathaniyell/vue-todo-app
   cd vue-todo-app
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Run the development server**:
   ```bash
   npm run dev
   ```

4. **Build for production**:
   ```bash
   npm run build
   ```

5. **Preview the build**:
   ```bash
   npm run preview
   ```

## Technologies Used
- **Vue 3**: The progressive JavaScript framework.
- **Composition API**: A more flexible and powerful way to write Vue components.
- **LocalStorage**: Browser storage for persisting tasks across sessions.

## Conclusion

This Todo app is a great way to manage daily tasks, with real-time updates, task filtering, and automatic state persistence. It's lightweight, responsive, and easy to use!