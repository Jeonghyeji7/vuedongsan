<script setup>
import { ref, defineProps, defineEmits } from "vue";

const month = ref(1);
const range = ref(1);

const props = defineProps({
  oneRoom: Array,
  modalState: Boolean,
});

const modalState = ref(props.modalState);

const validateMonth = (event) => {
  const value = Number(event.target.value);
  if (typeof value !== "number") {
    if (value !== "") {
      alert("숫자만 입력해!");
      month.value = 1;
    }
  } else if (value >= 13) {
    alert("13개월은 없어!");
    month.value = 1;
  } else {
    range.value = value;
  }
};
const validateRange = (event) => {
  const value = event.target.value;
  month.value = value;
};

const emits = defineEmits(["closeModal"]);
const closeModal = () => {
  emits("closeModal");
};
// 걍 $emit("closeModal") 도 가능
</script>

<template>
  <!--  @input v-model과 같음, 대신 number같은거 붙일수 있는듯?    -->
  <!--      input,textarea,select 다 v-model 가능-->
  <!-- v-modal.number와 <input @input="month=$event.target.value">-->

  <v-dialog width="auto" v-model="modalState">
    <v-card class="bg-green-lighten-2 pa-4">
      <v-img :src="props.oneRoom.image"></v-img>
      <v-card-title>{{ props.oneRoom.title }}</v-card-title>
      <v-card-text>{{ props.oneRoom.content }}</v-card-text>
      <input
        type="range"
        max="12"
        min="1"
        v-model.number="range"
        @input="validateRange($event)"
      />
      <input v-model.number="month" @input="validateMonth($event)" />
      <v-card-text>
        {{ month }}개월 선택함 : {{ props.oneRoom.price * month }}원
      </v-card-text>
      <v-card-actions>
        <v-btn color="primary" block @click="closeModal">Close</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<style scoped>
.black-bg {
  position: fixed;
}
</style>
