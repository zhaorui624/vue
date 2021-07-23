<template>
    <div>
        <nav-header @add="add"/>
        <nav-main :list="list" @del="del"></nav-main>
        <nav-footer :list="list" @clear="clear"/>
<!--        <div>{{list}}</div>-->
<!--        <button @click="goto">跳转</button>-->
    </div>
</template>

<script>
    import navHeader from '../components/navHeader'
    import navMain from '../components/navMain'
    import navFooter from '../components/navFooter'
    import {defineComponent,computed,ref} from 'vue'
    import {useStore} from 'vuex'
    import {useRouter} from 'vue-router'
    export default defineComponent({
        name:'Home',
        components:{
            navHeader,
            navMain,
            navFooter
        },
        setup(){
            let store = useStore();
            // console.log(store)
            let list = computed(()=>{ return store.state.list})
            // let router = useRouter()
            // console.log(router)
            // let goto = ()=>{
            //     router.push('/about')
            // }
            let value = ref('')
            let add = (val)=>{
                value.value = val;
                //判断
                let flag = true;
                list.value.map((item)=>{
                    if(item.title === value.value){
                        //重复
                        flag = false
                        alert('任务已经存在了')
                    }
                })
                //调用mutation
               if(flag){
                   store.commit('addTodo',{
                       title:value.value,
                       complete:false
                   })
               }
                console.log(val);
            }
            //删除
            let del = (val)=>{
                store.commit('delTodo',val)
            }
            let clear = (val)=>{
                store.commit('clear',val)
            }
            return{
                list,
                value,
                add,
                del,
                clear
            }
        }
    })
</script>

<style scoped lang="scss">

</style>