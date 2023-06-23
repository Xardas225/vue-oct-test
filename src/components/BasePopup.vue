<script setup>
import BaseButton from "./BaseButton";
import BaseInput from "./BaseInput";
import { ref, defineEmits, defineProps } from "vue";

const emit = defineEmits("editUser", "showModal");

const props = defineProps({ user: Object });

const name = ref(props.user.name);
const value = ref(props.user.value);

const editUser = (user) => {
  emit("editUser", user);
  emit("showModal", false);
  name.value = "";
  value.value = "";
};
</script>

<template>
  <div class="backdrop">
    <div class="popup">
      <h1 class="text-xl pb-5">Редактирование пользователя</h1>

      <div class="popup__body">
        <BaseInput
          disabled="true"
          class="mb-5"
          type="text"
          v-model:input="name"
          label="Имя пользователя"
          placeholder="Имя пользователя"
        />
        <BaseInput
          class="mb-5"
          type="text"
          v-model:input="value"
          label="Значение пользователя"
          placeholder="Значение пользователя"
        />
      </div>

      <div class="footer">
        <BaseButton
          class="mr-5"
          btnText="Сохранить"
          @click="editUser({ name, value })"
        />
        <BaseButton btnText="Закрыть" @click="emit('showModal', false)" />
      </div>
    </div>
  </div>
</template>

<style lang="scss">
.popup {
  width: 500px;
  top: 50px;
  padding: 20px;
  left: 50%;
  transform: translateX(-50%);
  position: fixed;
  z-index: 101;
  background-color: white;
  border-radius: 10px;
}

.popup h1 {
  text-align: center;
  margin: 0;
}

.backdrop {
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.8);
  z-index: 100;
}

.footer {
  text-align: right;
}
</style>
