<script setup lang="ts">
import { PropType, ref, watch, defineProps, defineEmits } from "vue";

import User from "../types/user";
import USER_FIELDS from "../constant/userFields";

//props
const props = defineProps({
  user: {
    type: Object as PropType<User>,
    required: true,
    default: null,
  },
});

//emits
const emit = defineEmits(["onCloseInfo"]);

//data
const currentUser = ref<User>(props.user);

//methods
const onCloseInfo = (): void => {
  emit("onCloseInfo");
};

//watch
watch(props.user, (newUser) => {
  currentUser.value = newUser;
});
</script>

<template>
  <div class="mt-16 w-70perc">
    <div class="b-blue pl-40 pt-5 pb-5">
      <input
        class="b-inherit user_name"
        type="text"
        v-model="currentUser.name"
        placeholder="Не указано"
      />
    </div>
    <div class="d-flex mt-16 ml-40">
      <div class="p-relative">
        <img
          class="w-75 mr-15"
          :src="`../assets/${currentUser.avatar}`"
          alt="avatar"
        />
        <div
          class="circle"
          :class="currentUser.active ? 'circle_active' : 'circle_inactive'"
        ></div>
      </div>
      <div>
        <div class="d-flex">
          <div class="w-100">
            <label for="post">{{ USER_FIELDS.post }}</label>
          </div>
          <div>
            <input
              class="border-gray"
              v-model="currentUser.post"
              name="post"
              type="text"
              placeholder="Не указано"
            />
          </div>
        </div>
        <div class="d-flex">
          <div class="w-100">
            <label for="department">{{ USER_FIELDS.department }}</label>
          </div>
          <div>
            <input
              class="border-gray"
              v-model="currentUser.department"
              name="department"
              type="text"
              placeholder="Не указано"
            />
          </div>
        </div>
        <div class="d-flex">
          <div class="w-100">
            <label for="company">{{ USER_FIELDS.company }}</label>
          </div>
          <div>
            <input
              class="border-gray"
              v-model="currentUser.company"
              name="company"
              type="text"
              placeholder="Не указано"
            />
          </div>
        </div>
      </div>
      <div class="d-flex d-items-end ml-20">
        <button class="btn btn_close c-pointer" @click="onCloseInfo">
          Close
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.circle {
  position: absolute;
  top: 60px;
  border-radius: 50%;
  width: 15px;
  height: 15px;

  &_active {
    background-color: lightgreen;
  }

  &_inactive {
    background-color: lightcoral;
  }
}

.border-gray {
  border: 1px lightgray solid;
}
.b-blue {
  background-color: lightblue;
}

.user_name {
  border: #0394c2d6 2px solid;
  border-radius: 3px;
}
</style>
