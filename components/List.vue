<template>
    <div>
        <!-- 받아온 todoList를 card형태로 출력될 수 있도록 만들어줄 것 -->
        <!-- v-card는 메모상자가 생기고 뒤에 그림자가 생긴다 -->
        <!-- v-for를 사용해서 카드의 형태가 반복되게 해준다 -->
        <!-- :key값은 list내용을 넣어줘도 되는데 중복될 수도 있기때문에 오류가 발생하기 때문에 index를 넣어준다 -->
        <!-- index를 넣어준 또 다른 이유는? 할 일 내용이 반복 될텐데 반복된 내용을 수정하거나 지울 때 몇 번째의 todolist인지 찾기 위해-->
        <!-- class="pa-3"의 의미는 vuetify에 클래스이다. padding all 1~5까지의 숫자를 넣어주는 것이다 모든 방향으로 3정도를 넣어줘라 -->
        <v-card class="pa-3 mb-3" :class="{'done': list.status =='done'}" v-for="(list, index) in todoList" :key="index">
            <p class="ma-2">{{list.memo}}</p>
            <!-- list들에 대한 액션 버튼 만들기 -->
            <!-- 할 일을 다 한 완료 버튼 -->
            <!-- 완료 버튼을 눌렀을 때 시그널을 부모컴포넌트로 보낸다 -->
            <!-- 부모컴포넌트가 가지고 있는 todolist에서 해당 리스트를 찾기위해서 index를 올려보내준다 -->
            <!-- 완료버튼을 눌렀을 때 status는 'done'으로 바뀌어야 한다 -->
            <!-- statusControl에 있는 함수를 부모 컴포넌트에서 받아서 실행 시킬 것 -->
            <v-btn v-if="list.status === 'created'" @click="$emit('statusControl', index, 'done')" class="ma-2" fab x-small color="green"><i class="fas fa-check"></i></v-btn>
            <!-- 다시 살릴 수 있는 버튼 -->
            <v-btn v-else @click="$emit('statusControl', index, 'created')" class="ma-2" fab x-small color="blue"><i class="fas fa-redo"></i></v-btn>
            <!-- 삭제 버튼 -->
            <v-btn @click="$emit('listDelete', index)" class="ma-2" fab x-small color="red"><i class="fas fa-trash"></i></v-btn>
            <!-- 수정버튼 -->
            <!-- 완료 됐을 경우에는 수정버튼이 눌리지 않게 해주어야한다 -->
            <v-btn v-if="list.status === 'created'" @click="listEdit(list.memo, index)" class="ma-2" fab x-small color="yellow"><i class="fas fa-trash"></i></v-btn>
        </v-card>
    </div>
</template>
<script>
import {eventBus} from "../main"

export default {
    // 부모컴포넌트의 todoList를 props로 받아오기
    props: ["todoList"],
    methods:{
        listEdit(memo, index){
            eventBus.listEdit(memo, index)
        }
    }
}
</script>

<style scoped>
/* 만약에 이 클래스에 대한 스타일을 list.vue컴포넌트 안에서만 작동되게 만들고 싶다면 scoped라는 속성을 넣어준다 */
.done p{
    text-decoration: line-through;
    color: rgba(0, 0, 0, 0.5);
}
</style>
