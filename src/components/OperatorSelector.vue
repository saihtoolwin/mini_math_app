<template>
    <div class="col-12 d-flex justify-content-evenly align-items-center mb-5">
      <button @click="$emit('selectOperator','+')" class="btn btn-primary btn-lg "> + <br> Additition</button>
      <button @click="$emit('selectOperator','-')" class="btn btn-primary btn-lg ">- <br> Subtraction</button>
      <button @click="$emit('selectOperator','/')" class="btn btn-primary btn-lg ">/ <br> Division</button>
      <button @click="$emit('selectOperator','*')" class="btn btn-primary btn-lg ">* <br> Multiplation</button>
    </div>
</template>

<script>
    export default {
        
    }
</script>

<style lang="scss" scoped>

</style>