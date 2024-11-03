<script>
import TodoList from './pages/TodoList.vue'
export default {
  components: {
    TodoList
  },
  data() {
    return {

    }
  },
  mounted() {
    this.$nextTick(() => {
      this.setScrollbarHeight();
      window.addEventListener('resize', this.setScrollbarHeight);
    });
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.setScrollbarHeight);
  },
  methods: {
    setScrollbarHeight() {
      const customScrollbar = this.$refs.customScrollbar;
      customScrollbar.style.maxHeight = '100vh'; 
    }
  }
}
</script>

<template>
  <section ref="customScrollbar" class="custom-scrollbar">
    <TodoList />
  </section>
</template>