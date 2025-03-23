<template>
  <div class="app">
    <h1>
      Сотрудники
    </h1>
    <button type="button" :class="['btn', 'btn-primary']" @click="toggleView">Сменить представление</button>
    <button type="button" :class="['btn','btn-right', themeBtn]" @click="toggleTheme">Сменить тему</button>
    <h2>Список</h2>
    <EmployeeTable :employees="flattenedEmployees" v-if="!isNestedView" />
    <EmployeeList :items="employees" v-else />

    <div class="total-salary">Общая сумма зарплат: {{ totalSalary }}</div>
  </div>
</template>

<script>
import EmployeeList from './components/EmployeeList.vue';
import EmployeeTable from './components/EmployeeTable.vue';

export default {
  components: {
    EmployeeList,
    EmployeeTable
  },
  data() {
    return {
      employees: [
        { type: 'user', name: 'Григоропулос Афинский', salary: 1300 },
        { type: 'user', name: 'Афина Совинская', salary: 1300 },
        {
          type: 'group',
          name: 'Отдел тестирования',
          childs: [
            { type: 'user', name: 'Иннокентий', salary: 200 },
            { type: 'user', name: 'Болик', salary: 300 },
            {
              type: 'group',
              name: 'Группа веселых ребят',
              childs: [
                { type: 'user', name: 'Клоунесса', salary: 600 },
                { type: 'user', name: 'Дрессировщица пользователей', salary: 900 },
              ],
            },
          ],
        },
      ],
      isNestedView: true,
      themeLight: true,
      themeBtn: 'btn-dark'
    };
  },
  computed: {
    flattenedEmployees() {
      const flatten = (items) => {
        return items.reduce((acc, item) => {
          if (item.type === 'user') {
            acc.push(item);
          } else if (item.type === 'group' && item.childs) {
            acc = acc.concat(flatten(item.childs));
          }
          return acc;
        }, []);
      };
      return flatten(this.employees);
    },
    totalSalary() {
      return this.flattenedEmployees.reduce((sum, employee) => sum + employee.salary, 0);
    }
  },
  methods: {
    toggleView() {
      this.isNestedView = !this.isNestedView;
    },
    toggleTheme() {
      this.themeLight = !this.themeLight
      if (this.themeLight){
        this.themeBtn = 'btn-dark'
        document.body.classList.add('theme-light');
        document.body.classList.remove('theme-dark');
      } else {
        this.themeBtn = 'btn-light'
        document.body.classList.add('theme-dark');
        document.body.classList.remove('theme-light');
      }
    }
  }
};
</script>
