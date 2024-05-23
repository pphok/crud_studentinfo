<template>
  <div class="student-form">
    <h3>{{ isEdit ? 'Edit Student' : 'Add Student' }}</h3>
    <form @submit.prevent="save">
      <label>Name:</label>
      <input v-model="student.name" required />
      <label>Age:</label>
      <input type="number" v-model="student.age" required />
      <label>Grade:</label>
      <input v-model="student.grade" required />
      <div class="form-buttons">
        <button type="submit">{{ isEdit ? 'Update' : 'Add' }}</button>
        <button type="button" @click="clear">Clear</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  props: ['studentToEdit'],
  data() {
    return {
      student: this.studentToEdit ? { ...this.studentToEdit } : { name: '', age: '', grade: '' },
    };
  },
  computed: {
    isEdit() {
      return !!this.studentToEdit;
    },
  },
  watch: {
    studentToEdit(newVal) {
      this.student = newVal ? { ...newVal } : { name: '', age: '', grade: '' };
    },
  },
  methods: {
    save() {
      this.$emit(this.isEdit ? 'update' : 'add', this.student);
      this.clear();
      this.$emit('close');
    },
    clear() {
      this.student = { name: '', age: '', grade: '' };
    },
  },
};
</script>

<style scoped>
.student-form {
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.student-form h3 {
  margin-bottom: 20px;
}

.student-form label {
  display: block;
  margin-bottom: 5px;
}

.student-form input {
  width: 100%;
  padding: 10px;
  margin-bottom: 15px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.form-buttons {
  display: flex;
  justify-content: space-between;
}

.form-buttons button {
  padding: 10px 15px;
  border: none;
  background-color: #007bff;
  color: white;
  border-radius: 5px;
  cursor: pointer;
}

.form-buttons button:hover {
  background-color: #0056b3;
}

.form-buttons button[type="button"] {
  background-color: #6c757d;
}

.form-buttons button[type="button"]:hover {
  background-color: #5a6268;
}
</style>
