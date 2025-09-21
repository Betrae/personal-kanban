<template>
  <div>
    <!-- Editable column title -->
      <input
        type="text"
        v-model="column.title"
        placeholder="List title"
        class="bg-transparent focus:outline-none text-lg font-bold flex-1"
      />

    <!-- Kebab -->
      <div class="absolute top-2 right-2 dropdown dropdown-end">
        <label tabindex="0" class="btn btn-ghost btn-sm">⋯</label>
        <ul tabindex="0" class="dropdown-content menu p-2 shadow rounded-box w-40 bg-gray-800 text-white">
          <li>
            <button
              class="w-full text-left px-2 py-1 hover:bg-gray-700 rounded"
              @click="$emit('delete-column')"
            >
              Delete
            </button>
          </li>
        </ul>
      </div>
  </div>
</template>

<script>
export default {
  name: 'list-board',
  props: {
    column: {
      type: Object,
      required: true
    }
  }
}
</script>

<style>

</style>
