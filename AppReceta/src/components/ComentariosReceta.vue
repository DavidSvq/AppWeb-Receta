<!--Componente que se encarga de agregar y mostrar comentarios de la receta-->


<!--<Script>-->

<!-- En el Script primero realizamos la importación usando {ref} (siempre se debe usar .value, 
 {reactive} para estructuras más complejas sin value) desde vue. -->

<!-- Se crea un array (comentarios) declarado con [], y una variable reactiva (nuevoComentario) 
 inicializada como un string vacío (""), para almacenar y recibir comentarios respectivamente.--> 
 
<!-- Se crea la función necesaria para agregar un nuevo comentario, valiendose de un condicional 
 if para confirmar que no sea un comentario vacio. Usamos .value, se usa siempre con {ref} para 
 obtener el valor y .trim para eliminar espacios si lo hubiera en cada extremo de la variable. 
 Después limpiamos el valor de nuevoComentario, preparandolo así para próxima inserción -->
<script setup>
import { ref } from "vue"

const comentarios = ref([])

const nuevoComentario = ref("")

const agregarComentarios = () => {
  if (nuevoComentario.value.trim() !== "") {
    comentarios.value.push(nuevoComentario.value.trim()), (nuevoComentario.value = "")
  }
}
</script>


<!--<Template>-->

<!--Su HTML contiene una lista dinamica(Array), y se vale de un bucle v-for para ir generando 
 comentarios a la receta. Un <input> que usa v-model para crear interactividad entre el <input> y la variable.
 Y por último, un botón para agregar el comentario, hace uso de @ para asignar la escucha del boton y 
 llamar a la función agregarComentarios definida en el <script> --> 
<template>
  <div class="comentarios">
    <h3>Comentarios</h3>
    <ul>
      <li v-for="(comentario, index) in comentarios" :key="index">
        {{ comentario }}
      </li>
    </ul>

    <input v-model="nuevoComentario" placeholder="Escribe un comentario..." />
    <button @click="agregarComentarios">Añadir comentarios</button>
  </div>
</template>


<!--<Style>-->

<!-- Caracteristicas del estilo destacables: 

Se aplica background-color: Azure a <li> como <h3> y se añade al <input> margin-right: 1 rem;
para separar visualmente el campo del botón-->

<!-- La Clase comentario, aparte de recibir un color para el fondo, cabe reseñar el uso
de ancho y alto máximo e incorporar un scroll con overflow: auto; (Evitando así que muchos 
comentarios en una receta pueda desconfigurarse el HTML) -->
<style scoped>
li {
  background-color: azure;
}
h3 {
  background-color: azure;
}
.comentarios {
  width: 100%;
  max-height: 17rem;
  max-width: 25rem;
  overflow: auto;
  margin-top: 1.1rem;
  background-color: rgba(210, 105, 30, 0.671);
}
input {
  margin-right: 1rem;
}
</style>
