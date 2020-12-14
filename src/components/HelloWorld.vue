<template>
  <div class="hello">
    
    <template>
      <h2>调用云函数</h2>
      <p>
        点击
        <a href="javascript:;" @click="callFunction">调用 hello world 云函数</a>
      </p>
      <p>
        <b>云函数执行结果</b>
      </p>
      <p>{{ callFunctionResult }}</p>
    </template>

  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      envId: "",
      callFunctionResult: "",
    };
  },
  props: {
    msg: String,
  },
  methods: {
    async callFunction() {
      try {
        const res = await this.$cloudbase.callFunction({
          name: "vue-echo",
          data: {
            foo: "bar",
          },
        });
        this.callFunctionResult = res;
      } catch (e) {
        console.error(e)
        this.callFunctionResult = e.message;
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h3 {
    margin: 40px 0 0;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  a {
    color: #42b983;
  }

  .hello {
    max-width: 500px;
    margin: 0 auto;
    word-break: break-all;
  }
</style>
