
<template>
  <button @click="fetchData">获取数据</button>
  <div id="data" v-if="data">
    {{ data }}
  </div>
</template>

<script>
import { ref } from "vue";
import axios from "axios";
export default {
  setup() {
    let data = ref("data from server...");
    function renderData(response) {
      data.value = response.data;
    }
    function fetchData() {
      // 使用Axios发送GET请求
      axios
        .get("http://localhost:8080/askForData")
        .then((response) => renderData(response))
        .catch((error) => {
          console.error("Error fetching data:", error);
        });
    }
    return {
      data,
      fetchData,
    };
  },
};
</script>

<style scoped>
button {
  background-color: #007bff;
  color: #fff;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  font-size: 16px;
  border-radius: 5px;
}

button:hover {
  background-color: #0056b3;
}

#data {
  margin: 20px;
  padding: 20px;
  background-color: #f0f0f0;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 18px;
}
</style> 