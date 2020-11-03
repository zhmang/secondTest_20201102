<template>
  <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
    <el-form-item label="姓名" prop="name">
      <el-input v-model="ruleForm.name"></el-input>
    </el-form-item>
    <el-form-item label="班级" prop="class">
      <el-select v-model="ruleForm.class" placeholder="请选择所属班级">
        <el-option label="17科技一班" value="keyi"></el-option>
        <el-option label="17科技二班" value="keer"></el-option>
        <el-option label="17科技三班" value="kesan"></el-option>
      </el-select>
    </el-form-item>
    <el-form-item label="入学时间" required>
      <el-col :span="11">
        <el-form-item prop="date1">
          <el-date-picker type="date" placeholder="选择日期" v-model="ruleForm.date1" style="width: 100%;"></el-date-picker>
        </el-form-item>
      </el-col>
      <el-col class="line" :span="2">-</el-col>
      <el-col :span="11">
        <el-form-item prop="date2">
          <el-time-picker placeholder="选择时间" v-model="ruleForm.date2" style="width: 100%;"></el-time-picker>
        </el-form-item>
      </el-col>
    </el-form-item>
    <el-form-item label="是否延期返校" prop="delivery">
      <el-switch v-model="ruleForm.delivery"></el-switch>
    </el-form-item>
    <el-form-item label="爱好" prop="hobby">
      <el-checkbox-group v-model="ruleForm.hobby">
        <el-checkbox label="篮球" name="type"></el-checkbox>
        <el-checkbox label="足球" name="type"></el-checkbox>
        <el-checkbox label="羽毛球" name="type"></el-checkbox>
      </el-checkbox-group>
    </el-form-item>
    <el-form-item label="性别" prop="sex">
      <el-radio-group v-model="ruleForm.sex">
        <el-radio label="男"></el-radio>
        <el-radio label="女"></el-radio>
      </el-radio-group>
    </el-form-item>
    <el-form-item label="备注" prop="desc">
      <el-input type="textarea" v-model="ruleForm.desc"></el-input>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="submitForm('ruleForm')">立即创建</el-button>
      <el-button @click="resetForm('ruleForm')">重置</el-button>
    </el-form-item>
  </el-form>
</template>

<script>
export default {
  name: 'App',
  data () {
    let validate1 = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入身份证号码'))
        // eslint-disable-next-line no-undef
      } else if (!IdCard.test(value)) {
        callback(new Error('请输入正确的身份证号码'))
      } else {
        callback()
      }
    }
    return {
      ruleForm: {
        IdCard: '',
        name: '',
        class: '',
        date1: '',
        date2: '',
        delivery: false,
        hobby: [],
        sex: '',
        desc: ''
      },

      rules: {
        IdCard: [
          {validator: validate1, trigger: 'blur'}
        ],
        name: [
          {required: true, message: '请输入姓名', trigger: 'change'}
        ],
        class: [
          {required: true, message: '请选择班级', trigger: 'change'}
        ],
        date1: [
          {type: 'date', required: true, message: '请选择日期', trigger: 'change'}
        ],
        date2: [
          {type: 'date', required: true, message: '请选择时间', trigger: 'change'}
        ],
        hobby: [
          {type: 'array', required: true, message: '请至少选择一个爱好', trigger: 'change'}
        ],
        sex: [
          {required: true, message: '请选择性别', trigger: 'change'}
        ],
        desc: [
          {required: true, message: '请输入备注', trigger: 'blur'}
        ]
      }
    }
  },
  methods: {
    submitForm (formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert('submit!')
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
    resetForm (formName) {
      this.$refs[formName].resetFields()
    }
  }
}
</script>
<style>

</style>
