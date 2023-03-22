<script setup>
import { onMounted, onUnmounted, ref } from "vue";
import testData from "../src/assets/data";
import CardComponent from "@/components/CardComponet.vue";
import OneRoomModal from "@/components/OneRoomModal.vue";
import DisCount from "@/components/DisCount.vue";

const data = ref({
  menus: ["Home", "Shop", "About"],
  bgColor: "color : green",
  showDiscount: true,
  disCountState: 40,
  oneRooms: [...testData],
  oneRoomsOrigin: [...testData],
  selectedOneRoom: {},
  // obj: { name: "kim", age: 20 },
  oneRoomIndex: 0,
  modalState: false,
});

const sortBack = () => {
  data.value.oneRooms = [...data.value.oneRoomsOrigin];
};
const priceSort = () => {
  data.value.oneRooms.sort(function (a, b) {
    console.log(a.price, b.price);
    return a.price - b.price;
  });
};
const sortWord = () => {
  data.value.oneRooms.sort(function (a, b) {
    let aa = a.title.toString().toLowerCase();
    let bb = b.title.toString().toLowerCase();
    return aa < bb ? -1 : aa == bb ? 0 : 1;
  });
};
const reversePriceSort = () => {
  data.value.oneRooms.sort(function (a, b) {
    return b.price - a.price;
  });
};
const openModal = () => {
  data.value.modalState = true;
  console.log("sdfds", data.value.selectedOneRoom);
};
const lessSort = () => {
  data.value.oneRooms.filter(function (a) {
    return a.price <= 500000;
  });
};

let interval;

onMounted(() => {
  interval = setInterval(() => {
    if (data.value.disCountState > 0) {
      data.value.disCountState -= 1;
    } else {
      clearInterval(interval);
    }
  }, 1000);
  //40초후
  //   setTimeout(() => {
  //     data.value.showDiscount = false;
  //   }, 40000);
});

onUnmounted(() => {
  clearInterval(interval);
});
</script>

<template>
  <OneRoomModal
    v-if="data.modalState"
    @closeModal="data.modalState = false"
    :one-room="data.selectedOneroom"
    :modal-state="data.modalState"
  />

  <!--  content -->
  <v-card class="d-flex flex-column">
    <v-img
      :width="200"
      aspect-ratio="4/3"
      cover
      alt="Vue logo"
      src="@/assets/logo.png"
    ></v-img>
    <!--menu-->
    <v-card class="flex-row d-flex rounded-xl">
      <v-card
        class="bg-amber-accent-4 text-blue-accent-1 v-card-title flex-grow-1"
        v-for="(menu, index) in data.menus"
        :key="index"
        :style="data.bgColor"
        >{{ menu }}
      </v-card>
    </v-card>
    <!--배너-->
    <DisCount
      v-if="data.showDiscount == true"
      :disCountState="data.disCountState"
    />
    <!--버튼-->
    <v-card class="d-flex flex-row">
      <v-btn variant="outlined" @click="priceSort">가격낮은순정렬</v-btn>
      <v-btn variant="outlined" @click="sortWord">가나다순</v-btn>
      <v-btn variant="outlined" @click="sortBack">되돌리기</v-btn>
      <v-btn variant="outlined" @click="reversePriceSort">가격높은순</v-btn>
      <v-btn variant="outlined" @click="lessSort">50만원이하 상품</v-btn>
    </v-card>
    <!--카드-->
    <div v-for="(item, index) in data.oneRooms" :key="`div${index}`">
      <CardComponent
        @click="data.selectedOneroom = item"
        @openModal="openModal"
        :one-Room="item"
        :bg-color="data.bgColor"
        히히="히히"
      />
    </div>
  </v-card>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}

body {
  margin: 0;
}

div {
  box-sizing: border-box;
}

.start {
  opacity: 0;
  transition: all 1s;
}

.end {
  opacity: 1;
}
</style>
