<template>
<h2>Cena {{ contador + 1 }}
  con el rey godo {{ productos [contador].nombre }}
</h2>
<h3 class="precio">Precio:  {{ productos[contador].precio  }}€</h3>
<div v-if="productos[contador].finDeSemana" class="soloFinesDeSemana dias">(solo Fines De Semana)</div>
<div v-else class=" dias todosLosDias">(De lunes a domingo )</div>
<div v-if="productos[contador].precio<100" class="oferta">
<div>Ahora un 10% dto:
  {{ nuevoPrecio }}€</div>
  <img src="/oferta.png" alt="rey godo en descuento">
  </div>  
<img :src="imagen" alt=""/>
<button @:click="siguiente">siguiente ({{contador + 1}}/ {{total}})</button>
</template> 

<script setup>
import {ref, computed} from "vue"
import { productos } from './datos';
const contador = ref(0)
const total = productos.length;
const ruta="https://www.html6.es/img/rey_";
const siguiente = () =>{
  contador.value++
  if (contador.value>=total){
    contador.value=0;
  }
}
const rey=computed(() => {
  const elNombre=productos[contador.value].nombre.toLowerCase()
  return elNombre.substring(0,1).toUpperCase() + elNombre.substring(1)
});
const imagen=computed(()=>{
  return  `${ruta}${productos[contador.value].nombre.toLocaleLowerCase()}.png`


})
const nuevoPrecio=computed(()=>{
  return Number (productos [contador.value].precio/1.10 ).toFixed(2)

})
</script>

<style scoped>
.todosLosDias{
  background-color: green;
}
.soloFinesDeSemana{
  background-color: red; }

.dias{
  color:white;
  padding:4px 17px;
  border-radius: 4px;
  margin:5px 0 10px;
  display:inline-block
}
</style>