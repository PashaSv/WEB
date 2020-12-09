<template>
    <div>
         <h1>Главная</h1>
        <form @submit="onSave()">
  <div class="form-group">
    <label for="name">Имя</label>
    <input v-model="name" placeholder="Name..." type="text" class="form-control" id="name" required>
  </div>
  <div class="form-group">
    <label for="surname">Фамилия</label>
    <input v-model="surname" placeholder="Surname..." type="text" class="form-control" id="surname" required>
  </div>
  <div class="form-group">
    <label for="patronymic">Отчество</label>
    <input v-model="patronymic" placeholder="Patronymic..." type="text" class="form-control" id="patronymic" required>
  </div>
  <div class="form-group">
    <label for="status">Отдел</label>
    <select id="inputState" class="form-control" v-model="status">
        <option value="">Choose...</option>
        <option v-for="item in org" :key="item.id" :value="item.id">{{item.name}}</option>
    </select>
  </div>
  <button class="btn btn-success">Сохранить</button>
</form>
    </div>
</template>

<script>
import axios from "axios";
    export default {
       data() {
           return {
                name: '',
              surname: '',
              patronymic: '',
              status: "",

              org: []
           }
       }, 
       methods: {
           onSave() {
               let worker = {
                   name: this.name,
                   surname: this.surname,
                   patronymic: this.patronymic,
                   status: this.status
               }
             axios.post('http://localhost:4667/WORKERS', worker)
             .then(() => alert('Сотрудник добавлен'))  
            },
       },
       mounted () {
           axios.get('http://localhost:4667/org')
             .then(res => this.org = res.data);
       },
    }
</script>

<style scoped>

</style>