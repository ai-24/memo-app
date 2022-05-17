<template>
  <button class="create-new-memo" @click="createMemo">+</button>
</template>

<script>
export default {
  name: 'NewMemo',
  emits: ['open'],
  methods: {
    createMemo () {
      this.$emit('open')
    }
  }
}
</script>

<style scoped>
.create-new-memo {
  width: 40px;
  height: 40px;
  font-size: 30px;
  background-color: white;
  border-color: white;
  border-style: none;
  margin-left: 10px;
}
.create-new-memo:hover {
  color: darkgray;
  cursor: pointer;
}
</style>
