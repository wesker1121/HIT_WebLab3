<script setup>
</script>

<template>
    <el-table :data="tableData" style="width: 100%">
      <el-table-column fixed prop="sid" label="学号" width="150" />
      <el-table-column prop="name" label="姓名" width="120" />
      <el-table-column prop="gender" label="性别" width="120" />
      <el-table-column prop="age" label="年龄" width="120" />
      <el-table-column prop="birthday" label="生日" width="120" />
      <el-table-column fixed="right" label="操作" width="120">
        <template #default="scope">
          <el-button link type="primary" size="small" @click="handleModify(scope.$index)">修改</el-button>
          <el-button link type="primary" size="small" @click="handleDelete(scope.$index)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
</template>



<script setup>
import { ElMessage, ElMessageBox } from 'element-plus'
import { ref } from 'vue'

const handleModify = (index) => {
  ElMessage({
    type: 'info',
    message: `modify ${index}`,
  })
}

const handleDelete = (index) => {
  ElMessageBox.confirm(
    'proxy will permanently delete the file. Continue?',
    'Warning',
    {
      confirmButtonText: 'OK',
      cancelButtonText: 'Cancel',
      type: 'warning',
    }
  )
    .then(() => {
      tableData.value.splice(index, 1)
      ElMessage({
        type: 'success',
        message: 'Delete completed',
      })
    })
    .catch(() => {
      ElMessage({
        type: 'info',
        message: 'Delete canceled',
      })
    })
}


const tableData = ref([
  {
    sid: '2016-05-02',
    name: 'alcice',
    gender:'f',
    age: '20',
    birthday: '1996-05-02',
  },
  {
    sid: '2016-05-02',
    name: 'bb',
    gender:'f',
    age: '20',
    birthday: '1996-05-02',
  },
  {
    sid: '2016-05-02',
    name: 'cc',
    gender:'f',
    age: '20',
    birthday: '1996-05-02',
  },
  {
    sid: '2016-05-02',
    name: 'dd',
    gender:'f',
    age: '20',
    birthday: '1996-05-02',
  },
  {
    sid: '2016-05-02',
    name: 'ee',
    gender:'f',
    age: '20',
    birthday: '1996-05-02',
  },
  {
    sid: '2017-05-02',
    name: 'ff',
    gender:'f',
    age: '20',
    birthday: '1996-05-02',
  },
])
</script>

