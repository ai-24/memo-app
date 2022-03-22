<template>
  <form>
    <textarea v-model="memo"></textarea>
    <button>
      <span v-if="newMemo" @click="onSubmit">新規作成</span>
      <span v-else @click="onEdit">編集</span>
    </button>
    <button @click="onDelete">削除</button>
  </form>
</template>

<script>
export default {
  name: 'MemoForm',
  props: ['newMemo', 'memos', 'pickedMemo', 'index'],
  data () {
    return {
      memo: '',
      detail: {
        memoTitle: '',
        memoContent: '',
        allMemo: ''
      },
      memosArray: []
    }
  },
  mounted () {
    if (this.pickedMemo.allMemo) {
      this.memo = this.pickedMemo.allMemo
    }
  },
  methods: {
    onSubmit () {
      this.memosArray = this.memos
      this.detail.allMemo = this.memo
      const memo = this.memo.split('\n')
      this.detail.memoTitle = memo[0]
      memo.shift()
      this.detail.memoContent = memo
      this.saveMemo()
    },
    saveMemo () {
      this.memosArray.push(this.detail)
      localStorage.setItem('memos', JSON.stringify(this.memosArray))
      this.$emit('renew')
    },
    onEdit () {
      this.memosArray = this.memos
      this.detail.allMemo = this.memo
      const memo = this.memo.split('\n')
      this.detail.memoTitle = memo[0]
      memo.shift()
      this.detail.memoContent = memo
      this.memosArray.splice(this.index, 1, this.detail)
      localStorage.setItem('memos', JSON.stringify(this.memosArray))
      this.$emit('renew')
    },
    onDelete () {
      this.memosArray = this.memos
      const isDelete = confirm('削除しますか？')
      if (isDelete) {
        this.memosArray.splice(this.index, 1)
        localStorage.setItem('memos', JSON.stringify(this.memosArray))
        this.$emit('renew')
      }
    }
  }
}
</script>

<style scoped>
textarea, form {
  height: 400px;
  width: 300px;
}

</style>
