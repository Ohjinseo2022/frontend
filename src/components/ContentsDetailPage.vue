<template>
  <div>
    <br />
    <div class="title">
      <span>제목 : </span
      ><input
        v-if="0"
        type="text"
        v-model="state.fakeData[0].title"
        name=""
        id=""
      />
      <span v-if="1">{{ state.fakeData[0].title }}</span>
    </div>
    <br />
    <hr />
    <div>
      <div class="contents" v-if="!state.update">
        {{ state.fakeData[0].contents }}
      </div>
      <textarea
        class="contents"
        v-model="state.fakeData[0].contents"
        v-if="state.update"
      /><br />
      <div class="btn">
        <button v-if="!state.update" @click="updateContents()">수정</button>
        <button v-if="state.update" @click="updateContents()">완료</button>
        |
        <button @click="deletContents()">삭제</button>
      </div>
    </div>

    <div>댓글쓰기</div>
  </div>
</template>
<script>
import router from '@/router'
import { reactive } from '@vue/reactivity'
import store from '@/store'

export default {
  components: {},
  data() {
    return {
      exData: ''
    }
  },
  setup() {
    const state = reactive({
      fakeData: {
        id: '',
        idx: 0,
        title: '',
        contents: '',
        time: ''
      },
      update: false
    })

    const idx = store.state.detailNum.idx

    state.fakeData = store.state.fakeData.filter((data) => {
      return data.idx === idx
    })

    const readContents = () => {
      // db와 통신하여 클릭한 게시글을 담아줘야쥬
      // state.form.tilte and state.form.contents 에 담아 줌
    }
    const updateContents = () => {
      state.update = !state.update
      // 업데이트 로직
    }

    const deletContents = () => {
      // 기본은 삭제 버튼 비활성화 시켜야함
      // 회원정보 체크로직 만들어야함
      const check = window.confirm('삭제하시겠습니까 ?')
      if (check) {
        // 삭제로직 작동 !
        router.push({ path: '/' })
      }
    }
    return { state, updateContents, deletContents, readContents }
  },
  created() {},
  mounted() {},
  unmounted() {},
  methods: {}
}
</script>
<style scoped>
input {
  border: 0;
}
.contents {
  width: 1200px;
  height: 500px;
  padding: 20px;
  resize: none;
  margin: 0 auto;
  text-align: left;
  font-size: 16px;
}
.title {
  text-align: left;
  padding-left: 100px;
}
.btn {
  text-align: right;
}
button {
  width: 80px;
  height: 25px;
}
</style>
