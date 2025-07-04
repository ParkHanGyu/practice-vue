<template>
  <div class="search-box">
    <!-- <input type="search" @input="inputText = $event.target.value" /> -->
    <!-- <input type="search" v-model="inputText" /> -->
    <input
      type="search"
      @change="
        $emit('searchBoss', $event.target.value);
        inputText = $event.target.value;
        $event.target.value = '';
      "
    />

    <button>검색</button>
  </div>
  <p>{{ inputText }}</p>
</template>
<script>
export default {
  name: "SearchBarComponent",
  data() {
    return {
      inputText: "",
    };
  },
  watch: {
    inputText(searchValue) {
      const findName = this.data.filter((boss) => {
        return boss.name.includes(searchValue);
      });

      if (findName.length == 0) {
        alert("해당 보스는 없는 보스입니다.");
      }
    },
  },

  props: {
    data: Array,
  },
};
</script>
<style>
.search-box {
  padding: 10px;
  display: flex;
  justify-content: center;
}

.search-box input {
  padding: 5px 10px;
}

.search-box button {
  margin: 0;
}
</style>
