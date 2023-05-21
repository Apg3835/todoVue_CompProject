<template>
  <div className="container">
    <h1>To-do List</h1>

    <input v-model="taskText" type="text" placeholder="Enter a task" className="inputTask">
    <button @click="addTask" className="addTodo">Add Task</button>

    <h2>Tasks:</h2>
    <ul>
      <li v-for="(task, index) in tasks" :key="index" @click="toggleTaskCompletion(index)" :class="{ 'completed': task.completed }">
        {{ task.text }}
      </li>
    </ul>

    <h2>Folders:</h2>
    <ul>
      <li v-for="(folder, index) in folders" :key="index" @click="selectFolder(index)" :class="{ 'selected': selectedFolder === index }">
        {{ folder.name }}
      </li>
    </ul>

    <input v-model="newFolderName" type="text" placeholder="Enter folder name" className="inputFolder">
    <button @click="addFolder" className="addFolder">Create Folder</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      taskText: '',
      tasks: [],
      folders: [],
      selectedFolder: null,
      newFolderName: '',
    };
  },
  methods: {
    addTask() {
      if (this.taskText.trim() !== '') {
        const task = {
          text: this.taskText,
          completed: false
        };
        this.tasks.push(task);
        this.taskText = '';
      }
    },
    toggleTaskCompletion(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    },
    addFolder() {
      if (this.newFolderName.trim() !== '') {
        const folder = {
          name: this.newFolderName,
          tasks: []
        };
        this.folders.push(folder);
        this.newFolderName = '';
      }
    },
    selectFolder(index) {
      this.selectedFolder = index;
      this.tasks = this.folders[index].tasks;
    }
  }
};
</script>

<style>
.container {
  border: 2px solid black;
  padding:auto;
margin:auto;
text-align:center;
width:50%;
background-color: rgb(162, 255, 255);
}
.inputTask{
  border: 2px solid rgb(15, 14, 14);
  border-radius: 8px;
  padding: 5px;
}
.inputFolder{
  border: 2px solid rgb(15, 14, 14);
  border-radius: 8px;
  padding: 5px;
  margin-left: 25px;
  margin-bottom: 10px
}
.addTodo{
  margin-left: 2px;
  border: 2px solid rgb(15, 14, 14);
  border-radius: 8px;
  padding: 4px;
}
.addFolder{
  margin-left: 2px;
  border: 2px solid rgb(15, 14, 14);
  border-radius: 8px;
  padding: 4px;
}
.completed {
  text-decoration: line-through;
}
.selected {
  font-weight: bold;
}
</style>