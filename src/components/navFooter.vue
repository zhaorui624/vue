<template>
    <div class="container">
        <div>已完成{{isComplete}} / 全部{{ list.length}}</div>
        <button v-if="isComplete > 0" @click="clear">清除已完成</button>
    </div>
</template>

<script>
    import {defineComponent,ref,computed} from 'vue'
    export default defineComponent({
        name:'navFooter',
        props:{
            list:{
                type:Array,
                required:true
            }
        },
        setup(props,txt){
            let isComplete =computed(()=>{
            let arr = props.list.filter(item=>{
                return item.complete
            })
                return arr.length
            })
            //清除方法
            let clear = ()=>{
                let arr = props.list.filter(item=>{
                    return item.complete === false
                })
                txt.emit('clear',arr)
            }
            return{
                isComplete,
                clear
            }
        }
    })
</script>

<style scoped>

</style>