<template>
  <div>
    <h1>Інформація про студента</h1>
    <p>ID студента: {{ id }}</p>
    <div v-if="student">
      <img :src="student.photo" alt="Фото студента" />
      <p>ПІБ: {{ student.name }}</p>
      <p>Група: {{ student.group }}</p>
      <p>Рік народження: {{ student.mark }}</p>
      <p>Практика: {{ student.isDonePr ? "Здав" : "Не здав" }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  props: {
    id: String, 
  },
  data() {
    return {
      student: null, 
    };
  },
  mounted() {
    this.fetchStudentInfo();
  },
  methods: {
    fetchStudentInfo() {
     
      axios
        .get(`http://34.82.81.113:3000/students/${this.id}`)
        .then((response) => {
          this.student = response.data;
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>

<style scoped>

</style>

