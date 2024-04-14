<template>
  <el-table :data="tableData" style="width: 100%">
    <el-table-column fixed prop="sid" label="学号" width="150"/>
    <el-table-column prop="name" label="姓名" width="120"/>
    <el-table-column prop="gender" label="性别" width="120"/>
    <el-table-column prop="age" label="年龄" width="120"/>
    <el-table-column prop="birthday" label="生日" width="120"/>
    <el-table-column fixed="right" label="操作" width="120">
      <template #default="scope">
        <el-button link type="primary" size="small" @click="handleEdit(scope.$index)">修改</el-button>
        <el-button link type="primary" size="small" @click="handleDelete(scope.$index)">删除</el-button>
      </template>
    </el-table-column>
  </el-table>
</template>


<script setup>
import {ElMessage, ElMessageBox} from 'element-plus'
import {ref, onMounted} from 'vue'
import axios from 'axios';

function handleDelete(index) {
  ElMessageBox.confirm(
      '将永久删除。是否继续？',
      '确认删除',
      {
        confirmButtonText: '确认删除',
        cancelButtonText: '取消',
        type: 'warning',
      }
  )
      .then(() => {
        let sid = tableData.value[index].sid
        axios.delete(`http://localhost:9999/hit/student/${sid}`)
            .then((res) => {
              findAll();
              ElMessage({
                type: 'success',
                message: '删除成功',
              })
            })
      })
      .catch(() => {
        ElMessage({
          type: 'info',
          message: '已取消删除',
        })
      })
}

/*
function handleDelete(index) {
  let sid = tableData.value[index].sid
  ElMessageBox.confirm(
      '是否删除学生信息？',
      'Warning',
      {
        confirmButtonText: '确定删除',
        cancelButtonText: '取消',
        type: 'warning',
      }
  )
      .then(() => {
        axios.delete(`http://localhost:9999/hit/student/${sid}`)
            .then((res) => {
              if (res.data.code === 200) {
                ElMessage.success(res.data.msg)
              }
            })
        ElMessage({
          type: 'success',
          message: `${tableData.value[index].sid}删除成功`,
        })
        tableData.value.splice(index, 1)
      })
      .catch(() => {
        ElMessage({
          type: 'info',
          message: '取消删除',
        })
      })
}
*/


function handleEdit(index) {
  ElMessage({
    type: 'info',
    message: `修改 ${tableData.value[index].sid}`,
  })
}

onMounted(() => {
  findAll();
})

function findAll() {
  axios.get('http://localhost:9999/hit/student/list')
      .then((res) => {
        tableData.value = res.data
      })
}

const tableData = ref([])
</script>

