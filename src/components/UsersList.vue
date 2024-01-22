<script setup lang="ts">
import { PropType, defineProps, defineEmits, ref } from "vue";

import User from "../types/user";

//props
const props = defineProps({
  users: {
    type: Array as PropType<User[]>,
    required: true,
  },
  isDisabledBtnLoad: {
    type: Boolean,
    required: true,
  },
});

//data
const currentUser = ref<User | null>();

//emits
const emit = defineEmits(["onChooseCurrentUser", "onLoadMore"]);

//methods
const onChooseCurrentUser = (user: User): void => {
  currentUser.value = user;
  emit("onChooseCurrentUser", user);
};

const onLoadMore = (): void => {
  emit("onLoadMore");
};
</script>

<template>
  <div>
    <ul
      class="d-flex f-column w-30perc ml-20 h-600 o-auto"
      style="display: flex; flex-direction: column"
    >
      <li
        v-for="user in props.users"
        :key="user.id"
        class="c-pointer"
        :class="{ user_active: user.id === currentUser?.id }"
        @click="onChooseCurrentUser(user)"
      >
        <div class="d-flex mb-5 d-items-center">
          <div>
            <img class="w-20" :src="`../assets/${user.avatar}`" alt="avatar" />
          </div>
          <div>
            <p class="f-size-19 ml-10 c-pointer">{{ user.name }}</p>
          </div>
        </div>
      </li>
    </ul>
    <div v-if="!props.isDisabledBtnLoad" class="d-flex j-content-center">
      <button class="btn btn_load c-pointer" @click="onLoadMore">
        load more...
      </button>
    </div>
  </div>
</template>

<style scoped lang="scss">
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
.user_active {
  background-color: lightblue;
}
</style>
