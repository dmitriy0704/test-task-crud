<script setup lang="ts">
import {ref, onMounted} from 'vue'
import axios from 'axios'


interface Employees {
  text: string
}
const empl_list = ref([] as Employees[])
async function initial() {
  const response = await axios.get<Employees[]>('http://localhost:8080/api/empl?list')
  empl_list.value = response.data
}
onMounted(async () => {
  await initial()
})
</script>

<template>
  <div class="row">
    <div class="col-md-12">
      <h3 class="green">Все сотрудники</h3>
    </div>
    <div class="col-md-6">
      <ul class="list-group">
        <li style="list-style: none; padding-bottom: 15px;" v-for="(item, index) in empl_list"
            :key="index"
            class="list-group-item">
          {{ index + 1 }}.
          - <i>ФИО:</i> <b>{{ item.fio }}</b> <br>
          - <i>Профессия:</i> <b>{{ item.profession }}</b><br>
          - <i>Отдел:</i> <b>{{ item.department }}</b><br>
          - <i>Примечание:</i>  {{item.description}}
        </li>
      </ul>
    </div>
  </div>

</template>

