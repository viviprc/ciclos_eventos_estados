<template>
  <div id="contenedor">
    <h1>Random Gift Cat</h1>
    <div id="parametros">
      <table>
        <tr>
          <td>
            <label for="titulo">Título:</label>
          </td>
          <td>
            <input v-model="titulo" type="text" placeholder="Escribe tu mensaje" />
          </td>
        </tr>
        <tr>
          <td>
            <label for="filtro">Filtro:</label>
          </td>
          <td>
            <select v-model="selectedFilter" @change="seleccionFiltro">
              <option disabled value="">Selecciona un filtro</option>
              <option :value="filtro.value" v-for="(filtro, i) in filtros" :key="i">
                <p>{{filtro.label}}</p>
              </option>
            </select>
          </td>
        </tr>
        <tr>
          <td>
            <label for="color">Color:</label>
          </td>
          <td>
            <select v-model="selectedColor" @change="seleccionColor">
              <option disabled value="">Selecciona un color</option>
              <option :value="color.value" v-for="(color, i) in colores" :key="i">
                <p>{{color.label}}</p>
              </option>
            </select>
          </td>
          <td>
            <div class="circulo" :style="{backgroundColor: this.color}"></div>
          </td>
        </tr>
        <tr>
          <td>
            <label for="tamano">Tamaño:</label>
          </td>
          <td>
            <input v-model="tamano" type="number" min="30" max="100" />
          </td>
        </tr>
      </table>
    </div>
    <div id="img-contenedor">
      <button :disabled="!completeUrlData" id="boton" @click="buscarGatito">MY GIFT CAT</button>
      <div v-if="imagenVisible" id="contenedor-imagen">
        <img :src="src" width="100%" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      titulo: "",
      filtro: "",
      selectedFilter: "",
      filtros: [
        { label: "Sin filtro", value: "none" },
        { label: "Borroso", value: "blur" },
        { label: "Monocromático", value: "mono" },
        { label: "Sepia", value: "sepia" },
        { label: "Negativo", value: "negative" },
        { label: "Pintura", value: "paint" },
        { label: "Pixelado", value: "pixel" },
      ],
      color: "",
      selectedColor: "",
      colores: [
        { label: "Rojo", value: "red" },
        { label: "Amarillo", value: "yellow" },
        { label: "Verde", value: "green" },
        { label: "Naranjo", value: "orange" },
        { label: "Azul", value: "blue" },
        { label: "Blanco", value: "white" },
        { label: "Negro", value: "black" },
      ],
      tamano: "",
      src: "",
      imagenVisible: false,
    };
  },
  methods: {
    buscarGatito() {
      this.src = this.url;
      this.imagenVisible = true;
      this.titulo ='';
      this.selectedFilter ='';
      this.selectedColor ='';
      this.tamano='';
    },
  },
  computed: {
    seleccionColor(){
      return this.color = this.selectedColor
    },
    seleccionFiltro(){
      return this.filtro = this.selectedFilter
    },
    url() {
      return `https://cataas.com/cat/gif/says/${this.titulo}?filter=${this.filtro}&color=${this.color}&size=${this.tamano}&type=or`;
    },
    completeUrlData() {
      return this.titulo && this.filtro && this.color && this.tamano;
    },
  },
};
</script>


<style>
body {
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  color: #ffc300;
  background-color: #581845;
  display: flex;
  justify-content: center;
}
#contenedor {
  width: 400px;
  height: 550px;
  display: flex;
  justify-content: flex-start;
  flex-direction: column;
  align-items: center;
  background-color: #900c3f;
  border: 1px solid #384c5e;
  border-radius: 15px;
  text-align: center;
}
#parametros {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  width: 100%;
  background-color: #ff5733;
  height: 150px;
}
table {
  border-collapse: collapse;
  width: 60%;
}
td {
  padding: 8px;
  text-align: right;
}
td:nth-child(even) {
  text-align: left;
}
select {
  border-radius: 3px;
  width: 100%;
}
input {
  border-radius: 3px;
  border-width: 1px;
  border-style: solid;
  border-color: -internal-light-dark(rgb(118, 118, 118), rgb(195, 195, 195));
}
.circulo {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background-color: #ff5733;
}
#boton {
  width: 120px;
  margin: 15px;
  border-radius: 3px;
  background-color: #900c3f;
  color: #ffc300;
  padding: 5px;
  border-width: 1px;
  border-style: solid;
  border-color: -internal-light-dark(rgb(118, 118, 118), rgb(195, 195, 195));
}
#boton:hover {
  background-color: #ff5733;
}
#contenedor-imagen {
  width: 300px;
  height: 250px;
  display: flex;
  justify-content: center;
}
#img-contenedor {
  background-color: #c70039;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>