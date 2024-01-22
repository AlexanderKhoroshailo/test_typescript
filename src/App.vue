<script setup lang="ts">
import { ref, computed } from "vue";

import UsersList from "./components/UsersList.vue";
import UserInfo from "./components/UserInfo.vue";

import usersData from "./data/users.json";
import User from "./types/user";

//data
let counts = 25;
const length: number = usersData.length;

const users = ref<User[]>(usersData.slice(0, counts));
const user = ref<User | null>(null);
const showInfo = ref<boolean>(false);
const isDisabledBtnLoad = ref<boolean>(false);

//methods
const onChooseCurrentUser = (userEmit: User): void => {
  user.value = userEmit;
  showInfo.value = true;
};

const onCloseInfo = (): void => {
  showInfo.value = false;
};

const onLoadMore = (): void => {
  if (counts < length) {
    counts += 25;
    users.value = usersData.slice(0, counts);
  } else {
    isDisabledBtnLoad.value = true;
  }
};

//computed
const currentUser = computed(() => {
  return user;
});
</script>

<template>
  <div class="d-flex">
    <UsersList
      v-if="users"
      :users="users"
      :showInfo="showInfo"
      :isDisabledBtnLoad="isDisabledBtnLoad"
      @onChooseCurrentUser="onChooseCurrentUser"
      @onLoadMore="onLoadMore"
    />
    <div v-else class="ml-20">
      <h2>No have Users</h2>
    </div>
    <UserInfo v-if="showInfo" :user="currentUser" @onCloseInfo="onCloseInfo" />
    <div v-else class="ml-20">
      <h2>Please choose User</h2>
    </div>
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
}
p {
  margin: 0;
}

label {
  color: grey;
}

.d-flex {
  display: flex;
}

.j-content-center {
  justify-content: center;
}

.d-items-center {
  align-items: center;
}

.d-items-end {
  align-items: end;
}

.b-inherit {
  background-color: inherit;
}

.f-column {
  flex-direction: column;
}

.p-relative {
  position: relative;
}

.btn {
  border-radius: 3px;
  color: whitesmoke;
  &_close {
    background-color: lightcoral;
    border: lightcoral 1px solid;
  }
  &_load {
    background-color: lightsteelblue;
    border: lightsteelblue 1px solid;
  }
}

.c-pointer {
  cursor: pointer;
  &:hover {
    opacity: 0.8;
  }
}

.w-20 {
  width: 20px;
}

.w-75 {
  width: 75px;
}

.w-100 {
  width: 100px;
}

.w-30perc {
  min-width: 30%;
}

.w-70perc {
  width: 70%;
}

.h-600 {
  height: 600px;
}
.o-auto {
  overflow: auto;
}

.f-size-19 {
  font-size: 19px;
}

.mb-5 {
  margin-bottom: 5px;
}

.ml-10 {
  margin-left: 10px;
}

.ml-20 {
  margin-left: 20px;
}

.ml-40 {
  margin-left: 40px;
}

.mr-15 {
  margin-right: 15px;
}

.mt-16 {
  margin-top: 16px;
}

.pl-40 {
  padding-left: 40px;
}

.pt-5 {
  padding-top: 5px;
}

.pb-5 {
  padding-bottom: 5px;
}
</style>
