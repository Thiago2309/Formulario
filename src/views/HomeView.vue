<script setup lang="ts">
import { ref } from 'vue'
import { Ref } from 'vue'

const name: Ref<string> = ref('');
const lastName: Ref<string> = ref('');
const age: Ref<number> = ref();
const gender: Ref<string> = ref('');
  const otro: Ref<string> = ref();
const errors: Ref<string[]> = ref([]);

const Value = () => {
  errors.value = [];
// Con el requiere es otra opcion
  if (!name.value) {
    errors.value.push('Nombre es obligatorio');
  } else if (name.value.length < 5 || name.value.length > 18) {
    errors.value.push('El nombre debe tener entre 5 y 18 caracteres');
  }

  // No debe de ser igual al nombre y obligatorio
  if (!lastName.value) {
  errors.value.push('Apellido es obligatorio');
  } else if (lastName.value === name.value) {
    errors.value.push('El apellido no puede ser igual al nombre');
  }

  // Tine que ser obligatorio
  if (!age.value) {
    errors.value.push('La edad es obligatoria');
  }

  // Mayor a 0
  if (age.value <= 0) {
    errors.value.push('La edad debe ser mayor a 0');
  }

  // Edad tiene que ser mayor 2 menor que 60
  if (age.value <= 1 || age.value >= 60) {
    errors.value.push('La edad debe estar entre 2 y 59');
  }

  if (!gender.value) {
  errors.value.push('El Género es obligatorio');
  } else if (gender.value === 'otro' && !otro.value) {
    errors.value.push('Especifique el génere');
  }

  // Si todo sale bien el formulario sera enviado
  if (errors.value.length === 0) {
    // Todas las validaciones pasaron, el formulario es válido
    return 'Formulario enviado';
  }else {
    // Si hay errores, puedes mostrarlos o hacer algo más
    return 'Por favor, corrija los errores antes de enviar el formulario';
  }
}

const submitForm = () => {
  // Limpiar errores antes de realizar una nueva validación
  errors.value = [];

    // Ejecutar la función Value y mostrar el resultado como alerta
  const result = Value();
  alert(result);
}

</script>

<template>
  <main>
    <h1>FORMULARIO</h1>
    <form @submit.prevent= "Value">
      <div>
        <label for="name">Nombre:</label>
        <input v-model="name" type="text" id="name">
      </div>
      <div>
        <label for="lastName">Apellido:</label>
        <input v-model="lastName" type="text" id="lastName">
      </div>
      <div>
        <label for="age">Edad:</label>
        <input v-model="age" type="number" id="age">
      </div>
      <div>
        <label for="gender gender1">Género:</label>
        <select v-model="gender" id="gender">
          <!-- <option value="seleccionar">Seleccione el Genero</option> -->
          <option value="masculino">Masculino</option>
          <option value="femenino">Femenino</option>
          <option value="otro">Otre</option>
        </select>
        <!-- Input adicional solo si se selecciona "Otro" -->
        <div v-if="gender === 'otro'">
          <label for="otro">Exprese su Genero:</label>
          <input v-model="otro" type="text" id="otro">
        </div>
      </div>

      <div>
        <input type="checkbox">
        <label for="termsAccepted">Acepto los términos  y condiciones.</label>
      </div>

      <button @click="submitForm" type="submit">Enviar</button>
    </form>

    <br>
    <h3>Validacion:</h3>
    <ul v-if="errors.length">
      <li v-for="error in errors" :key="error">{{ error }}</li>
    </ul>
  </main>
</template>

<style scoped>
/* Estilos generales */
main {
  background-color: #e1e1e1;
  padding: 20px;
  border-radius: 10px;
  max-width: 700px;
  margin: auto;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h3{
  color: black;
}

h1{
  color: black;
  text-align: center;
}

/* Estilos para los campos de formulario */
form div {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
  color: black;
}

/* Estilos para botón de enviar */
button {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 10px;
  cursor: pointer;
  border-radius: 5px;
  width: 100%;
}

button:hover {
  background-color: #45a049;
}

/* Estilos para mensajes de validación */
h3 {
  text-align: center;
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

li {
  color: rgb(0, 0, 0);
  /* background-color: red; */
  border: 1px solid rgb(0, 0, 0);
  border-radius: 5px;
  padding: 10px;
  margin-bottom: 5px;
}

/* Estilos para los campos de entrada */
input,
select {
  width: 100%;
  padding: 8px;
  box-sizing: border-box;
  margin-top: 5px;
}

/* Estilos para el input adicional cuando se selecciona "Otro" */
#otro {
  margin-top: 5px;
}
</style>

