<template>
  <form>
    <textarea v-model="memo"></textarea>
    <button>
      <span v-if="newMemo" @click="onSubmit">新規作成</span>
      <span v-else @click="onRenew">編集</span>
    </button>
    <button @click="onDelete">削除</button>
  </form>
</template>

<script>
export default {
  name: 'MemoForm',
  props: ['newMemo', 'pickedMemo'],
  data () {
    return {
      memo: '',
      detail: {
        memoTitle: '',
        memoContent: '',
        allMemo: ''
      }
    }
  },
  mounted () {
    if (this.pickedMemo.allMemo) {
      this.memo = this.pickedMemo.allMemo
    }
  },
  methods: {
    create () {
      this.detail.allMemo = this.memo
      const memo = this.memo.split('\n')
      this.detail.memoTitle = memo[0]
      memo.shift()
      this.detail.memoContent = memo
    },
    onSubmit () {
      this.create()
      this.$emit('create', this.detail)
    },
    onRenew () {
      this.create()
      this.$emit('edit', this.detail)
    },
    onDelete () {
      this.$emit('delete')
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
