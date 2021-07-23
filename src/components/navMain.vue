<template>
    <div v-for="(item,index) in list" :key="index">
        <div>
            <input type="checkbox" v-model="item.complete">
            {{ item.title}}
            <button @click="del(item,index)">删除</button>
        </div>
    </div>
</template>

<script>
    import {defineComponent,ref} from 'vue'
    export default defineComponent({
        name: "navMain",
        props:{
            list:{
                type:Array,
                required:true
            }
        },
        emits:['del'],
        setup(props,txt){
            let del = (item,index)=>{
                txt.emit('del',index)
                console.log(item);
                console.log(index);
            }
            return{
                del,
            }
        }
    })
</script>

<style scoped>

</style>