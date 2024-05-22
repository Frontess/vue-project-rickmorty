<template>

  <Input />
  <Characters :applyFilter="applyFilter"/>
  <Pagination />
  
 
</template>
  
<script>
import Characters from './components/Characters.vue';
import Input from './components/Input.vue';
import Pagination from './components/Pagination.vue';


export default {
  components: { Characters, Input, Pagination },
 
  mounted() {
    this.applyFilter(); // Вызов метода при загрузке страницы
  },
  methods: {
    async applyFilter() {
      try {
        const response = await fetch('https://rickandmortyapi.com/api/character');
        const data = await response.json();
        this.characters = data.results;
      } catch (error) {
        console.error('Ошибка при получении данных о персонажах:', error);
      }
    }
    
  }
};

</script>

<style>
</style> 
