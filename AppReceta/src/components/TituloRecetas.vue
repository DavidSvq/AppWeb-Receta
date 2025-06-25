<!--Este Componente se encarga de mostrar el <header> en App.vue-->


<!--<Script>-->

<!--En este script primero importamos los Componentes necesarios, tales como IconCubiertos.vue,
IconEspatulas.vue, IconFogones.vue e IconGorro (todos ellos son simples imágenes.) -->
<script setup>
import IconCubiertos from './icons/IconCubiertos.vue';
import IconEspatulas from './icons/IconEspatulas.vue';
import IconFogones from './icons/IconFogones.vue';
import IconGorro from './icons/IconGorro.vue';
</script>


<!--<Template>-->

<!--Esta formado por 1 <div id=""> para el texto del título y una Clase para contener los
iconos, en 3 contenedores-->

<!--La Clase contenedorIcon, simplemente contiene los Componentes(iconos) que proporcionan un pequeño
toque visual.-->

<!--El id="titulo" contiene 2 Clases, una para la parte derecha y otra para la parte izquierda (cuando
vea el <style> se entenderá mejor el por qué) en las que se divide el título.-->
<template>
  <div>
    <div class="contenedorIcon">
      <IconEspatulas />
      <IconCubiertos />
    </div>

    <div id="titulo">
      <p class="dcha">Mis Recetas</p>
      <p class="izq">Preferidas</p>
    </div>

    <div class="contenedorIcon">
      <IconGorro />
      <IconFogones />
    </div>
    
    
  </div>
</template>


<!--<Style>-->

<!--Aquí cabe reseñar la partición del texto de título en 2, para mostrar un inicio
dinamico cuando se conecta al navegador, donde una parte aparece de izquierda a derecha
acabando en el centro y la otra al reves, de derechas a izquierda también acabando en el
centro. Para ello se vale de los @keyframe y animation.-->

<!-- El resto son configuraciones típicas: alineación de textos, margenes, paddings, colores, etc...-->
<style scoped>
div {
  background-color: burlywood;
  text-align: center;
  align-items: center;
  width: 100%;
  height: 20%;
  max-height: 25rem;
  display: flex;
}

.contenedorIcon{
  display: flex;
  justify-content: space-around;
  width: 40%;
}
#titulo{
  text-align: center;
  width: 100%;
}

.dcha {
  color: aliceblue;
  text-shadow: 2px 2px 2px red;
  display: block;
  font-size: 3vw;
  font-weight: 900;
  font-family: monospace;
  white-space: nowrap;
  animation: letreado 2s steps(11);
  overflow: hidden;
  width: 100%;
  margin: 1%;
  text-align: right;
  padding-right: 1.5%;
}
.izq {
  color: red;
  text-shadow: 2px 2px 2px aliceblue;
  direction: rtl;
  display: inline-block;
  font-size: 3vw;
  font-family: monospace;
  white-space: nowrap;
  width: 11ch;
  animation: letreadoI 2s steps(11);
  overflow: hidden;
  width: 100%;
  text-align: left;
  margin: 1%;
  padding-left: 1.5%;
}

@keyframes letreado {
  from {
    transform: translateX(-100%);
  }
  to {
    transform: translateX(0);
  }
}

@keyframes letreadoI {
  from {
    transform: translateX(100%);
  }
  to {
    transform: translateX(0);
  }
}
</style>
