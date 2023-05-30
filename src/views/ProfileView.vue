<template>
  <div class="bg">
    <div class="profile">
      <div class="avatar">
        <img src="@/assets/avator.png" alt="个人照片" />
      </div>
      <div class="info">
        <div class="field">
          <span class="label">姓名:</span>
          <span class="value">王思琴</span>
        </div>
        <div class="field">
          <span class="label">出生日期:</span>
          <span class="value">1950-01-31</span>
        </div>
        <div class="field">
          <span class="label">年龄:</span>
          <span class="value">73岁</span>
        </div>
        <div class="field">
          <span class="label">性别:</span>
          <span class="value">男</span>
        </div>
        <div class="field">
          <span class="label">联系方式:</span>
          <span class="value">13993449346</span>
        </div>
        <div class="field">
          <span class="label">家庭住址:</span>
          <span class="value"
            >甘肃省庆阳市正宁县山河镇金牛家园四号楼2单元231</span
          >
        </div>
        <div class="field">
          <span class="label">以往病历:</span>
          <span class="value">患有心脑血管疾病，帕金森综合征，行动不便</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
// TypeScript logic here
</script>

<style scoped lang="scss">
.bg {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 87vh;
  background-image: url("@/assets/bg.jpg"); /* 背景图片路径 */
  background-size: cover;
}
.profile {
  position: relative;
  background-color: #ffffff;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  text-align: center;
  width: 40%;
  margin: 0 auto;
  border: 2px solid #ccc; /* 添加此行，设置边框样式和颜色 */
  border-radius: 20px; /* 添加此行，设置圆角半径 */
}

.avatar {
  margin-top: 20px;
  width: 100px;
  height: 100px;
  border-radius: 50%;
  overflow: hidden;
  background-color: lightblue;

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
}

.info {
  margin-left: 20px;
  text-align: left;
}

.field {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  margin-bottom: 10px;
}

.label {
  font-weight: bold;
  width: 90px;
  text-align: left;
}

.value {
  margin-left: 5px;
  text-align: left;
}
</style>
