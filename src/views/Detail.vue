<template>
  <div class="detail">
    <h2>值班详情</h2>
    <van-cell-group>
      <van-field label-align="right" label-class="labelName" label="团队" value="输入框只读" readonly />
      <van-field label-align="right" label-class="labelName" label="日期" value="输入框只读" readonly />
      <van-field label-align="right" label-class="labelName" label="星期" value="输入框只读" readonly />
      <van-field label-align="right" label-class="labelName" label="工作时间" value="输入框只读" readonly />
      <van-field label-align="right" label-class="labelName" label="姓名" value="输入框只读" readonly />
      <van-field label-align="right" label-class="labelName" label="登录名" value="输入框只读" readonly />
      <van-field label-align="right" label-class="labelName" label="办公电话" value="输入框只读" readonly />
      <van-field label-align="right" label-class="labelName" label="手机" value="输入框只读" readonly />
      <van-field label-align="right" label-class="labelName" label="值班类型" value="输入框只读" readonly />
      <van-field label-align="right" label-class="labelName" label="值班方式" value="输入框只读" readonly />
      <van-field label-align="right" label-class="labelName" label="主要职责" value="输入框只读" readonly />
      <van-field label-align="right" label-class="labelName" label="值班地点" value="输入框只读" readonly />
      <van-field label-align="right" label-class="labelName" label="值班场地" value="输入框只读" readonly />
      <van-field label-align="right" label-class="labelName" label="运维系统" value="输入框只读" readonly />
      <van-field label-align="right" label-class="labelName" label="值班角色" value="输入框只读" readonly />
      <van-field label-align="right" label-class="labelName" label="notes邮箱" value="输入框只读" readonly />
      <van-field label-align="right" label-class="labelName" label="人员备注" value="输入框只读" readonly />
      <van-field label-align="right" label-class="labelName" label="工作时间与否" value="输入框只读" readonly />
      <van-field label-align="right" label-class="labelName" label="状态" value="输入框只读" readonly />
    </van-cell-group>
  </div>
</template>
<script>
  import { CellGroup, Field} from 'vant';
  export default {
    data() {
      return {

      }
    },
    components: {
      [CellGroup.name]: CellGroup,
      [Field.name]: Field
    }
  }
</script>
<style>
  .detail {
    padding-bottom: 0.5rem;
  }
  .labelName {
    font-size: 0.4rem;
    font-weight: 800;
  }
  .van-cell:not(:last-child)::after {
    left: 0 !important;
  }
</style>