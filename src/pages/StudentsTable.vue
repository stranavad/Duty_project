<script setup>
import {supabase} from '@/supabase';
import {ref, onMounted} from 'vue';

const students = ref([]);

const loadStudents = async () => {
    students.value = (await supabase.from('Students').select()).data;
}

const getStudentName = student => `${student.firstname} ${student.lastname}`;

onMounted(loadStudents);


</script>

<template>
    <div class="students-page">
        <h2>Students</h2>
      <div class="students-table-header">
        <div class="w-name">Name</div>
        <div class="center w-status">Status</div>
        <div class="center w-group">Group</div>
      </div>
        <div class="students-table">
            <div v-for="student in students" :key="student.id" class="student">
                <div class="w-name">{{getStudentName(student)}}</div>
                <div class="w-status"><div  class="student-status" :class="{'active': student.active, 'not-active': !student.active}"/></div>
                <div class="center w-group">{{student.group}}</div>
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
.students-page {
  width: 100vw;
  display: flex;
  flex-direction:column;
  justify-content: center;
  align-items: center;

  h2 {
    width: 400px;
  }
 }

.students-table-header {
  min-width: 400px;
  display: flex;
  flex-direction: row;
}

.center {
  display: flex;
  justify-content: center;
}

.w-name {
  width: 35%;
}

.w-status {
  width: 20%;
}

.w-group {
  width: 20%;
}

.students-table {
  margin-top: 25px;

  .student {
    width: 400px;
    max-width: 99vw;
    background-color: #dddddd;
    display: flex;
    flex-direction: row;
    align-items: center;
    border-radius: 8px;
    padding: 15px;
    margin-bottom: 20px;

    .student-status {
      height: 12px;
      width: 12px;
      border-radius: 50%;
      margin: auto;

      &.active {
        background-color: green;
      }

      &.not-active {
        background-color: #ab0000;
      }
    }

    .student-group {
      margin-left: 25px;
    }
  }
}

</style>
