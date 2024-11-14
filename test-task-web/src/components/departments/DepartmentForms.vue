<script setup lang="ts">
import WelcomeItem from '../WelcomeItem.vue'
import GetForm from './GetDepartment.vue'
import CreateDept from "./CreateDepartment.vue";
</script>

<template>
  <WelcomeItem>
    <template #heading>
      <div class="head">
        <h2 class="green">Отделы</h2>
      </div>
    </template>
    <template #default>

      <div class="form-wrap">
        <div class="item">
          <CreateDept/>
        </div>
<!--        <div class="item">-->
<!--          <GetForm/>-->
<!--        </div>-->
      </div>
    </template>
  </WelcomeItem>

</template>

<style>
.head{
  display: flex;
  justify-content: flex-start;
  align-items: flex-start;
  margin-top: 50px;
  margin-bottom: 15px;
}
.form-wrap{
  display: flex;
  justify-content: flex-start;
  align-items: flex-start;
}
</style>

