<script setup lang="ts">
import {ref, onMounted} from 'vue'
import axios from 'axios'

// === GET === //

interface Departments {
  text: string
}
const dept_list = ref([] as Departments[])
async function initial() {
  const response = await axios.get<Departments[]>('http://localhost:8080/api/dept?list')
  dept_list.value = response.data
}
onMounted(async () => {
  await initial()
})
</script>

<template>
  <div class="row">
    <div class="col-md-12">
      <h3 class="green">Все отделы</h3>
    </div>
    <div class="col-md-6">
      <ul class="list-group">
        <li style="list-style: none; padding-bottom: 15px;"
            v-for="(item, index) in dept_list"
            :key="index"
            class="list-group-item">
          {{ index + 1 }}. - <i>Наименование:</i> <b>{{ item.name }}</b> - <i>Примечание:</i>  {{item.description}}
        </li>
      </ul>
    </div>

  </div>

</template>

