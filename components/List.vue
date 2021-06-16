<template>
    <div>
        <!-- 받아온 todoList를 card형태로 출력될 수 있도록 만들어줄 것 -->
        <!-- v-card는 메모상자가 생기고 뒤에 그림자가 생긴다 -->
        <!-- v-for를 사용해서 카드의 형태가 반복되게 해준다 -->
        <!-- :key값은 list내용을 넣어줘도 되는데 중복될 수도 있기때문에 오류가 발생하기 때문에 index를 넣어준다 -->
        <!-- index를 넣어준 또 다른 이유는? 할 일 내용이 반복 될텐데 반복된 내용을 수정하거나 지울 때 몇 번째의 todolist인지 찾기 위해-->
        <!-- class="pa-3"의 의미는 vuetify에 클래스이다. padding all 1~5까지의 숫자를 넣어주는 것이다 모든 방향으로 3정도를 넣어줘라 -->
        <v-card class="pa-3" v-for="(list, index) in todoList" :key="index">
            <p>{{list.memo}}</p>
            <!-- list들에 대한 액션 버튼 만들기 -->
            <!-- 할 일을 다 한 check 버튼 -->
            <v-btn fab  small color="green"><i class="fas fa-check"></i></v-btn>
            <!-- 다시 살릴 수 있는 버튼 -->
            <v-btn fab  small color="blue"><i class="fas fa-redo"></i></v-btn>
            <!-- 삭제 버튼 -->
            <v-btn fab  small color="red"><i class="fas fa-trash"></i></v-btn>
        </v-card>
    </div>
</template>
<script>
export default {
    // 부모컴포넌트의 todoList를 props로 받아오기
    props: ["todoList"]
}
</script>
