<script setup> 
import {defineProps,defineEmits} from 'vue'

const props = defineProps({text:{
    type:String,
    default:'默认按钮'
}})
const emit = defineEmits(['ok'])
function send(){
    emit('ok','父组件参数')
}

</script>

<template>
    <div @click="send" class="button">{{text}}</div>
</template>

<style scoped>
    .button{
        margin: 100px 0 0 200px;
        width: 100px;
        height: 50px;
        line-height: 50px;
        text-align: center;
        background-color: rgb(255, 255, 255);
        border-radius: 10px;
        white-space: nowrap;
    }
</style>