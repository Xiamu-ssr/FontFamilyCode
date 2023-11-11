<template>
  <div class="app-container">
    <el-row class="box-class">
      <el-col :span="8" align="center">
        <el-switch v-model="switch01" @change="switchChange1" inactive-text="FontWeight=Null" active-text="FontWeight=Bold"/>
      </el-col>
      <el-col :span="8" align="center">
        <el-row>
          <el-col :span="16"><el-input v-model="fontInput" placeholder="添加font-family看看效果吧"></el-input></el-col>
          <el-col :span="4"><el-button type="primary" @click="addFontFamily">添加</el-button></el-col>
          <el-col :span="4"><el-button type="primary" @click="delFontFamily" plain>重置</el-button></el-col>
        </el-row>
      </el-col>
    </el-row>
    <el-row :gutter="20" class="box-class" style="margin-top: 1vh">
      <el-col :span="8" v-for="f in fontList" style="padding: 5px" align="center">
        <el-card :style="{'font-family':f, 'font-size':'32px'}">
          <el-row>
            <el-col :span="18" :style="{'font-weight': fontBold}">
              {{ f }}
            </el-col>
            <el-col :span="6">
              <el-tooltip content="复制CSS"><el-button type="primary" @click="copyText(f)" plain><el-icon><CopyDocument /></el-icon></el-button></el-tooltip>
            </el-col>
          </el-row>
        </el-card>
      </el-col>
      <el-col :span="24" align="center">
        <el-link href="https://www.w3.org/Style/Examples/007/fonts.zh_CN.html" target="_blank"><el-card style="font-size: 32px">英文字体可参考这个CSS网站</el-card></el-link>
      </el-col>
    </el-row>
  </div>
</template>

<script setup>

import {ref} from "vue";
const switch01 = ref();
const fontBold = ref();
const fontInput = ref()
const fontListOrigin = ref([
  "黑体",
  "楷体",
  "宋体",
  "仿宋",
  "新宋体",
  "等线",
  "等线 Light",
  "方正粗黑宋简体",
  "微软雅黑",
  "微软雅黑 Light",
  "微軟正黑體",
  "微軟正黑體 Light",
  "細明體-ExtB",
  "新細明體-ExtB",
  "細明體_HKSCS-ExtB",
])
const fontList = ref([
  "黑体",
  "楷体",
  "宋体",
  "仿宋",
  "新宋体",
  "等线",
  "等线 Light",
  "方正粗黑宋简体",
  "微软雅黑",
  "微软雅黑 Light",
  "微軟正黑體",
  "微軟正黑體 Light",
  "細明體-ExtB",
  "新細明體-ExtB",
  "細明體_HKSCS-ExtB",
])

const switchChange1=(val)=>{
  if (val == true){
    console.log(val)
    fontBold.value = "bold"
  }else {
    fontBold.value = null
  }
}

const copyText=(f)=>{
  let textToCopy="font-family: "+ "\""+f+"\"";
  navigator.clipboard.writeText(textToCopy)
      .then(() => {
        console.log('复制成功');
      })
      .catch(err => {
        console.error('复制失败', err);
      });
}

const addFontFamily=()=>{
  fontList.value.push(fontInput.value)
  fontInput.value = ""
}

const delFontFamily=()=>{
  fontList.value = fontListOrigin.value
  fontInput.value = ""
}

</script>


<style scoped>
:deep(.box-class){
  padding: 20px;
  border-radius: 10px;
  box-shadow: 3px 0px 5px 3px #00000005,-3px 0px 5px 3px #00000005, 0px 3px 5px 3px #00000005,0px -3px 5px 3px #00000005;
}
:deep(.app-container ){
  margin-top: 6vh;
  margin-left: 4vw;
  margin-right: 4vw;
  margin-bottom: 8vh;
  height: 80vh;
}

</style>