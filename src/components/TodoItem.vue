<template>
  <li>
    <span v-bind:class="{done: item.completed}">
      <input type="checkbox" v-on:change="item.completed = !item.completed" v-bind:checked="item.completed">
      <strong>{{ index + 1 }}</strong>
      {{ item.title | uppercase }}
    </span>
    <button class="re" v-on:click="$emit('remove-item', item.id)">Delete</button>
  </li>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true
    },
    index: Number
  },
  filters: {
    uppercase (value) {
      return value.toUpperCase()
    }
  }
}
</script>

<style scoped>
li {
  border: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  padding: .5rem 2rem;
  margin-bottom: 1rem;
}

input {
  margin-right: 1rem;
}

.re {
  color: #d6133a;
  background-color: #ffff;
  border: none;
  outline: none!important;
  cursor: pointer;
}

.re:hover {
  color: #960c28;
}

.done {
  text-decoration: line-through;
}
</style>
