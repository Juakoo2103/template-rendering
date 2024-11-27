<script>
export default {
  data() {
    return {
      showShape: true,
      isHighlighted: false,
      borderRadiusValue: 20, // Valor inicial del slider para border-radius
      shapeStyles: {
        backgroundColor: "#ff0000",
        width: "150px", // Ancho fijo
        height: "150px", // Alto fijo
        borderRadius: "20%", // Valor inicial
        transition: "all 0.3s ease",
      },
      items: [
        { id: 1, name: "Elemento 1" },
        { id: 2, name: "Elemento 2" },
        { id: 3, name: "Elemento 3" },
      ],
    };
  },
  watch: {
    borderRadiusValue(newValue) {
      this.shapeStyles.borderRadius = `${newValue}%`;
    },
  },
  methods: {
    toggleShape() {
      this.showShape = !this.showShape;
    },
  },
};
</script>

<template>
  <div id="app" class="container">
    <!-- Controles (lado izquierdo) -->
    <div class="controls">
      <form>
        <!-- Input para cambiar el color -->
        <label>
          Cambiar color:
          <input v-model="shapeStyles.backgroundColor" type="color" />
        </label>

        <!-- Input para modificar border-radius -->
        <label>
          Cambiar borde redondeado:
          <input v-model="borderRadiusValue" type="range" min="0" max="50" />
        </label>

        <!-- Botón para mostrar u ocultar la figura -->
        <button type="button" @click="toggleShape">
          {{ showShape ? "Ocultar Figura" : "Mostrar Figura" }}
        </button>
      </form>

      <!-- Listado dinámico -->
      <ul>
        <li v-for="item in items" :key="item.id">
          {{ item.name }}
        </li>
      </ul>
    </div>

    <!-- Figura (lado derecho) -->
    <div v-show="showShape" :style="shapeStyles" class="figure">
      Figura dinámica
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
}

.controls {
  flex: 1;
  margin-right: 20px;
}

.controls form {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.figure {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid black;
  text-align: center;
  box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3);
}
</style>
