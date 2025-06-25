<!--Componente que se encarga de mostrar las recetas y su respectiva sección de comentarios-->


<!--<Script>-->

<!--En este script primero importamos los Componentes necesarios, tales como RecetaCocina.vue y
ComentariosReceta.vue
Cabe reseñar, que aquí como simplemente importamos los datos, y no se busca reactividad de los 
mismos, no se usa ref -->

<!--Se define Props, que permite a ListadoRecetas(hijo) ejecutarla, y se le indica el
elemento(en este caso, const recetario []) creado en App.vue. Como vemos se usa de padre a hijo, 
de App.vue a ListadoRecetas.vue. También se recibe la función eliminarRecetas -->
<script setup>
import RecetaCocina from "./RecetaCocina.vue"
import ComentariosReceta from "./ComentariosReceta.vue"

defineProps({
  recetario: Array,
  eliminarReceta: Function
})
</script>


<!--<Template>-->

<!--La Clase contenedorPrincipal es donde se guardan las recetas y sección de comentarios-->

<!--La Clase contenedorRecetas contiene varias Clases con la siguiente estructura: 
      {
        recetaContenedor{
              receta{},
              comentarios{}
        }
      }
-->

<!--La Clase recetaContenedor usa un bucle v-for para recorrer el array recetario usando :key="index"
donde se usa v-bind asignando como key el index (elemento reactivo), e ir mostrando el componente 
RecetaCocina y el componente ComentariosReceta, uniendo así ambos en un solo contenedor.-->

<!--La Clase receta muestra el componente RecetaCocina concreto (según índice en el bucle) del array, 
además añade un botón para borrar recetas, que usa @ para asociar el evento a la llamada de la 
función eliminarReceta (por el índice) cuando es pulsado-->

<!--La Clase comentarios usa(muestra) el componente ComentariosReceta-->

<template>
  <div class="contenedorPrincipal">
    <div class="contenedorRecetas">
      <div v-for="(receta, index) in recetario" :key="index" class="recetaContenedor">
        <div class="receta">
          <RecetaCocina :receta="receta" />
          <button @click="eliminarReceta(index)">Borrar</button>
        </div>
        <div class="comentarios">
          <ComentariosReceta />
        </div>
      </div>
    </div>
  </div>
</template>

<!--<Style>-->

<!--Aqui lo más destacable es la estructura definida para mostrar cada receta con su zona 
de comentarios. Sería la siguiente, donde los porcentajes o flex, indican el ancho del contenedor:
              Contenedor Principal 100%{
                    Contenedor Recetas 75%{
                          Receta Contenedor 100%{Receta flex:1.3, Comentarios flex:0.7}
                    }
                    .............
              }
Cuando un contendor tiene display: flex, una forma de indicar el ancho, alternativa a width, para sus elementos
es mediante flex: 1 (ajustar según necesidades, si hay dos elementos en el contenedor, te garantizas que ocupe
1 de los 2 enteros)-->

<!-- El resto son configuraciones típicas: alineación de textos, margenes, paddings, colores, etc...-->
<style scoped>
/* Contenedor principal ocupa todo el ancho */
.contenedorPrincipal {
  width: 100%;
  display: flex;
  justify-content: center;
}

/* Contenedor de todas las recetas */
.contenedorRecetas {
  width: 75%;
  display: flex;
  flex-direction: column;
  background-color: burlywood;
  border-radius: 10%;
}

/* Cada receta + sus comentarios estarán en su propio contenedor */
.recetaContenedor {
  display: flex;
  width: 100%;
  margin: 2%;
  border-top-left-radius: 25%;
  border-top-right-radius: 10%;
  border-bottom-right-radius: 10%;
}

/* Cada receta ocupa la mitad del ancho */
.receta {
  flex: 1.3;
  padding: 15px;
  border: 1px solid wheat;
  background-color: rgba(255, 228, 196, 0.897);
  margin: 2%;
  border-top-left-radius: 20%;
  border-top-right-radius: 10%;
  border-bottom-right-radius: 10%;
  border-bottom-left-radius: 5%;
}

/* Los comentarios ocuparán la otra mitad */
.comentarios {
  flex: 0.7;
  padding: 1rem;
  border: 1px solid #ccc;
  background: #eaeaea;
  margin: 2%;
  border-top-left-radius: 20%;
  border-top-right-radius: 10%;
  border-bottom-right-radius: 10%;
  border-bottom-left-radius: 5%;
}
</style>
