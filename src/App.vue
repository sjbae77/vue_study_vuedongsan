<template>

  <Transition name="fade">
    <Modal :onerooms="onerooms" :target="target" :modal="modal" 
    @closeModal="modal = false;" />
  </Transition>
  

  <div class="menu">
    <a v-for="(menu,i) in menus" :key="i">{{ menu }}</a>
  </div>

  <DiscountBanner v-if="showDiscount == true" :discount="discount" />

  <button @click="priceSort">가격순</button>
  <button @click="sortABC">가나다순</button>
  <button @click="sortBack">되돌리기</button>

  <Card v-for="(oneroom,i) in onerooms" :key="i"
  :oneroom="oneroom"
  @openModal="modal = true; target=$event" />

</template>

<script>

import data from "./assets/oneroom.js";
import DiscountBanner from "./components/DiscountBanner.vue";
import Modal from "./components/Modal.vue";
import Card from "./components/Card.vue";

export default {
  name: 'App',
  //데이터 보관함
  data(){
    return {
      target: 0,
      onerooms: data,
      modal: false,
      menus: ["Home", "Shop", "About"],
      org: [...data],
      showDiscount: true,
      discount: 30,
    }
  },
  //함수 만드는 공간
  methods : {
    priceSort(){
      this.onerooms.sort(function(a,b){
        return a.price - b.price
      })
    },
    sortBack() {
      this.onerooms = [...this.org];
    },
    sortABC(){
      this.onerooms.sort(function(a,b){
        return a.title.localeCompare(b.title)
      });
    },
  },
  // mounted(){
  //   setTimeout(()=>{
  //     this.showDiscount = false;
  //   },2000);
  // },
  created(){
    let timer = setInterval(() => {
      this.discount--;
      if(this.discount <= 0) clearInterval(timer);
    }, 1000);
  },
  components: {
    //왼쪽이름으로 사용하겠다
    //오른쪽은 위에서 import해온 변수명
    //Discount: Discount,

    //왼쪽 오른쪽 이름이 같다면 축약해서 사용가능(es6)
    DiscountBanner,
    Modal,
    Card,
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%; height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding: 15px;
}
.menu a {
  color: white;
  padding: 10px;
}

.room-img {
  width: 100%;
  max-width: 800px;
  margin-top: 40px;
}

/* 애니메이션 */
.start {
  opacity: 0;
  transition: all 1s;
}
.end {
  opacity: 1;
}

.fade-enter-from {
  opacity: 0;
}
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  opacity: 1;
}

.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  opacity: 0;
}

</style>
