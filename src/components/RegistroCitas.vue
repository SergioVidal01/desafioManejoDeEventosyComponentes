
<template>
  <form @submit.prevent="handleSubmit">
    <div v-for="field in fields" :key="field.name">
      <label :style="{ color: form[field.name] ? 'black' : 'red' }">
        {{ field.label }}
      </label>
      <template v-if="field.name === 'severity'">
        <select v-model="form[field.name]" name="severity" @change="validateForm">
          <option value="">Selecciona una opción</option>
          <option value="Baja">Baja</option>
          <option value="Media">Media</option>
          <option value="Alta">Alta</option>
        </select>
      </template>
      <template v-else>
        <input 
          v-model="form[field.name]" 
          :name="field.name" 
          :type="field.type" 
          @change="validateForm"
        />
      </template>
    </div>
    <button type="submit" :disabled="!isFormValid">Agregar</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      form: {
        patient: '',
        date: '',
        time: '',
        severity: '',
        reason: ''
      },
      fields: [
        { name: 'patient', label: 'Paciente', type: 'text' },
        { name: 'date', label: 'Fecha', type: 'date' },
        { name: 'time', label: 'Hora', type: 'time' },
        { name: 'severity', label: 'Gravedad', type: 'select' },
        { name: 'reason', label: 'Motivo', type: 'text' }
      ],
      isFormValid: false
    };
  },
  methods: {
    validateForm() {
      this.isFormValid = Object.values(this.form).every(field => field);
    },
    handleSubmit() {
      this.$emit('add-appointment', { ...this.form });
      this.form = {
        patient: '',
        date: '',
        time: '',
        severity: '',
        reason: ''
      };
      this.isFormValid = false;
    }
  }
};
</script>

<style scoped>
form {
  background-color: #fff;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  max-width: 700px;
  margin: 20px auto;
  display: flex;
  gap: 5px;
  
}

form div {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

input {
  width: 100%;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
 
}

button {
  background-color: #5cb85c;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

button:disabled {
  background-color: #d4d4d4;
}
</style>



