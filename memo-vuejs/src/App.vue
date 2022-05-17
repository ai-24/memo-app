<template>
  <div class="background" @click.self="hideForm">
    <div class="title">
      <h1>{{ title }}</h1>
    </div>
    <div class="memo-list" v-if="memos">
      <MemoList :memos="memos"
                @show-detail="resetForm"
                @hide-form="hideForm"
      ></MemoList>
    </div>
    <div class="new" @click.self="hideForm">
      <NewMemo @open="newForm"></NewMemo>
    </div>
  </div>
  <div class="form" v-if="form">
    <MemoForm :newMemo="newMemo"
              :pickedMemo="pickedMemo"
              @create="onCreate"
              @edit="onEdit"
              @delete="onDestroy"
    ></MemoForm>
  </div>
</template>

<script>
import MemoList from './components/MemoList.vue'
import MemoForm from '@/components/MemoForm.vue'
import NewMemo from '@/components/NewMemo.vue'

export default {
  name: 'App',
  components: { NewMemo, MemoList, MemoForm },
  data () {
    return {
      title: 'Memos',
      form: false,
      newMemo: false,
      memos: [],
      pickedMemo: [],
      index: ''
    }
  },
  mounted () {
    this.memos = JSON.parse(localStorage.getItem('memos'))
  },
  methods: {
    onDestroy () {
      const isDelete = confirm('削除しますか？')
      if (isDelete) {
        this.memos.splice(this.index, 1)
        localStorage.setItem('memos', JSON.stringify(this.memos))
      }
    },
    onEdit (detail) {
      this.memos.splice(this.index, 1, detail)
      localStorage.setItem('memos', JSON.stringify(this.memos))
    },
    onCreate (detail) {
      this.memos.push(detail)
      localStorage.setItem('memos', JSON.stringify(this.memos))
    },
    newForm () {
      this.newMemo = true
      this.pickedMemo = []
      this.form = true
    },
    hideForm () {
      this.form = false
    },
    resetForm (memo) {
      this.hideForm()
      this.onForm(memo)
    },
    onForm (memo) {
      if (this.pickedMemo) {
        this.pickedMemo = []
      }
      this.index = memo[1]
      this.pickedMemo.splice(this.index, 1, memo[0].allMemo)
      this.newMemo = false
      this.form = true
    }
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
.background {
  top: 0;
  position: absolute;
  width: 100%;
  height: 200%;
}
.title {
  margin: 50px 0 0 100px;
}
.memo-list {
  display: inline-block;
  width: 500px;
  margin-left: 10px;
  position: relative;
}
.form {
  display: inline-block;
  position: absolute;
  top: 130px;
  left: 530px;
  height: 400px;
  width: 300px;
}
.new {
  top: 100px;
  margin-left: 15px;
}
</style>
