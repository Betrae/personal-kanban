<template>
  <div class="container mx-auto p-4">
    <h1 class="text-3xl font-bold mb-6 text-center">Kanban</h1>

    <div class="flex flex-wrap gap-6 items-start">
      <div
        v-for="(column, index) in columns"
        :key="index"
        class="card w-80 bg-base-100 shadow-xl flex-shrink- relative"
      >

      <ListBoard
        :column="column"
        @delete-column="deleteColumn(index)" />
        <div class="card-body">

          <!-- Task cards -->
          <div class="space-y-2 mb-2">
            <div
              v-for="(task, taskIndex) in column.tasks"
              :key="taskIndex"
              class="card p-3 bg-primary text-primary-content shadow flex justify-between items-center"
            >
              <span>{{ task.title }}</span>
              <button class="btn btn-xs btn-circle btn-outline" @click="removeTask(index, taskIndex)">×</button>
            </div>
          </div>

          <!-- Button to add a task -->
          <button class="btn btn-sm btn-outline w-full" @click="addTask(index)">
            + Add Card
          </button>
        </div>
      </div>
    </div>
    <button
      class="btn btn-primary fixed bottom-20 right-10 z-50"
      @click="addColumn"
    >
      + Add List
    </button>
  </div>
</template>

<script>
import ListBoard from '@/components/layouts/ListBoard.vue'
export default {
  name: "kan-ban",
  components: {
    ListBoard
  },
  data() {
    return {
      columns: [],
      columnInfo: {
        title: '',
        tasks: []
      }
    }
  },
  methods: {
    addColumn() {
      this.columns.push({ ...this.columnInfo })
    },
    deleteColumn (index) {
      this.columns.splice(index, 1)
    },
    addTask(columnIndex) {
      const title = prompt('Enter task title:')
      if (title) {
        this.columns[columnIndex].tasks.push({ title })
      }
    },
    removeTask(columnIndex, taskIndex) {
      this.columns[columnIndex].tasks.splice(taskIndex, 1)
    }
  }
}
</script>

<style scoped>
.input:focus {
  border-color: #646cff;
  box-shadow: 0 0 0 2px rgba(100,108,255,0.3);
}
</style>
