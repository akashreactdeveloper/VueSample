<template>
  <div class="tasks-container">
    <div
      v-for="(task, index) in tasks"
      :key="task.id"
      class="task-item"
      :class="{ locked: !task.unlocked, completed: task.completed }"
      @click="openTask(index)"
    >
      <div class="task-content">
        <h3>Task {{ index + 1 }}</h3>
        <p v-if="task.unlocked">{{ task.description }}</p>
        <p v-else><i class="fas fa-lock"></i> Locked</p>
      </div>
      <button v-if="task.unlocked && !task.completed" @click.stop="completeTask(index)">Mark as Complete</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        { id: 1, description: "Task 1", completed: false, unlocked: true },
        { id: 2, description: "Task 2", completed: false, unlocked: false },
        { id: 3, description: "Task 3", completed: false, unlocked: false },
        { id: 4, description: "Task 4", completed: false, unlocked: false },
        { id: 5, description: "Task 5", completed: false, unlocked: false },
      ],
    };
  },
  methods: {
    openTask(index) {
      if (this.tasks[index].unlocked) {
        alert(`Opening ${this.tasks[index].description}`);
      } else {
        alert("Complete the previous task to unlock this one!");
      }
    },
    completeTask(index) {
      this.tasks[index].completed = true;
      if (index + 1 < this.tasks.length) {
        this.tasks[index + 1].unlocked = true;
      }
    },
  },
};
</script>

<style scoped>
.tasks-container {
  display: flex;
  flex-direction: column;
  gap: 15px;
}
.task-item {
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 5px;
  background-color: #f9f9f9;
  position: relative;
  cursor: pointer;
  transition: 0.3s;
}
.task-item.locked {
  filter: blur(1px);
  cursor: not-allowed;
}
.task-item.completed {
  background-color: #d4f0d4;
}
.task-item .task-content i {
  color: #aaa;
  font-size: 16px;
}
button {
  margin-top: 10px;
}
</style>
