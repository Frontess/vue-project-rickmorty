<template>
<div>
<div className="wrapper">
    <h1>Приложение о героях Rick and Morty</h1>
    <p>Посмотреть имя или статус персонажа {{ userInput == "" ? "Rick and Morty" : '"'+userInput+'"' }}</p>
    <input type="text" v-model="userInput" placeholder="Введите имя персонажа">
    
    <button v-if="userInput != ''" @click="getUserInput()">Применить</button>
    <button disabled v-else>Введите персонажа</button>

    <p className="error"> {{ error }}</p>

    <div className="cards" v-if="info">
      <div v-for="character in info.results" :key="character.id">

      <div className="card-item">
        <div className="card-image">
          <img :src="character.image" alt="Character Image" />
        </div>
          <div className="card-content">
          <h3 className="card-name">{{ character.name }}</h3>
          <p className="card-status">Status: {{ character.status }}</p>
        </div>
      </div>

      </div>
    </div>
</div>
</div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      userInput: '',
      error: "",
      info: null,
    }
  },
  methods: {
    getUserInput() {
      if(this.userInput.trim().length < 2) {
        this.error = ";) Нужно ввести больше одной буквы"
        return false;
      }
      this.error = ""
      axios.get(`https://rickandmortyapi.com/api/character/?name=${this.userInput}&status=alive`)
      .then(result => (this.info = result.data ))
      .catch(error => {
          console.error('Ошибка при получении данных о персонажах:', error);
          this.info = null;
        });
    }

  }
}
</script>

<style scoped>
.cards {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  width: 1200px;
  height: 100vh;
  margin-top: 80px;
  margin-bottom: 20px;
}
.error {
  color: red;
}
.wrapper {
  width: 1200px;
  height: 200px;
  border-radius: 50px;
  padding: 10px;
  margin-top: 20px;
  background: #c1d2d2;
  text-align: center;
  color: black;
}

.wrapper h1 {
  margin-top: 50px;
} 

.wrapper p {
  margin-top: 5px;
}
.wrapper input {
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid black;
  color: #053a6c;
  font-size: 14px;
  padding: 5px 50px;
  outline: none;
  cursor: pointer;
}
.wrapper input:hover {
  border-bottom-color: #f7d61e;
}
.wrapper button {
  background: #149c9c;
  color: black;
  border-radius: 10px;
  border: 2px solid #126d6d;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}
.wrapper button:disabled {
  background: #126d6d;
  color: #c1d2d2;
  cursor: not-allowed;
}
.wrapper button:hover {
  transform: scale(1.1) translateY(-5px);
}

.card-item {
  margin-right: 10px;
  margin-top: 30px;
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
width: 200px;
height: 300px;
border-radius: 10px;
background-color: #c1d2d2;
}
</style>