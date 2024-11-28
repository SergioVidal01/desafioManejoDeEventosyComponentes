<template>
    <div :style="{ backgroundColor: getBackgroundColor(appointment.severity) }" class="appointment-card">
      <p>Paciente: {{ appointment.patient }}</p>
      <p>Fecha: {{ appointment.date }}</p>
      <p>Hora: {{ appointment.time }}</p>
      <p>Gravedad: {{ appointment.severity }}</p>
      <p>Motivo: {{ appointment.reason }}</p>
      <button @click="$emit('delete-appointment', appointment)">Eliminar</button>
    </div>
  </template>
  
  <script>
  export default {
    props: ['appointment'],
    methods: {
      getBackgroundColor(severity) {
        switch (severity) {
          case 'Alta':
            return 'red';
          case 'Media':
            return 'yellow';
          case 'Baja':
            return 'green';
          default:
            return 'white';
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .appointment-card {
    background-color: white;
    padding: 15px;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    margin: 10px 0;
    display: flex;
    flex-direction: column;
  }
  
  .appointment-card p {
    margin: 5px 0;
  }
  
  .appointment-card button {
    background-color: #d9534f;
    color: white;
    border: none;
    padding: 10px;
    border-radius: 4px;
    cursor: pointer;
    font-size: 16px;
  }
  </style>
  
  