<template>
  <div style="display: flex; align-items:center; justify-content: center;">
    <div class="block">
      <span class="demonstration">默认</span>
      <el-date-picker v-model="value1" type="monthrange" :align="align" range-separator="至" start-placeholder="开始月份"
        end-placeholder="结束月份">
      </el-date-picker>
    </div>
    <div class="block">
      <span class="demonstration">带快捷选项</span>
      <el-date-picker v-model="value2" type="monthrange" align="center" unlink-panels range-separator="至"
        start-placeholder="开始月份" end-placeholder="结束月份" :picker-options="pickerOptions">
      </el-date-picker>
    </div>

    <button style="position: fixed; bottom: 0px;" @click="change">change</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      align: '',
      aligns: ['left', 'center', 'right'],
      idx: 0,
      pickerOptions: {
        shortcuts: [{
          text: '本月',
          onClick(picker) {
            picker.$emit('pick', [new Date(), new Date()]);
          }
        }, {
          text: '今年至今',
          onClick(picker) {
            const end = new Date();
            const start = new Date(new Date().getFullYear(), 0);
            picker.$emit('pick', [start, end]);
          }
        }, {
          text: '最近六个月',
          onClick(picker) {
            const end = new Date();
            const start = new Date();
            start.setMonth(start.getMonth() - 6);
            picker.$emit('pick', [start, end]);
          }
        }]
      },
      value1: '',
      value2: ''
    };
  },
  methods: {
    change() {
      this.align = this.aligns[this.idx++ % 3]
      console.log(this.align);
    }
  }
};
</script>
