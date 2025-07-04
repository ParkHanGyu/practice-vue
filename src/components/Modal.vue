<template>
  <div class="modal" v-if="isModal">
    <div class="inner">
      <h3>{{ data[selectedBoss].name }}</h3>
      <p>보스 상세정보</p>
      <button v-on:click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>
<script>
export default {
  name: "ModalComponent",
  props: {
    data: Array,
    isModal: Boolean,
    selectedBoss: Number,
  },
};
</script>
<style></style>
