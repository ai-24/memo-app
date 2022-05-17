<template>
  <p class="new-memo" v-if="newMemo">新規メモ</p>
  <form>
    <textarea v-model="memo"></textarea>
    <div class="form-button">
      <button class="add">
        <span v-if="newMemo" @click="onSubmit">新規作成</span>
        <span v-else @click="onRenew">編集</span>
      </button>
      <button class="delete" v-if="!newMemo" @click="onDelete">削除</button>
    </div>
  </form>
</template>

<script>

export default {
  name: 'MemoForm',
  props: {
    newMemo: {
      type: Boolean,
      require: true
    },
    pickedMemo: {
      type: Array
    }
  },
  emits: ['create', 'edit', 'delete'],
  data () {
    return {
      content: '',
      detail: {
        memoTitle: '',
        memoContent: '',
        allMemo: ''
      }
    }
  },
  methods: {
    create () {
      this.detail.allMemo = this.content
      console.log(this.content)
      const memo = this.content.split('\n')
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
  },
  computed: {
    memo: {
      get () {
        return this.pickedMemo
      },
      set (memo) {
        this.content = memo
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
.delete, .add  {
  margin: 10px;
  padding:5px 25px;
  border: none;
  border-radius: 20px;
  background-color: cornflowerblue;
  color: white;
  font-weight: bolder;
}
.form-button {
  text-align: center;
}
.new-memo {
  font-weight: bold;
  margin: 7px 10px;
}
</style>
