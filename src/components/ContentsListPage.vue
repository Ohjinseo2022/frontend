<template>
  <div class="contents">
    <br />
    <hr />
    <div class="title">자유게시판</div>
    <table class="table">
      <tr>
        <th>No</th>
        <th>제목</th>
        <th>작성자</th>
        <th>작성시간</th>
        <th>댓글수</th>
      </tr>
      <tr v-for="i in state.fakeData" :key="i.idx">
        <td>{{ i.idx }}</td>
        <td>
          <div @click="detailgo(i.idx)">{{ i.title }}</div>
        </td>
        <td>{{ i.id }}</td>
        <td>{{ i.time }}</td>
        <td>0</td>
      </tr>
    </table>
    <button class="createText" @click="createText()">글쓰기</button>
    <br />
    <br />
    <hr />
  </div>
</template>
<script>
import router from '@/router'

import { reactive } from '@vue/reactivity'
import { useStore } from 'vuex'

export default {
  components: {},
  data() {
    return {
      sampleData: ''
    }
  },

  setup() {
    const state = reactive({
      fakeData: {
        id: [],
        idx: [],
        title: [],
        contents: [],
        time: []
      }
    })
    const store = useStore()
    const createText = () => {
      if (store.state.account.id) {
        router.push({ path: '/create' })
      } else {
        window.alert('로그인한 회원만 글쓰기가 가능합니다.')
      }
    }
    state.fakeData = store.state.fakeData
    const detailgo = (e) => {
      store.commit('setNumber', e)
      router.push({ path: '/detail' })
    }

    return { createText, state, detailgo }
  },
  created() {},
  mounted() {},
  unmounted() {},
  methods: {}
}
</script>
<style scoped>
.contents {
  width: 100%;
}
.title {
  text-align: start;
  font-size: 2rem;
  font-weight: bold;
  margin-bottom: 2rem;
  margin-top: 3rem;
}
.table {
  width: 1440px;
  align-content: center;
  border-top: 1px solid black;
  border-collapse: collapse;
  padding: 8px;
  margin-bottom: 12px;
}
.table > tr > th,
td {
  padding: 8px;
  border-top: 1px solid gray;
  border-bottom: 1px solid gray;
}
.table > tr > th:first-child {
  width: 32px;
}

.table > tr > th:nth-child(2) {
  width: 900px;
}
.table > tr > th > td {
  font-weight: bold;
}
.table > tr > td:nth-child(2) {
  padding: 16px;
  text-align: left;
}
.table > tr > td:nth-child(3),
td:nth-child(4),
td:nth-child(5) {
  color: #c9c6c6;
}
.createText {
  margin: 0 5px;
  position: relative;
  left: 650px;
  width: 100px;
  height: 30px;
  background: #7f00cb;
  border: 0;
  color: #c9c6c6;
  font-weight: bold;
  border-radius: 5px;
}
.createText:active {
  background: #ec65ff;
}

a {
  color: inherit;
  text-decoration: none;
}
</style>
