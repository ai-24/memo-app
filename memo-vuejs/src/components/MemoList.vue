<template>
    <ul v-for="(memo, index) in memos" :key="memo">
      <li @click="showMemo(memo, index)" @click.self="$emit('hideForm')"><span class="list-text">{{ memo.memoTitle }}</span></li>
    </ul>
</template>

<script>
export default {
  name: 'MemoList',
  props: {
    memos: {
      type: Array
    }
  },
  emits: ['showDetail', 'hideForm'],
  methods: {
    showMemo (memo, index) {
      this.$emit('showDetail', [memo, index])
    }
  }
}
</script>

<style scoped>
.list-text:hover {
  color: darkgray;
  cursor: pointer;
}
.list-text {
  color: black;
}

</style>
