<template>
  <div>
    <button @click="flag=!flag">Toggle</button>
    <!-- <transition name="fade" mode="out-in">   
      <h2 v-if="flag" key="main">Good Morning</h2>
      <h2 v-else key="secondary">Good Evening</h2>
    </transition>  -->

    <transition
    @before-enter="beforeEnter"
    @enter="enter"
    @after-enter="afterEnter"
    @before-leave="beforeLeave"
    @leave="leave"
    @after-leave="afterLeave"
    :css="true"
    name="zoom"
    >
      <h2 v-if="flag">Hello</h2>
    </transition>

  </div>
  <list :numList="numbers" @add-number="addNumber" @remove-number="removeNumber"></list>
</template>

<script>
  import List from './components/list.vue'
  export default {
    name:'App',

    data(){
      return {
        flag: false,
        numbers: [1,2,3,4,5]
      }
    },
    components: {
      List
    },
    methods:{
      addNumber(num){
        this.numbers.push(num);
      },
      removeNumber(index){
        this.numbers.splice(index,1)
      },
      beforeEnter(el){
        console.log('be');
      },
      enter(el){
        // const animation = el.animate([{transform: "scale3d(0,0,0)"},{}],{
        //   duration:1000
        // })
        // animation.onfinish = () =>  done();
      },
      afterEnter(el){
        console.log('ae');
      },
      beforeLeave(el){
        console.log('bl');
      },
      leave(el){
        // const animation = el.animate([{},{transform: "scale3d(0,0,0)"}],{
        //   duration:1000
        // })
        // animation.onfinish = () =>  done();

        console.log('l')
      },
      afterLeave(el){
        console.log('al')
      }
    }
  }
</script>

<style>
h2{
  width: 400px;
  padding: 20px;
}

.zoom-enter-from{
  opacity: 0;
}
.zoom-enter-active{
  animation: zoom-in 1s linear forwards;
  transition: all 1s linear;
}

.zoom-leave-to{
  transition: all 1s linear;
  opacity: 0;
}
.zoom-leave-active{
  animation: zoom-out 1s linear forwards;
}
@keyframes zoom-in{
  from{
    transform:scale(0,0);
  }
  to{
    transform:scale(1,1);
  }
}
@keyframes zoom-out{
  from{
    transform:scale(1,1)
  }
  to{
    transform:scale(0,0)
  }

}

.fade-enter-from{
  opacity: 0;
}
.fade-enter-active{
  transition: all 1s linear;
}
.fade-leave-to{
  transition: all 1s linear;
  opacity: 0;
}

</style>


