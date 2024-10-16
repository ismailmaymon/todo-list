<template>
  <div @click="cancelDelete" v-if="isModalOpen"
    class="fixed inset-0 z-[100] flex items-center justify-center bg-gray-900 bg-opacity-50">
    <div class="bg-white max-w-auto max-w-full mx-5 p-6 rounded-lg shadow-xl" @click.stop>
      <h2 class="text-xl text-gray-700 font-semibold mb-4">Confirm Deletion</h2>
      <p>Are you sure you want to delete <span class="font-bold text-gray-800">{{ todoToDelete.name }}</span> ?</p>
      <div class="flex justify-end gap-4 mt-6">
        <button @click="cancelDelete" class="px-4 py-[7px] w-20 border border-blue-950 bg-blue-950 text-white hover:bg-opacity-95 transition ease-in-out duration-300 rounded-md">Cancel</button>
        <button @click="$emit('confirm-delete', todoToDelete)"
          class=" px-4 py-[7px] border border-blue-950 hover:bg-blue-950 w-20 flex justify-center items-center hover:text-white hover:bg-opacity-95 transition ease-in-out duration-300 rounded-md">
          <span>Delete</span>
        
        </button>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
  
    }
  },
  props: {
    isModalOpen: {
      type: Boolean,
      default: false
    },
    todoToDelete: Object
  },
  methods: {
    cancelDelete() {
      this.$emit('cancel-delete');
    }
  }
}
</script>