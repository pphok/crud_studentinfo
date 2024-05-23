<template>
    <div class="student-list">
      <div class="sort-buttons">
        <button @click="sortBy('name')">Sort by Name</button>
        <button @click="sortBy('age')">Sort by Age</button>
        <button @click="sortBy('grade')">Sort by Grade</button>
      </div>
      <ul>
        <li v-for="student in sortedStudents" :key="student.id" class="student-item">
          {{ student.name }} - Age: {{ student.age }} - Grade: {{ student.grade }}
          <div class="action-buttons">
            <button @click="$emit('edit', student)">Edit</button>
            <button @click="$emit('delete', student.id)">Delete</button>
          </div>
        </li>
      </ul>
      <button class="download-button" @click="downloadData">Download Data</button>
    </div>
  </template>
  
  <script>
  export default {
    props: ['students'],
    data() {
      return {
        sortKey: '',
      };
    },
    computed: {
      sortedStudents() {
        return [...this.students].sort((a, b) => {
          if (this.sortKey) {
            if (a[this.sortKey] < b[this.sortKey]) return -1;
            if (a[this.sortKey] > b[this.sortKey]) return 1;
          }
          return 0;
        });
      },
    },
    methods: {
      sortBy(key) {
        this.sortKey = key;
      },
      downloadData() {
        const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(this.students));
        const dlAnchorElem = document.createElement('a');
        dlAnchorElem.setAttribute("href", dataStr);
        dlAnchorElem.setAttribute("download", "students.json");
        dlAnchorElem.click();
      },
    },
  };
  </script>
  
  <style scoped>
  .student-list {
    padding: 20px;
    background-color: #f9f9f9;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  }
  
  .sort-buttons {
    margin-bottom: 20px;
  }
  
  .sort-buttons button {
    margin-right: 10px;
    padding: 10px 15px;
    border: none;
    background-color: #007bff;
    color: white;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .sort-buttons button:hover {
    background-color: #0056b3;
  }
  
  .student-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    margin-bottom: 10px;
    background-color: white;
    border-radius: 5px;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
  }
  
  .action-buttons button {
    margin-left: 10px;
    padding: 5px 10px;
    border: none;
    background-color: #dc3545;
    color: white;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .action-buttons button:hover {
    background-color: #c82333;
  }
  
  .action-buttons button:first-child {
    background-color: #28a745;
  }
  
  .action-buttons button:first-child:hover {
    background-color: #218838;
  }
  
  .download-button {
    margin-top: 20px;
    padding: 10px 15px;
    border: none;
    background-color: #007bff;
    color: white;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .download-button:hover {
    background-color: #0056b3;
  }
  </style>
  