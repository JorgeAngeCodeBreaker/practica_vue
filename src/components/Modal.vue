<template>
    <div class="modal" v-if="showModal">
      <div class="modal-content">
        <span class="close" @click="closeModal">&times;</span>
        <h2>Ingresa los datos de la película</h2>
        <div>
          <label for="movie-title">Título:</label>
          <input type="text" id="movie-title" v-model="title">
        </div>
        <div>
          <label for="movie-genre">Género:</label>
          <select id="movie-genre" v-model="selectedGenre">
            <option v-for="genre in genres" :key="genre.id" :value="genre">{{ genre.name }}</option>
          </select>
        </div>
        <div>
          <label for="movie-year">Año:</label>
          <input type="number" id="movie-year" v-model="year">
        </div>
        <button @click="saveMovie">Guardar</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        showModal: false,
        title: '',
        selectedGenre: null,
        genres: [],
        year: ''
      };
    },
    mounted() {
      // Llamar a la función para cargar los géneros cuando se monte el componente
      this.loadGenres();
    },
    methods: {
      openModal() {
        this.showModal = true;
      },
      closeModal() {
        this.showModal = false;
      },
      loadGenres() {
        fetch('http://localhost:8080/api/movies/genres')
          .then(response => response.json())
          .then(data => {
            this.genres = data;
            this.selectedGenre = data[0]; // Establecer el primer género como seleccionado por defecto
          })
          .catch(error => {
            console.error('Error al cargar los géneros:', error);
          });
      },
      saveMovie() {
        const movie = {
          name: this.title,
          genre: this.selectedGenre,
          year: parseInt(this.year)
        };
  
        fetch('http://localhost:8080/api/movies/movies', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(movie)
        })
        .then(response => response.text())
        .then(data => {
          console.log(data);
          // Aquí puedes realizar cualquier otra acción después de guardar la película, como cerrar el modal o actualizar la lista de películas
          this.closeModal();
        })
        .catch(error => {
          console.error('Error al guardar la película:', error);
        });
      }
    }
  };
  </script>
  
  <style>
  /* Estilos del modal */
  .modal {
    display: none;
    position: fixed;
    z-index: 1;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    overflow: auto;
    background-color: rgba(0, 0, 0, 0.5);
  }
  
  .modal-content {
    background-color: #fefefe;
    margin: 15% auto;
    padding: 20px;
    border: 1px solid #888;
    width: 50%;
  }
  
  .close {
    color: #aaa;
    float: right;
    font-size: 28px;
    font-weight: bold;
  }
  
  .close:hover,
  .close:focus {
    color: black;
    text-decoration: none;
    cursor: pointer;
  }
  </style>
  