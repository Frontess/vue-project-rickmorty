<template>
    <div className="button">
      <button @click="getData(pagination.currentPage-1)">Предыдущая страница</button>
      <p>Текущая страница {{pagination.currentPage}}</p>
  
     <button @click="getData(pagination.currentPage+1)">Следующая страница</button>
    </div>
  </template>
  
  <script>
  export default {
     name: "App",
     data(){
       return {
         pagination:{
          currentPage: 1,
          nextPage:null,
          prevPage:null
         },
         
         data:[],
          url:"https://rickandmortyapi.com/api/character"
       }
     },
     created(){
      this.getData()
     },
     methods:{
       async getData(pageNumber){
  
          const response=await fetch(this.url+"?page="+(pageNumber||this.pagination.currentPage))
          const {results,info}=await response.json()
          this.data=results
          this.pagination={
            currentPage:pageNumber?pageNumber:1,
            nextPage:info.next,
            prevPage:info.prev
          }
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
  margin-top: 20px;
  margin-bottom: 20px;
}

.card-item {
  margin-right: 10px;
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
</style>
