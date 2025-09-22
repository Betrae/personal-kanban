<template>
  <div>
    <!-- Task cards -->
    <div class="space-y-2 mb-2">
      <div
        v-for="(task, taskIndex) in tasks"
        :key="taskIndex"
      >
        <input
          type="text"
          v-model="task.title"
          class="input input-bordered input-sm w-full"
        />
      </div>
    </div>

    <!-- Add card input mode -->
    <div v-if="showInput" class="space-y-2">
      <input
        v-model="newTask"
        type="text"
        placeholder="Enter a title for this card..."
        class="input input-bordered input-sm w-full"
        ref="taskInput"
        @keyup.enter="saveTask"
      />
      <div class="flex gap-2">
        <button class="btn btn-sm btn-success" @click="saveTask">✔</button>
        <button class="btn btn-sm btn-error" @click="cancelTask">✖</button>
      </div>
    </div>

    <!-- Default button -->
    <button
      v-else
      class="btn btn-sm btn-outline w-full"
      @click="toggleInput"
    >
      + Add Card
    </button>
  </div>
</template>

<script>
export default {
  name: 'list-card',

  props: {
    tasks: {
      type: Array,
      required: true,
    },
  },

  emits: ['add-task'],

  data() {
    return {
      showInput: false,
      newTask: '',
    }
  },

  methods: {
    toggleInput() {
      this.showInput = true
      this.$nextTick(() => {
        this.$refs.taskInput?.focus()
      })
    },

    saveTask() {
      if (this.newTask.trim() !== '') {
        this.$emit('add-task', { title: this.newTask })
      }
      this.newTask = ''
      this.showInput = false
    },

    cancelTask() {
      this.newTask = ''
      this.showInput = false
    },
  },
}
</script>
