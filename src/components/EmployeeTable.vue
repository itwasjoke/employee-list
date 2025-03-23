<template>
  <table>
    <thead>
    <tr>
      <th>Имя</th>
      <th>Зарплата</th>
    </tr>
    </thead>
    <tbody>
    <tr v-for="(employee, index) in employees" :key="index">
      <td>{{ employee.name }}</td>
      <td>{{ employee.salary }} ₽</td>
    </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: {
    employees: {
      type: Array,
      required: true
    }
  }
};
</script>