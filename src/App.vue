<template>
  <div>
    <h1>Json API</h1>
    <!-- 
    1. Tổng quan API
    2. HTTP
    3. Json-server Mock-API
    4. sử dụng phương thức fetch làm việc với API
    -->
    <ul>
      <li v-for="user in users" :key="user.id">
        {{ user.name }}
        <button @click="deleteUser(user.id)">delete</button>
      </li>
    </ul>
    <button @click="addUser">Add user</button>
    <Bt02></Bt02>
    <Bt03></Bt03>
    <Bt04></Bt04>
    <Bt05></Bt05>
    <Bt06></Bt06>
    <h1>Product</h1>
    <Bt07></Bt07>
  </div>
</template>
<script setup>
import { onMounted, ref } from "vue";
import Bt02 from "./components/Bt02.vue";
import Bt03 from "./components/Bt03.vue";
import Bt04 from "./components/Bt04.vue";
import Bt05 from "./components/Bt05.vue";
import Bt06 from "./components/Bt06.vue";
import Bt07 from "./components/bt_07_08_09_10_11/Bt07.vue";

const users = ref([]);
const getData = async () => {
  const res = await fetch("http://localhost:3000/user");
  const data = await res.json();

  users.value = data;
};

onMounted(() => {
  getData();
});

// khai baos them user
const addUser = () => {
  const newUser = {
    name: "Thu Trang",
  };

  fetch("http://localhost:3000/user", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(newUser),
  });
};

// Ham Xoa
const deleteUser = (id) => {
  fetch(`http://localhost:3000/user/${id}`, {
    method: "DELETE",
  });
  getData();
};
</script>
<style></style>
