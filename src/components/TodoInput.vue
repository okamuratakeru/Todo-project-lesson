<template>
  <div>
    <p v-if="isErrMsg">入力してください</p>
  </div>
  <div>
    <form @submit.prevent="onSubmitForm">
      <label>やること<input type="text" v-model="input"/></label>
      <label>期限<input type="date" v-model="inputDate" /></label>
      <input type="submit" value="登録！">
      
    </form>
  </div>
</template>

<script setup>
import {ref} from "vue";
import {statuses} from "../const/statuses.js";

const input = ref("");
const inputDate = ref("");

const isErrMsg = ref(false);

function onSubmitForm() {
  console.log(input.value)
  if (input.value == "" || inputDate.value == "") {
    isErrMsg.value = true
    return;
  }

  const items = JSON.parse(localStorage.getItem("items")) || [];

  const newItem = {
    id: items.length,
    content: input.value,
    limit: inputDate.value,
    state: statuses.NOT_START,
    onEdit: false
  };

  items.push(newItem);

  localStorage.setItem("items", JSON.stringify(items));

  location.reload();
}



</script>
