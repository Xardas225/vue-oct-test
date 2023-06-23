<script setup>
import { ref } from "vue";
import { useUsersStore } from "@/store";
import BaseButton from "./components/BaseButton.vue";
import BasePopup from "./components/BasePopup.vue";

const store = useUsersStore();
const users = store.getUsers;

const showModal = ref(false);

const editUser = (user) => {
  store.editUserByName(user);
};

const currentUser = ref(null);

const togglePopup = (user) => {
  currentUser.value = user;
  showModal.value = true;
};
</script>

<template>
  <div class="container max-w-4xl mx-auto px-6">
    <div class="text-gray-900 text-xl">Users</div>
    <div class="bg-green-500 w-full h-1"></div>

    <div class="mx-auto mt-6">
      <div class="my-4 flex">
        <div class="w-1/3 py-2 text-lg font-bold">User Name</div>
        <div class="w-1/3 py-2 text-lg font-bold">User Value</div>
        <div class="w-1/3 py-2 text-lg font-bold">Editing</div>
      </div>
      <template v-for="user in users" :key="user.name">
        <div class="my-4 flex flex-wrap justify-between">
          <div class="w-1/3 py-2 text-lg">{{ user.name }}</div>
          <div class="w-1/3 py-2 text-lg">{{ user.value }}</div>
          <BaseButton
            class="w-1/3"
            btnText="Редактировать"
            @click="togglePopup(user)"
          />
        </div>
      </template>
    </div>

    <BasePopup
      :user="currentUser"
      v-if="showModal"
      @showModal="showModal = false"
      @editUser="editUser"
    />
  </div>
</template>

<style lang="scss"></style>
