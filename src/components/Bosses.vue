<template>
  <div class="container">
    <h1>보스 정보</h1>
    <div v-for="boss in data" :key="boss.id" class="item">
      <figure>
        <img :src="boss.imgUrl" :alt="boss.name" />
      </figure>

      <div class="info">
        <h3 class="bg-yellow" :style="textRed">{{ boss.name }}</h3>

        <p>출시일 : {{ boss.year }}</p>
        <p>장르 : {{ boss.tribe }}</p>
        <!-- <button v-on:click="increseLike(i)">좋아요</button> -->
        <button v-on:click="$emit('increseLike', boss.id)">좋아요</button>
        <span>{{ boss.like }}</span>
        <p>
          <button v-on:click="$emit('openModal', boss.id)">상세보기</button>
        </p>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "BossesComponent",
  props: {
    data: Array,
  },
};
</script>
<style>
.container {
  padding: 20px;
}
</style>
