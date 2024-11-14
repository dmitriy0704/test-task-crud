<script>
import axios from 'axios'

export default {
  name: 'CreateDepartment',
  components: {},
  data() {
    return {
      dept_list: {},
      dept: {
        name: '',
        description: ''
      },
      isSaving: false,
    };
  },
  methods: {
    async getDepartmentList() {
      const {data} = await axios.get(
          "http://localhost:8080/api/dept?list",
      );
      this.dept_list = data;
    },
    handleSave() {
      this.isSaving = true
      axios.post('http://localhost:8080/api/dept', this.dept)
          .then(response => {
            this.getDepartmentList();
            this.isSaving = false
            this.dept.name = ""
            this.dept.description = ""
            return response
          })
          .catch(error => {
          });
    },
  },
  beforeMount() {
    this.getDepartmentList();
  },
};
</script>

<template>

  <div class="create-form-flex-container">
    <div class="flex-column">
      <div class="col-md-12">
        <h3 class="green">Создание отдела</h3>
      </div>
      <form>
        <div class="form-group">
          <div>
            <label htmlFor="name">Наименование</label>
          </div>
          <div>
            <input
                v-model="dept.name"
                type="text"
                class="form-control"
                id="name"
                name="name"/>
          </div>

        </div>

        <div class="form-group">
          <div>
            <label htmlFor="name">Примечание</label>
          </div>
          <div>
            <input
                v-model="dept.description"
                type="text"
                class="form-control"
                id="description"
                name="description"/>
          </div>


        </div>
        <button
            @click="handleSave()"
            :disabled="isSaving"
            type="button"
            class="green">
          Создать
        </button>
      </form>


    </div>
    <div class="flex-column">
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
              <span class="green">{{ index + 1 }}</span>.

              <span class="green"><i>Наименование:</i></span>   <span style="color: #2c3e50"><b>{{ item.name }}</b></span>     <br>

              <span class="green"> <i>&nbsp;&nbsp;&nbsp;&nbsp;Примечание:</i> </span>   <span style="color: #2c3e50"><b> {{ item.description }} </b></span>
            </li>
          </ul>
        </div>

      </div>

    </div>
  </div>


</template>