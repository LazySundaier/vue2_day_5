<template>
  <div class="my-tag">
    <input 
    @blur="isEdit = false" v-focus 
    v-if="isEdit" class="input" 
    type="text" 
    placeholder="输入标签"
    :value="value"
    @keyup.enter="change"
    />
    <div @dblclick="edit" v-else class="text">
      {{value}}
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isEdit: false,
    }
  },
  props: {
    value: String,
  },
  methods: {
    edit() {
      this.isEdit = true
      //等dom更新完了在执行代码
      // this.$nextTick(()=>{
      //   this.$refs.inp.focus()
      // })
    },
    change(e){
      if(e.target.value.trim()===''){
        alert('请不要输入空值')
        return
      }
      this.$emit('input',e.target.value)
      this.isEdit=false
    }
  }
}
</script>

<style lang="less" scoped>
.my-tag {
  cursor: pointer;

  .input {
    appearance: none;
    outline: none;
    border: 1px solid #ccc;
    width: 100px;
    height: 40px;
    box-sizing: border-box;
    padding: 10px;
    color: #666;

    &::placeholder {
      color: #666;
    }
  }
}
</style>