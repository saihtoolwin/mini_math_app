<template>
  <div class="row ">
    <h1 class="d-flex align-items-end justify-content-center">Math Quiz App</h1>
    <OperatorQuiz v-if="operator" @onBack='clearOperator' :operator="operator"/>
    <OperatorSelector v-if="!operator" @selectOperator=selectOperator />
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
import "bootstrap/dist/css/bootstrap.min.css";
import OperatorSelector from "./components/OperatorSelector.vue";
import OperatorQuiz from "./components/OperatorQuiz.vue";
export default {
  name: "App",
  data(){
    return {
      operator:null,
    }
  },
  components: {
    OperatorSelector,OperatorQuiz
  },
  methods: {
    selectOperator(operator)
    {
      this.operator=operator
      console.log(this.operator)
    },
    clearOperator()
    {
      this.operator=null
    }
  },
};
</script>

<style >
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  /* background-color:cornflowerblue; */
  width: 100%;
  height: 400px;
  margin-top: 60px;
  font-size: 80px;
  border-radius: 50px;
}
h1{
  height: 150px;
}
.row{
  border-radius: 20px;
  background-color:#6fb08c;
  width: 50%;
  height: 350px;
}
</style>
