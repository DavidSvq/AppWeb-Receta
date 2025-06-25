<!--Componente que contiene la estructura básica necesaria para almacenar los datos de una 
receta en la web-->
<!--<Script>-->
<!--Este componente no necesita importar nada.-->
<!--Se define Props, que es la propiedad que nos permite entrelazar datos, y se le indica el
elemento(en este caso, receta: Object) creado en App.vue.-->
<!--Se crea la función esUrlValida para validar el url, donde intenta, a modo de prueba, 
conectar con la url en concreto y si lo consigue devuelve true. Además recogida como excepción, 
try-catch,en caso de que falle y entonces devuelve false.-->
<script setup>
defineProps({
  receta: Object,
});

const esUrlValida = (url) => {
  try{
    new URL(url);
    return true;
  }
  catch {
    return false;
  }
};
</script>

<!--<Template>-->
<!--La Clase receta contiene los siguientes atributos o campos:
  Nombre: Nombre de la receta.
  Descripción: Breve información sobre la receta(no como se hace la receta en sí).
  Tiempo: Minutos que se emplean en elaborar la receta.
  Dificultad: Indica el nivel de dificultad de la receta.
  Enlace: Contiene la dirección web, de una página externa que contiene los pasos para la
  elaboración de la receta. Para este atributo, además añadí un v-if sobre la función creada
  para comprobar si la url es válida. De no serlo, v-else muestra un mensaje alternativo al 
  enlace.-->
<template>
  <div class="receta">
    <h3>{{ receta.nombre }}</h3>
    <p><strong>Descripcion</strong> {{ receta.descripcion }}</p>
    <p><strong>Tiempo</strong> {{ receta.tiempo }} minutos</p>
    <p><strong>Dificultad</strong> {{ receta.dificultad }}</p>
    <a v-if="esUrlValida(receta.enlace)" :href="receta.enlace" target="_blank" class="boton-enlace">Ver receta completa</a>
    <p v-else class="errorEnlace">Enlace No Válido</p>
  </div>
</template>

<!--<Style>-->
<!--Este Componente no tiene nada reseñable en su estilo, más alla del uso de
medidas relativas como % o rem. O el uso de padding-left y padding rigth asi:
padding: "valor para la izquierda" "valor para la derecha;", el resto son las 
configuraciones típicas: alineación de textos, margenes, paddings, colores, etc...-->
<style scoped>
.receta {
  width: 100%;
  min-width: 15rem;
}
h3 {
  background-color: azure;
  width: 90%;
  max-width: 35rem;
}
p {
  background-color: azure;
  padding: 1%;
  padding-left: 5%;
  width: 80%;
  max-width: 35rem;
  border-radius: 15%;
}
.boton-enlace {
  display: inline-block;
  margin-top: .8rem;
  padding: .5rem .8rem;
  background-color: azure;
  color: black;
  text-decoration: none;
  border-radius: 50%;
}
</style>
