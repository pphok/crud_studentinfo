<template>
    <div class="student-crud">
      <student-form @add="addStudent"></student-form>
      <student-list
        :students="students"
        @edit="openEditModal"
        @delete="deleteStudent"
      ></student-list>
      <base-modal :isOpen="isEditModalOpen" @close="closeEditModal">
        <student-form
          :student-to-edit="studentToEdit"
          @update="updateStudent"
          @close="closeEditModal"
        ></student-form>
      </base-modal>
    </div>
  </template>
  
  <script>
  import StudentList from './StudentList.vue';
  import StudentForm from './StudentForm.vue';
  import BaseModal from './BaseModal.vue';
  
  export default {
    components: {
      StudentList,
      StudentForm,
      BaseModal,
    },
    data() {
      return {
        students: this.getStudents(),
        studentToEdit: null,
        isEditModalOpen: false,
      };
    },
    methods: {
      getStudents() {
        const students = localStorage.getItem('students');
        return students ? JSON.parse(students) : [];
      },
      saveStudents(students) {
        localStorage.setItem('students', JSON.stringify(students));
      },
      addStudent(student) {
        student.id = Date.now();
        this.students.push(student);
        this.saveStudents(this.students);
      },
      openEditModal(student) {
        this.studentToEdit = student;
        this.isEditModalOpen = true;
      },
      closeEditModal() {
        this.isEditModalOpen = false;
        this.studentToEdit = null;
      },
      updateStudent(updatedStudent) {
        const index = this.students.findIndex(student => student.id === updatedStudent.id);
        this.students.splice(index, 1, updatedStudent);
        this.saveStudents(this.students);
        this.closeEditModal();
      },
      deleteStudent(id) {
        this.students = this.students.filter(student => student.id !== id);
        this.saveStudents(this.students);
      },
    },
  };
  </script>
  
  <style scoped>
  .student-crud {
    display: flex;
    flex-direction: column;
    gap: 20px;
    padding: 20px;
  }
  </style>
  