<script>
import axios from 'axios'
import {ref} from 'vue'

export default {
  name: 'CreateEmployee',
  components: {},
  data() {
    return {
      prof_list: {},
      dept_list: {},
      empl_list: {},
      employee: {
        fio: '',
        description: '',
        professions: ''
      },
      isSaving: false,
    };
  },
  methods: {
    async getProfessionList() {
      const {data} = await axios.get(
          "http://localhost:8080/api/prof?list",
      );
      this.prof_list = data;
    },
    async getDepartmentList() {
      const {data} = await axios.get(
          "http://localhost:8080/api/dept?list",
      );
      this.dept_list = data;
    },

    async getEmployeeList() {
      const {data} = await axios.get(
          "http://localhost:8080/api/empl?list",
      );
      this.empl_list = data;
    },
    handleSave() {
      this.isSaving = true
      axios.post('http://localhost:8080/api/empl', this.employee)
          .then(response => {
            this.getEmployeeList()
            this.isSaving = false
            this.employee.fio = ""
            this.employee.description = ""
            this.employee.profession = ""
            this.employee.department = ""
            return response
          })
          .catch(error => {
          });
    },
  },

  beforeMount() {
    this.getProfessionList();
    this.getDepartmentList();
    this.getEmployeeList()
  },

};
</script>


<template>
  <div class="create-form-flex-container">
    <div class="flex-column">
      <div class="col-md-12">
        <h3 class="green">Создать сотрудника</h3>
      </div>
      <div class="form">

        <form>
          <div class="form-group">
            <div>
              <label htmlFor="name">ФИО</label>
            </div>
            <div>
              <input
                  v-model="employee.fio"
                  type="text"
                  class="form-control"
                  id="fio"
                  name="fio"/>
            </div>
          </div>

          <div class="form-group">
            <div> Профессия:</div>
            <select v-model="employee.profession">
              <option disabled value="">Выберете профессию</option>
              <option v-for="(item, index) in prof_list"
                      :key="index"
                      class="list-group-item">
                {{ item.name }}
              </option>
            </select>
            <input
                style="display: none"
                v-model="employee.profession"
                type="text"
                class="form-control"
                id="profession"
                name="profession"/>
          </div>
          <div class="form-group">
            <div> Отдел:</div>
            <select v-model="employee.department">
              <option disabled value="">Выберете отдел</option>
              <option v-for="(item, index) in dept_list"
                      :key="index"
                      class="list-group-item">
                {{ item.name }}
              </option>
            </select>
            <input
                style="display: none"
                v-model="employee.department"
                type="text"
                class="form-control"
                id="profession"
                name="profession"/>
          </div>
          <div class="form-group">
            <div>
              <label htmlFor="name">Примечание</label>
            </div>
            <div>

              <input
                  v-model="employee.description"
                  type="text"
                  class="form-control"
                  id="description"
                  name="description"/>
            </div>

          </div>
          <div class="form-group">
            <button
                @click="handleSave()"
                :disabled="isSaving"
                type="button"
                class="green">
              Создать
            </button>
          </div>
        </form>
      </div>
    </div>
    <div class="flex-column">
      <div class="row">
        <div class="col-md-12">
          <h3 class="green">Все сотрудники</h3>
        </div>
        <div class="col-md-6">
          <ul class="list-group">
            <li style="list-style: none; padding-bottom: 15px;"
                v-for="(item, index) in empl_list"
                :key="index"
                class="list-group-item">
              {{ index + 1 }}.

              <span class="green"><i>ФИО:</i> </span>
                      <b>{{ item.fio }}</b> <br>
              <span class="green"><i>&nbsp;&nbsp;&nbsp;&nbsp;Профессия:</i></span>
                      <b>{{item.profession }}</b><br>
              <span class="green"><i>&nbsp;&nbsp;&nbsp;&nbsp;Отдел:</i></span><b>
                      {{item.department }}</b><br>
              <span class="green"><i>&nbsp;&nbsp;&nbsp;&nbsp;Примечание:</i></span>
                      <b>{{ item.description }}</b>


            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>


</template>

