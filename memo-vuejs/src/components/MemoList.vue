<template>
    <ul v-for="(memo, index) in memos" :key="memo">
      <li @click="showMemo(memo, index)"><span class="list-text">{{ memo.memoTitle }}</span></li>
    </ul>
</template>

<script>
export default {
  name: 'MemoList',
  props: ['memos'],
  emits: ['showDetail'],
  methods: {
    showMemo (memo, index) {
      this.$emit('showDetail', [memo, index])
    }
  }
}
</script>

<style scoped>
.list-text:hover {
  color: black;
  cursor: pointer;
}

</style>
