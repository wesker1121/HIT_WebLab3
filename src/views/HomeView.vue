<template>
  <el-table :data="tableData" style="width: 100%">
    <el-table-column fixed prop="sid" label="学号" width="150"/>
    <el-table-column prop="name" label="姓名" width="120"/>
    <el-table-column prop="gender" label="性别" width="120"/>
    <el-table-column prop="age" label="年龄" width="120"/>
    <el-table-column prop="birthday" label="生日" width="120"/>
    <el-table-column fixed="right" label="操作" width="120">
      <template #default="scope">
        <el-button link type="primary" size="small" @click="handleModify(scope.$index)">修改</el-button>
        <el-button link type="primary" size="small" @click="handleDelete(scope.$index)">删除</el-button>
      </template>
    </el-table-column>
  </el-table>
</template>


<script setup>
import {ElMessage, ElMessageBox} from 'element-plus'
import {ref} from 'vue'

const handleModify = (index) => {
  ElMessage({
    type: 'info',
    message: `修改 ${tableData.value[index].sid}`,
  })
}

const handleDelete = (index) => {
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
        console.log(tableData.value[index]);
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


const tableData = ref([
  {
    sid: '111',
    name: 'alice',
    gender: 'f',
    age: '20',
    birthday: '1996-05-02',
  },
  {
    sid: '222',
    name: 'bb',
    gender: 'f',
    age: '20',
    birthday: '1996-05-02',
  },
  {
    sid: '333',
    name: 'cc',
    gender: 'f',
    age: '20',
    birthday: '1996-05-02',
  },
  {
    sid: '444',
    name: 'dd',
    gender: 'f',
    age: '20',
    birthday: '1996-05-02',
  },
  {
    sid: '555',
    name: 'ee',
    gender: 'f',
    age: '20',
    birthday: '1996-05-02',
  },
  {
    sid: '666',
    name: 'ff',
    gender: 'f',
    age: '20',
    birthday: '1996-05-02',
  },
])
</script>

