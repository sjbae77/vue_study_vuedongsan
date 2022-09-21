<template>
  <div>
    <img :src="oneroom.image" alt="방사진" class="room-img" style="cursor:pointer"
    @click="sendModal">
    <h4>{{ oneroom.title }}</h4>
    <p>{{ oneroom.price }}원</p>
  </div>
</template>

<script>
export default {
    name: "Card",
    props: {
        oneroom: Object,
    },
    methods: {
        sendModal() {
            this.$emit('openModal', this.oneroom.id)
        }
    }
}
</script>

<style>

</style>