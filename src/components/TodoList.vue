<template>
  <div>
    <ul>
      <TodoItem
        v-for="(item, i) in todos"
        :key="item.id"
        v-bind:item="item"
        v-bind:index="i"
        v-on:remove-item="removeItem"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from '@/components/TodoItem'

export default {
  props: ['todos'],
  components: {
    TodoItem
  },
  methods: {
    removeItem (id) {
      this.$emit('remove-item', id)
    }
  }
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
