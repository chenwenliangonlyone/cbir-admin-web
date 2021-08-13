<template>
  <el-dialog
    append-to-body
    :close-on-click-modal="false"
    :before-close="crud.cancelCU"
    :visible="crud.status.cu > 0"
    :title="crud.status.title"
    width="500px"
  >
    <el-form
      ref="form"
      :model="form"
      :rules="rules"
      size="small"
      label-width="80px"
    >
      <el-form-item
        label="标签名称"
        prop="labelName"
      >
        <el-input
          v-model="form.labelName"
          style="width: 370px;"
        />
      </el-form-item>
    </el-form>
    <div
      slot="footer"
      class="dialog-footer"
    >
      <el-button
        type="text"
        @click="crud.cancelCU"
      >
        取消
      </el-button>
      <el-button
        :loading="crud.status.cu === 2"
        type="primary"
        @click="crud.submitCU"
      >
        确认
      </el-button>
    </div>
  </el-dialog>
</template>

<script>
import { form } from '@crud/crud'

const defaultForm = {
  // labelId: '',
  labelName: ''
}
export default {
  mixins: [form(defaultForm)],
  data() {
    return {
      rules: {
        // labelId: [
        //   { required: true, message: '请输入标签ID', trigger: 'blur', type: 'number' }
        // ],
        labelName: [
          { required: true, message: '请输入标签名称', trigger: 'blur' }
        ]
      }
    }
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
 ::v-deep .el-input-number .el-input__inner {
    text-align: left;
  }
</style>
