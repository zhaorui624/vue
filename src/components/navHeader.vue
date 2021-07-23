<template>
    <div>
        <input type="text" placeholder="请输入一个数据" v-model="value" @keydown.enter="enter" >
    </div>
</template>

<script>
    import {defineComponent,ref} from 'vue'
    export default defineComponent({
        name: "navHeader",
        setup(props,txt){
            let value = ref('')
            let enter = ()=>{
                // console.log(value.value)
                txt.emit('add',value.value)
            }
            return{
                value,
                enter
            }
        }
    })
</script>

<style scoped>

</style>