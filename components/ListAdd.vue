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
        <v-btn v-if="mode==='add'" class="ma-3" @click="listAdd">추가</v-btn>
        <v-btn v-if="mode==='edit'" class="ma-3" @click="listEdit">수정</v-btn>
    </div>
</template>
<script>
import {eventBus} from "../main"

export default {
    data(){
        return{
            // v-model로 binding 시킨 memo
            memo: null,
            index: null,
            mode: "add"
            // memo를 인자로 받아서 $emit을 통해서 부모컴포넌트로 신호를 보내도록 하겠다
        }
    },
    created(){
        eventBus.$on('listEdit', (memo, index) => {
            this.memo = memo
            this.index = index
            this.mode = "edit"
        })
    },
    methods: {
        listAdd(){
            // 빈 내용을 추가했을 경우
            if(this.memo === null){
                alert("내용을 입력해주세요.")
            }else{
                this.$emit("listAdd", this.memo)
                this.memo = null
            }
        },
        listEdit(){
            if(this.memo === null){
                alert("내용을 입력해주세요.")
            }else {
                this.$emit("listEdit", this.memo, this.index)
                this.memo = null
                this.mode = "add"
            }
        }
    }
}
</script>
