<template>
  <div>
    <transition name="modal-fade" appear>
      <div
        @click="$emit('closeModal')"
        @touchstart="handleTouchStart"
        @touchmove="handleTouchMove"
        @touchend="handleTouchEnd"
        v-if="isModalOpen"
        class="fixed inset-0 z-50 flex items-center justify-end bg-black bg-opacity-50"
      >
        <div
          class="bg-white sm:max-w-[450px] w-full sm:ml-0 ml-14 h-full"
          @click.stop
        >
          <div class="h-full">
            <div
              class="border-b flex justify-between items-center sm:px-5 px-4 py-3"
            >
              <h1 class="text-blue-950 text-2xl">Add Todo</h1>
              <svg
                @click="$emit('closeModal')"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="text-blue-950 w-6 h-6 cursor-pointer hover:opacity-80 transition ease-in-out duration-300"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M6 18 18 6M6 6l12 12"
                />
              </svg>
            </div>
            <div class="mt-4 h-full">
              <div class="sm:px-5 px-4">
                <label for="">Type a Todo</label>
                <input
                  v-model="name"
                  type="text"
                  :class="`border mt-2 w-full focus:outline-none px-4 sm:py-2 py-[7px] rounded-lg text-lg ${
                    errors.name ? 'border-red-500' : 'focus:border-blue-950'
                  }`"
                />
                <!-- Reserve space for error text with min-height -->
                <div class="min-h-[20px] mt-[2px]">
                  <h6 class="text-red-500 text-[13px]" v-if="errors.name">
                    {{ errors.name }}
                  </h6>
                </div>
              </div>
              <div
                class="w-full sm:h-[calc(100%-193px)] h-[calc(100%-185px)] flex items-end"
              >
                <div class="border-t w-full sm:px-5 px-4 sm:pt-5 pt-4">
                  <button
                    @click="handleAdd"
                    class="bg-blue-950 sm:text-xl text-lg px-4 sm:py-2 py-[7px] w-full text-white rounded-lg cursor-pointer hover:opacity-85 transition ease-in-out duration-300"
                  >
                    Add
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import { object, string } from "yup";
import { useForm, useField } from "vee-validate";

export default {
  props: {
    addTodo: Function,
    isModalOpen: Boolean,
  },
  setup(props, { emit }) {
    const schema = object({
      name: string().required("Name is required!"),
    });

    const { errors, validate, resetForm } = useForm({
      validationSchema: schema,
      initialValues: {
        name: "",
      },
    });

    const { value: name } = useField("name");

    const handleAdd = async () => {
      const { valid } = await validate();
      if (!valid) {
        console.error("Validation failed:", errors.value);
        return;
      }

      props.addTodo.push({
        name: name.value,
        isTrueRecycle: true,
      });

      name.value = ""; // Clear the input field
      resetForm(); // Reset form validation
      emit("closeModal");
    };

    return {
      errors,
      validate,
      name,
      handleAdd,
    };
  },
  data() {
    return {};
  },
  methods: {
    handleTouchStart(event) {
      this.touchStartX = event.touches[0].clientX;
    },
    handleTouchMove(event) {
      const touchMoveX = event.touches[0].clientX;
      if (touchMoveX - this.touchStartX > 50) {
        // Handle swipe right
      }
    },
    handleTouchEnd(event) {
      const touchEndX = event.changedTouches[0].clientX;
      if (touchEndX - this.touchStartX > 50) {
        this.$emit("closeModal");
      }
    },
  },
};
</script>

<style scoped>
.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity 0.2s;
}

.modal-fade-enter,
.modal-fade-leave-to {
  opacity: 0;
}
</style>
