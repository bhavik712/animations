<template>
    <input type="number" @change="addItem($event)">
    <ul>
        <transition-group name="fade">
            <li v-for="(number,index) in numList" :key="number" @click="removeItem(index)">{{ number }}</li>
        </transition-group>
        
    </ul>
</template>

<script>
    export default {
        name:'List',
        props:['numList'],
        emits:['add-number','remove-number'],

        methods:{
            addItem(event){
                const num = event.target.value;
                if(num){
                    this.$emit('add-number',num);
                }
            },
            removeItem(index){
                this.$emit('remove-number',index);
            }
        }
    }
</script>

<style>
li{
    cursor: pointer;
}

.fade-enter-from{
  opacity: 0;
}
.fade-enter-active{
  transition: all 1s linear;
}
.fade-leave-active{
    position: absolute;
}
.fade-leave-to{
  transition: all 1s linear;
  opacity: 0;
}
.fade-move{
    transition: all 1s linear;
}


</style>