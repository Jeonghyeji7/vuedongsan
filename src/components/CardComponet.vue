<script setup>
import { defineProps, defineEmits, ref } from "vue";
const props = defineProps({
  oneRoom: Object,
  bgColor: String,
  히히: String,
});

const data = ref({ show: false });

console.log(props.히히);

const emits = defineEmits(["openModal"]);

const handleModal = () => {
  emits("openModal", props.oneRoom.id);
};
</script>

<template>
  <!--  커스텀 이벤트!!! 자식->부모 : 메세지 보냄-->
  <v-card class="mx-auto ma-4" max-width="344" @click="handleModal">
    <v-card class="mx-auto">
      <v-img :src="props.oneRoom.image" height="200px" cover></v-img>
      <v-card-title :style="props.bgColor">
        {{ props.oneRoom.title }}
      </v-card-title>
      <v-card-subtitle>
        {{ props.oneRoom.content }}
      </v-card-subtitle>
      <v-card-text>{{ props.oneRoom.price }} 원</v-card-text>
    </v-card>
    <v-card-actions>
      <v-btn color="orange-lighten-2" variant="text"> 더보기 </v-btn>
      <v-spacer></v-spacer>
      <v-btn
        :icon="data.show ? 'mdi-chevron-up' : 'mdi-chevron-down'"
        @click="data.show = !data.show"
      ></v-btn>
    </v-card-actions>
    <v-expand-transition>
      <div v-show="data.show">
        <v-divider></v-divider>
        <v-card-text>
          I'm a thing. But, like most politicians, he promised more than he
          could deliver. You won't have time for sleeping, soldier, not with all
          the bed making you'll be doing. Then we'll go with that data file!
          Hey, you add a one and two zeros to that or we walk! You're going to
          do his laundry? I've got to find a way to escape.
        </v-card-text>
      </div>
    </v-expand-transition>
  </v-card>
</template>

<style scoped></style>

<!--단, vite로 바꿔야함-->
<!--https://eslint.vuejs.org/user-guide/#does-not-work-well-with-script-setup-->
<!--defineProps와 defineEmits는 컴파일러 매크로로써, -->
<!--<script setup> 내에서만 사용할 수 있습니다. 이들은 import할 필요가 없으며, <script setup>이 컴파일될 때 제거됩니다[1]. -->
<!--  따라서 defineProps를 사용할 때 import 과정은 불필요-->
