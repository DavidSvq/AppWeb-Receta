<!-- Componente que se encarga de solicitar los datos de la receta con un formulario interactivo y 
los envía al array global(recetario) En App.vue-->

<!--<Script>-->

<!-- En el Script primero realizamos la importación usando {ref} (siempre se debe usar .value, 
 {reactive} para estructuras más complejas sin value) desde vue. -->

<!--Se define Props, que es la propiedad que nos permite entrelazar datos, y se le indica el
elemento(en este caso, const recetario []) creado en App.vue. Como vemos se usa de padre a hijo, 
de App.vue a FormularioReceta.vue. -->

<!--Se vuelve a usar ref() para crear las nuevas recetas con const nuevaReceta = ref, incluyendo 
todos los campos vacíos para definir una receta en RecetaCocina. Es decir, con esto nuevaReceta puede 
ser usada App.vue logrando que los datos se actualicen automáticamente ante cualquier cambio en ellos-->

<!-- Se define emit, dispara eventos para que el padre los escuche, para llamar a la función 
agregarReceta y mantener a la escucha a App.vue y ejecutar el evento. Su sintaxis, se crea una 
variable para ello const emit = defineEmits(["agregar-receta"]) donde agregar-receta es el nombre 
indicado en la función cuando se use emit. -->

<!-- Se crea la función agregarReceta, valiendose de un condicional if para confirmar que no sea 
un nombre vacio. Usamos .value, se usa siempre con {ref} para obtener el valor y .trim para 
eliminar espacios si lo hubiera en cada extremo de la variable.
Si se entra en el if, se usa el emit asociando la receta devuelta al nombre asignado en el emit.
Después limpiamos el valor de nuevaReceta, preparándolo así para próxima inserción
NOTA IMPORTANTE: La función agregarReceta aquí solo envía los datos a App.vue de la receta en 
cuestión, no puede alterar el array global que esta en App, es decir, App.vue debe implementar 
su método agregarReceta para poder manipular el array global "recetario"-->

<script setup>
import { ref } from "vue"

defineProps({
  recetario: Array,
})

const nuevaReceta = ref({
  nombre: "",
  descripcion: "",
  tiempo: "",
  dificultad: "Fácil",
  enlace: "",
})

const emit = defineEmits(["agregar-receta"])

const agregarReceta = () => {
  if (nuevaReceta.value.nombre.trim() !== "") {
    emit("agregar-receta", { ...nuevaReceta.value })
    nuevaReceta.value = { nombre: "", descripcion: "", tiempo: "", dificultad: "Fácil", enlace: "" }
  }
}
</script>

<!--<Template>-->

<!-- La Clase formulario se encargar de solicitar los datos de un Componente RecetaCocina, que son: 
nombre de la receta, breve descripción de la receta, tiempo de elaboración, nivel de dificultad y un
enlace hacia la página web externa que contiene la receta. Para ello, primero hace uso de @ (v-on) 
submit.prevent="agregarReceta" en <form> para evitar la recarga de la página y ejecutar la función 
"agregarReceta" al enviar el formulario.
Después se usa v-model para crear interactividad y reactividad entre los valores introducidos por el navegador para cada variable 
necesaria para el componente RecetaCocina. Se incluye <select> para elegir la dificultad de la receta. Por último, se coloca el 
<button> para el sumbit que espera el comando @ -->

<template>
  <div class="formulario">
    <h3>Añadir una nueva receta</h3>
    <form @submit.prevent="agregarReceta" id="formAgregarReceta">
      <input v-model="nuevaReceta.nombre" placeholder="Nombre de la receta" />
      <input v-model="nuevaReceta.descripcion" placeholder="Descripción" />
      <input type="number" v-model="nuevaReceta.tiempo" placeholder="Tiempo en minutos" />
      <label class="dificultad"
        >Nivel de la receta
        <select v-model="nuevaReceta.dificultad" placeholder="Nivel de Dificultad">
          <option value="Fácil">Fácil</option>
          <option value="Media">Media</option>
          <option value="Difícil">Difícil</option>
        </select>
      </label>
      <input v-model="nuevaReceta.enlace" placeholder="URL de la receta" />
      <button type="submit" id="botonAnadir">Añadir receta</button>
    </form>
  </div>
</template>

<!--<Style>-->

<!-- Caracteristicas del estilo destacables:
  Uso del comando clamp, con el que se puede establecer un tamaño, precedido por el mínimo y seguido
  por el máximo que pueden alcanzar. (Con el objetivo, de enfrentarse a diferentes tamaños del navegador
  o de diferentes tamaños de la pantalla.)-->

<!-- El resto son configuraciones típicas: alineación de textos, margenes, paddings, colores, etc...-->

<!--Estan organizadas según el orden de aparición en el HTML-->
<style scoped>
.formulario {
  margin-bottom: 1rem;
  text-align: center;
  font-size: clamp(1.3rem, 2.5vw, 2rem);
  margin: 2%;
  border: 3rem double wheat;
  width: 60%;
  min-width: 45rem;
  margin-left: auto;
  margin-right: auto;
}

h3 {
  margin-top: clamp(2.5rem, 1vw, 3rem);
  color: crimson;
  text-shadow: 0.2rem 0.2rem 0.4rem white;
}

#formAgregarReceta {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 1%;
}

input {
  width: 100%;
  max-width: 30rem;
  height: 2rem;
  max-height: 3rem;
  margin: 0.5%;
  border-radius: 5%;
  font-size: clamp(1rem, 2vw, 1.5rem);
}

.dificultad {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  width: 70%;
  height: 2rem;
  max-height: 3rem;
  margin: 1%;
}

label {
  font-size: 1rem;
  width: 30%;
  height: 2rem;
  max-height: 3rem;
  margin: 1%;
}
select {
  width: 80%;
  max-width: 20rem;
  height: 2rem;
  max-height: 3rem;
  margin: 1%;
  font-size: 0.9rem;
}

#botonAnadir {
  width: 30%;
  max-width: 15rem;
  height: 2rem;
  max-height: 2rem;
  margin: 1%;
  border-radius: 50%;
}
</style>
