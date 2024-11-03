<template>
  <div
    @click="cancelDelete"
    v-if="isModalOpen"
    class="fixed inset-0 z-[100] flex items-center justify-center bg-gray-900 bg-opacity-50"
  >
    <div
      class="bg-white max-w-xl sm:mx-auto mx-4 w-full rounded-lg shadow-xl"
      @click.stop
    >
      <header class="border-b flex items-center justify-between px-4 py-3">
        <h2 class="text-xl text-gray-900 font-semibold">Confirm Delete</h2>
        <button
          @click="cancelDelete"
          class="h-8 w-8 hover:bg-gray-100 flex items-center justify-center rounded-lg"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="size-6 text-gray-600"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M6 18 18 6M6 6l12 12"
            />
          </svg>
        </button>
      </header>
      <div class="px-4 py-3 sm:min-h-40 min-h-36">
        <p class="text-lg">
          Are you sure you want to delete
          <span class="font-bold text-gray-800">{{ todoToDelete.name }}</span> ?
        </p>
      </div>
      <footer class="flex justify-end gap-4 border-t px-4 py-3">
        <button
          @click="cancelDelete"
          class="px-4 py-[7px] w-[90px] font-medium border hover:bg-gray-100 hover:text-blue-950 transition ease-in-out duration-300 rounded-lg"
        >
          Close
        </button>
        <button
          @click="$emit('confirm-delete', todoToDelete)"
          class="px-4 py-[7px] border border-blue-950 bg-blue-950 w-[90px] font-medium flex justify-center items-center text-white hover:bg-opacity-85 transition ease-in-out duration-300 rounded-lg"
        >
          <span>Confirm</span>
        </button>
      </footer>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: {
    isModalOpen: {
      type: Boolean,
      default: false,
    },
    todoToDelete: Object,
  },
  methods: {
    cancelDelete() {
      this.$emit("cancel-delete");
    },
  },
};
</script>