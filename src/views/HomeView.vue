<template>
  <div class="elderly-info">
    <h2>已发布服务信息列表</h2>
    <div class="sort-button">
      <label>时间排序顺序：</label>
      <select v-model="sortOrder">
        <option value="asc">升序</option>
        <option value="desc">降序</option>
      </select>
    </div>
    <table>
      <thead>
        <tr>
          <th>姓名</th>
          <th>服务地址</th>
          <th>具体服务地址</th>
          <th>服务类型</th>
          <th>服务详细描述</th>
          <th
            @click="sortByStartTime"
            :class="{ active: sortKey === 'startTime' }"
          >
            服务开始时间
          </th>
          <th>服务结束时间</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(elderly, index) in sortedElderlyList" :key="index">
          <td>{{ elderly.name }}</td>
          <td>{{ elderly.serviceAddress.join(' ') }}</td>
          <td>{{ elderly.specificAddress }}</td>
          <td>{{ elderly.serviceType }}</td>
          <td>{{ elderly.serviceDescription }}</td>
          <td
            :class="{
              'sorted-asc': sortKey === 'startTime' && sortOrder === 'asc',
              'sorted-desc': sortKey === 'startTime' && sortOrder === 'desc',
            }"
          >
            {{ elderly.startTime }}
          </td>
          <td>{{ elderly.endTime }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, watch, computed } from "vue";

interface Elderly {
  name: string;
  serviceAddress: string[];
  specificAddress: string;
  serviceType: string;
  serviceDescription: string;
  startTime: string;
  endTime: string;
}

const elderlyList = ref<Array<Elderly>>([]);
const sortKey = ref("startTime");
const sortOrder = ref("asc");
elderlyList.value = JSON.parse(localStorage.getItem("elder") || "[]");
window.addEventListener("elder", () => {
  elderlyList.value = JSON.parse(localStorage.getItem("elder") || "[]");
  console.log(elderlyList.value);
});
  console.log(elderlyList.value);


// const sortedElderlyList = ref<Array<Elderly>>([]);
const sortedElderlyList = computed(()=>{
  const arr = elderlyList.value.slice().sort((a, b) => {
    const dateA = new Date(a.startTime);
    const dateB = new Date(b.startTime);

    if (sortOrder.value === "asc") {
      return dateA.getTime() - dateB.getTime();
    } else if (sortOrder.value === "desc") {
      return dateB.getTime() - dateA.getTime();
    } else {
      return 0;
    }
  });
  return arr
})


function sortByStartTime() {
  sortKey.value = "startTime";
}
</script>

<style scoped lang="scss">
.elderly-info {
  /* Add your styles here */
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

thead th {
  background-color: #f0f0f0;
  padding: 10px;
  text-align: center;
  cursor: pointer;
}

thead th.active {
  font-weight: bold;
}

tbody td {
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

.sorted-asc::after {
  content: " ↑";
}

.sorted-desc::after {
  content: " ↓";
}

.sort-button {
  margin-bottom: 10px;
}
</style>
