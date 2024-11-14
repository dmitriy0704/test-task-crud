<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import Departments from '@/components/departments/DepartmentForms.vue'
import Profession from '@/components/professions/ProfessionForms.vue'
import EmployeeForms from "@/components/employees/EmployeeForms.vue";
</script>

<template>
<!--  <header>-->
<!--&lt;!&ndash;    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />&ndash;&gt;-->
<!--    <div class="wrapper">-->
<!--      <HelloWorld msg="Test Task Web App" />-->
<!--    </div>-->
<!--  </header>-->

  <main>
    <div class="container">
      <Profession />
      <Departments />
      <EmployeeForms/>
    </div>


  </main>
</template>

<style scoped>

main{

}

main .container{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
