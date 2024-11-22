<template>
    <h1 :style="{color: count === 5 ? 'red' : 'green'}">Hello {{ prenom.toUpperCase() }}</h1>
    <p>Ceci est une page avec plein d'exemple</p>
    <!-- v-show et v-hide sont des sortes de conditions (attention elles restent dans le code meme si elles ne sont pas montrés)
     v-if et v-else sont dans le meme principe mais supprime l'élément du DOM lorsque la condition est remplis -->
    <div v-show="count === 5">Bravo neuilles t'as cliqué 5 fois</div>
  
    <!-- v-bind permet d'avoir des éléments dynamique (avec les : la valeurs peut-etre interprete ) -->
    <p :id="count" :class="{5 : count ===5}">Compteur : {{ count }}</p> 
    <!-- comme pour le style tu peux très bien mettre une condition pour une classe -->
    <!-- pour mettre qlq chose dans le 'template' tu met ça : {{  }} -->
     <button v-on:click="count++">Incrément</button>
     <!-- si la fonction est petite on peut juste la mettre dedans sans prendre la valeur ref et juste la const -->
     <button @click="decrement">Décrémente</button>
    <!-- v-on = addEventlistener / @ est plus simple d'utilisation -->
  
    <button @click="sortMovies">Réorganiser</button>
  
  
     <hr>
    <!-- v-for est une sortes de foreach -->
     <ul>
      <li v-for="movie in movies" :key="movie" :class="movie">
        {{ movie }} <button @click="deleteMovie(movie)">Supprimer</button>
      </li>
     </ul>
  
     <hr>
  
     <form action="" @submit.prevent="addMovie">
      <h3>Ajouter un film : </h3>
      <input type="text" placeholder="Titre du Film" v-model="movieName">
      {{ movieName }} <button>Ajouter</button>
     </form>
  
  </template>
  
  <script setup>
  import {ref} from 'vue'
  
  
  //constantes 
  const prenom = "Ywen"
  const count = ref(0)
  const movies = ref([
    'spiderman',
    'batman',
    'tompere'
  ])
  const movieName = ref('')
  //methodes 
  
  const increment = () => {
    count.value++
  }
  
  const decrement = () => {
    count.value--
  }
  
  const deleteMovie = (movie) => {
    movies.value = movies.value.filter(m => m != movie)
  }
  
  const sortMovies = () => {
    movies.value.sort((a,b) => a > b ? 1 : -1)
  }
  
  const addMovie = () => {
    movies.value.push(movieName.value)
    movieName.value =''
  }
  </script>
  
  <style>
  
  </style>