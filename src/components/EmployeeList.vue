<template>
  <div  v-for="(item, index) in items" :key="index">
    <p v-if="item.type === 'user'">
      {{ item.name }} - {{ item.salary }} ₽
    </p>

    <div class="sublist" v-if="item.childs && item.childs.length">
      <h2>{{item.name}}</h2>
      <employees :items="item.childs"></employees>
    </div>

  </div>
</template>

<script>
export default {
  name: "employees",
  props: {
    items: {
      type: Array,
      required: true
    }
  }
};
</script>