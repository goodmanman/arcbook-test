<template>
  <div id="app">
    <div class="container">
      <div class="title">Profile 信息</div>
      <div class="line">
        <div class="label">用户名:</div>
        <div class="item">
          <input v-if="isEdit" class="input" type="text" v-model="info.name" />
          <span v-else class="text">{{ info.name }}</span>
        </div>
      </div>
      <div class="line">
        <div class="label">邮箱:</div>
        <div class="item">
          <input v-if="isEdit" class="input" type="text" v-model="info.email" />
          <span v-else class="text">{{ info.email }}</span>
        </div>
      </div>
      <div class="line">
        <div class="label">手机号:</div>
        <div class="item">
          <input v-if="isEdit" class="input" type="text" v-model="info.phone" />
          <span v-else class="text">{{ info.email }}</span>
        </div>
      </div>
      <div class="option">
        <div class="btn" @click="handleEdit">{{ isEdit ? '保存' : '编辑' }}</div>
        <div class="btn" v-if="isEdit" @click="handleCancel">取消</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      isEdit: false,
      info: {
        name: '',
        email: '',
        phone: '',
      },
      copyInfo: {},
    };
  },
  mounted() {
    const info = localStorage.getItem('arc_info');
    if (!info) {
      return;
    }
    this.info = JSON.parse(info);
  },
  methods: {
    handleEdit() {
      this.copyInfo = JSON.parse(JSON.stringify(this.info));
      if (!this.isEdit) {
        this.isEdit = true;
        return;
      }
      console.log(this.copyInfo, 'this.copyInfo');
      localStorage.setItem('arc_info', JSON.stringify(this.info));
      this.isEdit = false;
    },
    handleCancel() {
      this.isEdit = false;
      console.log(this.copyInfo, '333');
      this.info = JSON.parse(JSON.stringify(this.copyInfo));
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 1rem;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.container {
  width: 100%;
}
.title {
  margin-bottom: 0.2rem;
  font-size: 0.3rem;
  font-weight: bolder;
}
.option {
  display: flex;
  justify-content: flex-end;
  margin: 0.2rem;
}
.btn {
  width: 0.8rem;
  height: 0.4rem;
  line-height: 0.4rem;
  font-size: 0.15rem;
  background: #377cea;
  border-radius: 4px;
  color: #fff;
  font-family: Inter;
  text-align: center;
  font-style: normal;
  font-weight: 400;
  margin-left: 0.15rem;
  cursor: pointer;
}
.cancel {
  cursor: pointer;
}
.line {
  width: 100%;
  height: 0.5rem;
  margin-bottom: 0.2rem;
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.label {
  width: 1rem;
  height: 0.5rem;
  font-size: 0.2rem;
  line-height: 0.5rem;
  margin-right: 0.08rem;
  text-align: right;
}
.item {
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.input {
  height: 0.5rem;
  font-size: 0.2rem;
  padding-left: 0.1rem;
  border: 1px solid #c9c9c9;
  border-radius: 4px;
}
.text {
  display: inline-block;
  font-size: 0.2rem;
  height: 0.5rem;
  line-height: 0.5rem;
}
</style>
