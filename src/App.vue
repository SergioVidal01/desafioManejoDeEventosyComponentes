<template>
  <div>
    <h1>Administrador de Citas Médicas</h1>
    <RegistroCitas @add-appointment="addAppointment" />
    <div v-if="appointments.length === 0">
      <p style="color: red;">Aún no hay consultas registradas.</p>
    </div>
    <div v-else>
      <TarjetaCita
        v-for="(appointment, index) in appointments"
        :key="index"
        :appointment="appointment"
        @delete-appointment="deleteAppointment"
      />
    </div>
  </div>
</template>

<script>
import RegistroCitas from './components/RegistroCitas.vue';
import TarjetaCita from './components/TarjetaCita.vue';

export default {
  components: {
    RegistroCitas,
    TarjetaCita
  },
  data() {
    return {
      appointments: []
    };
  },
  methods: {
    addAppointment(appointment) {
      this.appointments.push(appointment);
    },
    deleteAppointment(appointmentToDelete) {
      this.appointments = this.appointments.filter(
        appointment => appointment !== appointmentToDelete
      );
    }
  }
};
</script>

<style scoped>
body { font-family: Arial, sans-serif; 
background-color: #f0f0f0; 
margin: 0; 
padding: 20px; 
} 
h1 { 
  text-align: center; 
  color: #333; 
  } 
.container { 
    display: flex; 
    flex-direction: 
    column; 
    align-items: center; 
    } 
.content { 
    display: flex; 
    justify-content: space-between; 
    width: 100%; 
    max-width: 1200px; }
.appointments { 
    flex: 1; 
    margin-left: 20px; 
} 
p { 
    margin: 0; 
}
</style>

