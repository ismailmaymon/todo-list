<template>
  <div class="relative h-screen">
    <div class="mx-auto sm:container sm:pt-20 sm:pb-8 pb-5 pt-5 sm:px-5 px-4">
      <h1 class="sm:text-3xl text-2xl font-medium text-blue-950">Todo List</h1>
      <div v-if="todoList.length === 0" class="text-blue-950 mt-10 text-center text-2xl">Your todo list is empty.</div>

      <div v-else class="sm:mt-6">
        <div class="bg-blue-950 shadow w-full rounded-xl sm:px-6 px-4 sm:py-3 py-[10px] sm:my-5 my-4 flex justify-between"
          v-for="(item, index) in todoList" :key="index">
          <div class="">
            <label @click="toggleRecycle(index)" class="flex sm:gap-4 gap-3 items-center cursor-pointer">
              <input type="checkbox" name="" id="" class="sm:h-4 sm:w-4 h-[16px] w-[16px] cursor-pointer"
                v-if="item.isTrueRecycle === true">
              <h1 v-if="item.isTrueRecycle === true" class="text-white text-lg sm:text-2xl">{{ item.name }}</h1>
              <strike v-if="item.isTrueRecycle === false" class="text-white text-lg sm:text-2xl">{{ item.name }}</strike>
            </label>
          </div>
          <div class="flex items-center sm:gap-3 gap-2">
            <svg @click="toggleRecycle(index)" v-if="item.isTrueRecycle === false" xmlns="http://www.w3.org/2000/svg"
              class="text-white sm:h-5 sm:w-5 h-5 w-5 cursor-pointer transition ease-in-out duration-300 hover:opacity-80 icon icon-tabler icon-tabler-refresh"
              viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" fill="none" stroke-linecap="round"
              stroke-linejoin="round">
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path d="M20 11a8.1 8.1 0 0 0 -15.5 -2m-.5 -4v4h4" />
              <path d="M4 13a8.1 8.1 0 0 0 15.5 2m.5 4v-4h-4" />
            </svg>

            <svg @click="openDeleteModal(item)" xmlns="http://www.w3.org/2000/svg"
              class="text-white sm:h-5 sm:w-5 h-5 w-5 cursor-pointer transition ease-in-out duration-300 hover:opacity-80 icon icon-tabler icon-tabler-trash"
              viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" fill="none" stroke-linecap="round"
              stroke-linejoin="round">
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path d="M4 7l16 0" />
              <path d="M10 11l0 6" />
              <path d="M14 11l0 6" />
              <path d="M5 7l1 12a2 2 0 0 0 2 2h8a2 2 0 0 0 2 -2l1 -12" />
              <path d="M9 7v-3a1 1 0 0 1 1 -1h4a1 1 0 0 1 1 1v3" />
            </svg>
          </div>
        </div>
      </div>
    </div>
    <div>
      <DeleteTodoModal :isModalOpen="deleteModalOpen" :todoToDelete="todoToDelete" @cancel-delete="cancelDelete"
        @confirm-delete="deleteTodo" />
    </div>
    <div>
      <AddTodoModal :isModalOpen="addModalOpen" @closeModal="addModalOpen = false" :addTodo="todoList"/>
    </div>
    <div class="pt-10">
      <div class="fixed bottom-8 sm:right-10 right-6">
        <div class="bg-blue-900 hover:opacity-80 transition ease-in-out duration-300 p-1 rounded-lg cursor-pointer" @click="openAddModal">
          <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-plus text-white h-8 w-8"
            viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" fill="none" stroke-linecap="round"
            stroke-linejoin="round">
            <path stroke="none" d="M0 0h24v24H0z" fill="none" />
            <path d="M12 5l0 14" />
            <path d="M5 12l14 0" />
          </svg>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import AddTodoModal from '../components/AddTodoModal.vue';
import DeleteTodoModal from '../components/DeleteTodoModal.vue';

export default {
  components: {
    AddTodoModal,
    DeleteTodoModal
  },
  data() {
    return {
      todoList: [
        {
          name: "Gym",
          isTrueRecycle: true
        },
        {
          name: "Study",
          isTrueRecycle: true
        },
        {
          name: "Work",
          isTrueRecycle: true
        },
        {
          name: "Cook",
          isTrueRecycle: false
        },
        {
          name: "Clean",
          isTrueRecycle: true
        },
        {
          name: "Walk",
          isTrueRecycle: true
        },
        {
          name: "Read",
          isTrueRecycle: true
        },
        {
          name: "Sleep",
          isTrueRecycle: true
        },
        {
          name: "Play",
          isTrueRecycle: true
        },
        {
          name: "Relax",
          isTrueRecycle: false
        },
      ],
      deleteModalOpen: false,
      addModalOpen: false,
      todoToDelete: null
    }
  },
  methods: {
    openDeleteModal(todo) {
      this.todoToDelete = todo;
      this.deleteModalOpen = true;
    },
    openAddModal() {
      this.addModalOpen = true;
    },
    cancelDelete() {
      this.deleteModalOpen = false;
      this.addModalOpen = false;
      this.todoToDelete = null;
    },
    deleteTodo(todoToDelete) {
      const index = this.todoList.indexOf(todoToDelete);
      if (index !== -1) {
        this.todoList.splice(index, 1);
      }
      this.deleteModalOpen = false;
      this.todoToDelete = null;
    },
    toggleRecycle(index) {
      this.todoList[index].isTrueRecycle = !this.todoList[index].isTrueRecycle;
    }
  }
}
</script>
