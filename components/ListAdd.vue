<template>
    <div>   
        <!-- 할 일을 입력할 수 있는 텍스트필드 -->
        <!-- v-model을 통해서 vue 인스턴스와 연결 -->
        <v-textarea
            outlined
            v-model = "memo"
            label="투두리스트를 입력해주세요"
            value=""
        ></v-textarea>

        <!-- 부모컴포넌트로 $emit을 보낼 수 있는 추가버튼 -->
        <v-btn @click="listAdd">추가</v-btn>
    </div>
</template>
<script>
export default {
    data(){
        return{
            // v-model로 binding 시킨 memo
            memo: null
            // memo를 인자로 받아서 $emit을 통해서 부모컴포넌트로 신호를 보내도록 하겠다
        }
    },
    methods: {
        listAdd(){
            console.log('리스트 추가')
            // 빈 내용을 추가했을 경우
            if(this.memo === null){
                alert("내용을 입력해주세요.")
            }else{
                this.$emit("listAdd", this.memo)
            }
        }
    }
}
</script>
