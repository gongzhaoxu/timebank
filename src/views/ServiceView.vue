<template>
  <div class="form-container">
    <div class="form-wrapper">
      <el-form ref="form" :model="formData" label-width="100px">
        <el-form-item label="服务地址">
          <el-cascader
            v-model="formData.serviceAddress"
            :options="addressOptions"
          ></el-cascader>
        </el-form-item>
        <el-form-item label="具体服务地址">
          <el-input v-model="formData.specificAddress"></el-input>
        </el-form-item>
        <el-form-item label="服务类型">
          <el-select
            v-model="formData.serviceType"
            placeholder="请选择服务类型"
          >
            <el-option label="陪同就医" value="陪同就医"></el-option>
            <el-option label="房屋清洁" value="房屋清洁"></el-option>
            <el-option label="聊天" value="聊天"></el-option>
            <el-option label="康复服务" value="康复服务"></el-option>
            <el-option label="紧急救援" value="紧急救援"></el-option>
            <el-option label="其他" value="其他"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="服务详细描述">
          <el-input
            v-model="formData.serviceDescription"
            type="textarea"
          ></el-input>
        </el-form-item>
        <el-form-item label="服务开始时间">
          <el-date-picker
            v-model="formattedStartTime"
            type="datetime"
            :value-format="dateTimeFormat"
            :picker-options="pickerOptions"
          ></el-date-picker>
        </el-form-item>
        <el-form-item label="服务结束时间">
          <el-date-picker
            v-model="formattedEndTime"
            type="datetime"
            :value-format="dateTimeFormat"
            :picker-options="pickerOptions"
          ></el-date-picker>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="submitForm">提交</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineComponent ,ref, reactive, getCurrentInstance, onMounted, toRefs,h} from "vue";
import { EluiChinaAreaDht } from 'elui-china-area-dht'
import {
  ElForm,
  ElFormItem,
  ElCascader,
  ElInput,
  ElSelect,
  ElOption,
  ElTimePicker,
  ElButton,
  ElMessage,
} from "element-plus";
import dayjs from "dayjs";

const dateTimeFormat = "YYYY-MM-DD HH:mm";

const formData = reactive({
  name:"王思琴",
  serviceAddress: [],
  specificAddress: "",
  serviceType: "房屋清洁",
  serviceDescription: "",
  startTime: null as string | null,
  endTime: null as string | null,
});

const addressOptions = ref([
  {
    value: "北京",
    label: "北京",
    children: [
      {
        value: "海淀区",
        label: "海淀区",
        children: [
          {
            value: "中关村",
            label: "中关村",
          },
          {
            value: "五道口",
            label: "五道口",
          },
        ],
      },
      {
        value: "东城区",
        label: "东城区",
        children: [
          {
            value: "天安门",
            label: "天安门",
          },
        ],
      },
    ],
  },
  // Add more location options here
]);

const pickerOptions = ref({
  start: "09:00",
  step: "01:00",
  end: "18:00",
});

const { startTime, endTime } = toRefs(formData);
const formattedStartTime = ref(
  startTime.value ? dayjs(startTime.value).format(dateTimeFormat) : null
);
const formattedEndTime = ref(
  endTime.value ? dayjs(endTime.value).format(dateTimeFormat) : null
);

// 提交表单
function submitForm() {


  const formattedFormData = {
    ...formData,
    startTime: formattedStartTime.value,
    endTime: formattedEndTime.value,
  };

  const formDataJson = JSON.stringify(formattedFormData);
  console.log(formDataJson);

  
  const arr:Array<any> = JSON.parse(localStorage.getItem("elder") || "[]");
  arr.push(formattedFormData)
  localStorage.setItem('elder', JSON.stringify(arr))

  ElMessage({
    showClose: true,
    message:'提交成功',
    type: 'success',
  })
}
</script>

<style scoped lang="scss">
.form-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 88vh;
  background-image: url("@/assets/bg1.jpg"); /* 背景图片路径 */
  background-size: cover;
}

.form-wrapper {
  width: 400px;
}
.el-form {
  width: 400px;
  color: #000000; /* 字体颜色设置为纯黑色 */
  background-color: #ffffff; /* 表单背景色设置为白色 */
  border: 1px solid #000000; /* 增加黑色边框 */
  border-radius: 20px;
  padding: 20px; /* 添加 padding */
  .el-form-item__label {
    width: 100px;
    color: #000000; /* 字体颜色设置为纯黑色 */
  }

  .el-input {
    width: 100%;
    color: #000000; /* 字体颜色设置为纯黑色 */
  }

  .el-cascader {
    width: 100%;
    color: #000000; /* 字体颜色设置为纯黑色 */
  }

  .el-select {
    width: 100%;
    color: #000000; /* 字体颜色设置为纯黑色 */
  }

  .el-time-picker {
    width: 100%;
    color: #000000; /* 字体颜色设置为纯黑色 */
  }

  .el-button {
    margin-top: 20px;
    color: #000000; /* 字体颜色设置为纯黑色 */
  }
}
</style>
