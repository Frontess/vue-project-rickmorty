<template>
  <div>
    <select className="select" v-model="filter" @change="applyFilter">
      <option>Выбор статуса персонажа</option>
      <option value="All">All</option>
      <option value="Alive">Alive</option>
      <option value="Dead">Dead</option>
      <option value="Unknown">Unknown</option>
    </select>
  </div>
    <!-- Отображение карточек персонажей -->
    <div className="cards">
      <div className="card-item" v-for="character in filteredCharacters" :key="character.id">
       <div className="card-image"><img :src="character.image" alt="Character Image" /></div>
       <div className="card-content">
          <h3 className="card-name">{{ character.name }}</h3>
          <p className="card-status">Status: {{ character.status }}</p>
        </div>
      </div>
   </div>
</template>

<script>

import { onMounted } from 'vue';

export default {
  setup() {
    onMounted(() => {
      this.applyFilter();
    });
  },
  data() {
    return {
      filter: 'Выбор статуса персонажа',
      characters: [] // данные о персонажах
    };
  },
  computed: {
    filteredCharacters() {
      if (this.filter === 'All') {
        return this.characters;
      } else {
        return this.characters.filter(character => character.status === this.filter);
      }
    }
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
<style scoped>
.cards {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  width: 1200px;
  margin-top: 20px;
  margin-bottom: 20px;
}

img {
  height: 100%;
  border-radius: 10px 10px 0px 0px;
  cursor: pointer;
}

.card-content {
  font-size: 16px;
  font-weight: 300;
}

.card-name {
  font-size: 14px;
  font-weight: 700;
  margin-top: 15px;
  margin-bottom: 15px;
}
.card-item {
margin: 10px;
margin-top: 30px;
width: 200px;
height: 300px;
border-radius: 10px;
background-color: #c1d2d2;
}

.button {
  display: flex;
  justify-content: center;
}

.button p {
  font-family: 'Kanit', cursive;
  font-size: 16px;
}
.button button {
  background: #149c9c;
  color: black;
  border-radius: 10px;
  border: 2px solid #126d6d;
  padding: 10px 15px;
  margin-left: 20px;
  margin-right: 20px;
  margin-bottom: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}
.button button:hover {
  transform: scale(1.1) translateY(-5px);
}
.button button:active {
  border: 2px solid #e1ecec;
  transform: scale(1.1);
}
.select {
  margin-top: 20px;
  height: 20%;
  width: 20%;
  font-family: 'Kanit', cursive;
  font-size: 16px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background: transparent;
  color: #c1d2d2;
  cursor: pointer;
  transition: border-color 0.3s ease;
}

.select:hover {
  border-color: #999;
}

/* Стили для опций в выпадающем списке */
.select option {
  font-weight: normal;
  background-color: #f9f9f9;
  color: #333;
}

/* Стили для выбранной опции */
.select option:checked {
  font-weight: bold;
  background-color: #e0e0e0;
}
</style>