<script setup lang="ts">
import {ref, onMounted} from 'vue'
import axios from 'axios'

// === GET === //

interface Professions {
  text: string
}
const prof_list = ref([] as Professions[])

async function intial() {
  const response = await axios.get<Professions[]>('http://localhost:8080/api/prof?list')
  prof_list.value = response.data
}
onMounted(async () => {
  await intial()
})



</script>

<template>
  <div class="row">
    <div class="col-md-12">
      <h3 class="green">Все Профессии</h3>
    </div>
    <div class="col-md-6">
      <ul class="list-group">
        <li style="list-style: none;  padding-bottom: 15px;"
            v-for="(item, index) in prof_list"
            :key="index"
            class="list-group-item">
          {{ index + 1 }}.
          - <i>Наименование:</i> <b>{{ item.name }}</b>
          - <i>Примечание:</i>  {{item.description}}
        </li>
      </ul>
    </div>
  </div>

</template>

