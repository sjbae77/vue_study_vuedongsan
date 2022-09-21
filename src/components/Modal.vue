<template>
  <div class="black-bg" v-if="modal === true">
    <div class="white-bg">
      <h4>{{ onerooms[target].title }}</h4>
      <img :src="onerooms[target].image" alt="방사진">
      <p>{{ onerooms[target].content }}</p>
      <!-- <input @input="month = $event.target.value"> -->
      <input v-model.number="month">
      <p>{{ month }}개월 선택함 : {{ onerooms[target].price * month }}원</p>
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  data() {
    return {
      month: "",
    }
  },
  watch : {
    month(a){
      if (typeof(a) == "string"){
        alert('숫자로 입력해주세요');
        this.month = "";
      }
    },
  },
  beforeUpdate() {
    if(this.month == 2){
      alert("해당 개월수는 불가능합니다.");
      this.month = 1;
    }  
  },
  props: {
    onerooms: Array,
    target: Number,
    modal: Boolean,
  }
}
</script>

<style>

</style>