<template>
    <div class="buttons">
      <button class="btn" @click="prevPage">⬅ Back</button>
      <button class="btn" @click="nextPage">Next ➡</button>
    </div>
  </template>
  
  <script>
  import { computed } from "vue";
  import { useStore } from "vuex";
  
  export default {
    setup() {
      const store = useStore();
  
      const pageNext = computed(() => {
        return store.state.next;
      });
  
      const pagePrev = computed(() => {
        return store.state.prev;
      });
  
      const prevPage = () => {
        if (pagePrev.value) {
          store.dispatch("getCharacters", pagePrev.value);
        }
      };
  
      const nextPage = () => {
        if (pageNext.value) {
          store.dispatch("getCharacters", pageNext.value);
        }
      };
  
      return {
        prevPage,
        nextPage,
      };
    },
  };
  </script>
  