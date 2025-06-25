<!--Este Componente, es el Componente Principal(Padre) llamado App -->


<!--Script-->

<!-- En el Script primero realizamos la importación usando {ref} (siempre se debe usar .value, 
{reactive} para estructuras más complejas sin value) desde vue. Lo cual permite que los
datos cambien reactivamente.-->

<!--Después importamos los Componentes necesarios, usados por App, tales como: TituloRecetas.vue,
FormularioReceta.vue y ListadoRecetas.vue-->

<!--A continuación se crea recetario [], con 2 recetas ya insertas de muestras.-->

<!--Se crea la función agregarReceta para añadir las nuevas recetas a recetario[] según
se vaya rellenando el formulario. 
NOTA IMPORTANTE: Aquí, no se reciben directamente los datos ingresados por el navegador, aquí
se reciben desde el Componente (hijo) FormularioReceta los datos que si son recogidos allí, y 
esos datos se vuelcan sobre una variable reactiva que está en ambos Componentes(creada en el 
Componente hijo), por lo que se actualizan automáticamente con cualquier cambio. -->

<!--Se crea la función eliminarReceta, definido su props en el Componente ListadoRecetas.vue 
(donde es llamada), para eliminar una receta de recetario en base a su índice con 
recetario.value.splice(index, 1) donde .splice indica borrar(index, "nº de elementos a borrar");. 
Además, se añade la función confirm() dentro de un if, para lanzar una ventanita de confirmación 
de que se quiere eliminar. -->
<script setup>
import { ref } from "vue"
import TituloRecetas from "./components/TituloRecetas.vue"
import FormularioReceta from "./components/FormularioReceta.vue"
import ListadoRecetas from "./components/ListadoRecetas.vue"

// Array global para almacenar recetas, inlcuye 2 recetas ya cargadas.
const recetario = ref([
  {
    nombre: "Tortilla de Patatas",
    descripcion: "Plato típico español",
    tiempo: 30,
    dificultad: "Media",
    enlace:
      "https://recetasdecocina.elmundo.es/2024/09/tortilla-de-patatas-con-cebolla-receta-facil.html",
  },
  {
    nombre: "Lamingtons",
    descripcion: "Dulce típico australiano",
    tiempo: 60,
    dificultad: "Dificil",
    enlace: "https://www.bonviveur.es/recetas/lamingtons",
  },
])

// Función para agregar recetas al array
const agregarReceta = (nuevaReceta) => {
  recetario.value.push(nuevaReceta)
}

// Función para eliminar recetas del array
const eliminarReceta = (index) => {
   if (confirm('¿Seguro que quieres borrar esta receta?')) {
    recetario.value.splice(index, 1);
  }
}
</script>


<!--Template-->

<!--La clase App es donde se agrupan y usan el resto de Componentes y sus funciones 
para mostrar en el archivo index.html cuando se carga en el main.js.
Contiene el Componente TituloRecetas para el <header> de index.html. Después va el <main>
que contiene los componentes: 
  FormularioReceta que usa @ para enlazar ambas funciones @agregar-receta="agregarReceta" 
donde agregar-receta hace referencia a FormularioReceta y agregarReceta hace referencia a App.
  ListadoRecetas que usa 2 : para establecer en enlaces dinámicos para el array global tal que
así: :recetario="recetario" :eliminarReceta="eliminarReceta" y la función eliminarReceta 
respectivamente (ambas lanzadas con props en sus componentes).-->
<template>
  <div class="App">
    <TituloRecetas />
    <main>
      <FormularioReceta @agregar-receta="agregarReceta" />
      <ListadoRecetas :recetario="recetario" :eliminarReceta="eliminarReceta"/>
    </main>
  </div>
</template>


<!--<style>-->

<!-- Establezco el tamaño de la fuente de texto para toda la App. Es decir, los rem tomaran este
tamaño como referencia, queda establecido en 16px, además uso de clamp, como ya explique en otro 
comentario, para establecer mínimo y máximo de una unidad por aquello de los tamaños.-->

<!--Elección del tipo de letra(y la de repuesto) poppins (sans-serif) y alto de línea de 1.6-->

<!--Se añada una imagen de fondo, asegurando que cubra todo el elemento con background-size: cover;
y este centrado con background-position: center;-->
<style scoped>
.App {
  width: 100%;
  height: 100%;
  font-size: clamp(12px, 16px, 22px);
  line-height: 1.6;
  font-family: "Poppins", sans-serif;
  font-weight: 600;
  background-image: url("/src/assets/FondoComida2.jpg");
  background-size: cover;
  background-position: center;
}
</style>
