<template>
  <Navber />
  <Event :text="text[eventTextNum]" @stopInterval="stopInterval()" />
  <SearchBar :data="data_temp" @searchBoss="searchBoss($event)" />
  <p>
    <button v-on:click="showAllBoss()">전체보기</button>
  </p>
  <Bosses
    :data="data_temp"
    @openModal="
      isModal = true;
      selectedBoss = $event;
    "
    @increseLike="increseLike($event)"
  />
  <Modal
    :data="data"
    :isModal="isModal"
    :selectedBoss="selectedBoss"
    @closeModal="isModal = false"
  />
</template>

<script>
import data from "./assets/boos";
import Navber from "./components/Navbar.vue";
import Modal from "./components/Modal.vue";
import Event from "./components/Event.vue";
import Bosses from "./components/Bosses.vue";
import SearchBar from "./components/SearchBar.vue";
export default {
  name: "App",
  data() {
    return {
      isModal: false,
      data: data, // 원본
      data_temp: [...data], // 사본
      selectedBoss: 0,
      text: ["군단장 레이드1", "군단장 레이드2", "군단장 레이드3"],
      eventTextNum: 0,
      interval: null,
    };
  },
  methods: {
    increseLike(id) {
      // this.data[i].like += 1;
      this.data.find((boss) => {
        if (boss.id == id) {
          boss.like += 1;
        }
      });
    },

    searchBoss(bossName) {
      this.data_temp = this.data.filter((boss) => {
        return boss.name.includes(bossName);
      });
    },

    showAllBoss() {
      this.data_temp = [...this.data];
    },

    stopInterval() {
      clearInterval(this.interval); // 인터벌 멈춤
    },
  },
  components: {
    Navber: Navber,
    Modal: Modal,
    Event: Event,
    Bosses: Bosses,
    SearchBar: SearchBar,
  },
  mounted() {
    this.interval = setInterval(() => {
      if (this.eventTextNum == this.text.length - 1) {
        this.eventTextNum = 0;
      } else {
        this.eventTextNum += 1;
      }
    }, 3000);
  },
  unmounted() {
    clearInterval(this.interval); // 인터발 해제
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
}

body {
  max-width: 768px;
  margin: 0 auto;
  padding: 20px;
}

h1,
h2,
h3 {
  margin-bottom: 1rem;
}

p {
  margin-bottom: 0.5rem;
}

button {
  margin-right: 10px;
  margin-top: 1rem;
}

.item {
  width: 100%;
  border: 1px solid #ccc;
  display: flex;
  margin-bottom: 20px;
  padding: 1rem;
}

.item figure {
  width: 30%;
  margin-right: 1rem;
}
.item img {
  width: 100%;
}
.item .info {
  width: 100%;
}
.modal {
  background: rgba(0, 0, 0, 0.7);
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal .inner {
  background: #fff;
  width: 80%;
  padding: 20px;
  border-radius: 10px;
}
</style>
