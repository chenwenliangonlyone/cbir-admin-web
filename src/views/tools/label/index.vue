<template>
  <div class="app-container">
    <!--工具栏-->
    <div class="head-container">
      <eHeader :permission="permission" />
      <crudOperation :permission="permission" />
    </div>
    <!--表格渲染-->
    <el-table ref="table" v-loading="crud.loading" :data="crud.data" style="width: 100%;" @selection-change="crud.selectionChangeHandler">
      <el-table-column type="selection" width="55" />
      <el-table-column prop="id" label="标签ID" >
        <template slot-scope="scope">
          {{ scope.row.id }}
        </template>
      </el-table-column>
      <el-table-column prop="labelName" label="标签名称"/>
      <el-table-column prop="createBy" label="创建人"/>
      <el-table-column prop="createTime" label="创建日期" />
      <!--   编辑与删除   -->
      <el-table-column
        v-if="checkPer(['admin','label:edit','label:del'])"
        label="操作"
        width="130px"
        align="center"
        fixed="right"
      >
        <template slot-scope="scope">
          <udOperation
            :data="scope.row"
            :permission="permission"
          />
        </template>
      </el-table-column>
    </el-table>
    <!--分页组件-->
    <pagination />
    <!--表单渲染-->
    <eForm />
  </div>
</template>

<script>
import crudLabel from '@/api/tools/label'
import eHeader from './module/header'
import eForm from './module/form'
import CRUD, { presenter } from '@crud/crud'
import crudOperation from '@crud/CRUD.operation'
import pagination from '@crud/Pagination'
import udOperation from '@crud/UD.operation'
export default {
  name: 'Label',
  components: { eHeader, eForm, crudOperation, pagination, udOperation },
  cruds() {
    return CRUD({
      title: '标签',
      url: 'api/label',
      sort: ['id,asc'],
      crudMethod: { ...crudLabel }
    })
  },
  mixins: [presenter()],
  // 数据字典
  data() {
    return {
      permission: {
        add: ['admin', 'label:add'],
        edit: ['admin', 'label:edit'],
        del: ['admin', 'label:del']
      }
    }
  },
  methods: {
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
 ::v-deep .el-input-number .el-input__inner {
    text-align: left;
  }
</style>
