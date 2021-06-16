<template>
  <!-- vuetify의 그리드 시스템을 활용한 구조 -->
  <v-container>
    <v-layout row wrap>
      <!-- 화면의 절반을 v-flex가 차지하게 된다 -->
      <!-- v-flex는 class를 넣지 않아도 된다 -->
      <v-flex xs6 pa-2>
        <!-- todoList: []내용을 전달해줘야 한다 -->
        <!-- props -->
        <List :todoList="todoList"/>
      </v-flex>
      <v-flex xs6 pa-2>
        <!-- $emit을 통해 시그널을 받고 그 data를 받은 것을 내부의 있는 빈 Array 값에 넣어주는 작업을 해야 한다 -->
        <!-- @listAdd라는 신호가 오면 "listAdd라는 함수를 실행시켜줘" -->
        <ListAdd @listAdd="listAdd"/>
        <!-- @listAdd라는 함수가 실행되었을 때 listAdd(memo)에서 memo를 인자로 받는다 그 후 todoList: []에 추가 잘 될 것이다-->
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
// List를 보여줄 컴포넌트
import List from "./List"
// List를 추가할 컴포넌트
import ListAdd from "./ListAdd"

export default {
  components: {
    List,
    ListAdd
  },
  data(){
    return{
      todoList: []
    }
  },
  methods: {
    listAdd(memo){
      console.log("받았어!")
      // to do list는 완료하기까지의 과정을 수정할 수 있어야 하기 때문에
      // memo를 string으로 array에 넣는 것이 아니라 객체형태로 넣어준다
      // {속성: 값}
      // listAdd는 list가 생성이 될때만 작성되기 때문에 created라는 status를 하나 넣어준다
      this.todoList.push({memo: memo, status: "created"})
    }
  }
}
</script>