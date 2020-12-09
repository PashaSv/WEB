<template>
    <div>
        <h1>Сотрудники</h1>
        <form @click.prevent>
  <div class="form-group">
    <label for="name">Имя</label>
    <input v-model="name" placeholder="Name..." type="text" class="form-control" id="name">
  </div>
  <div class="form-group">
    <label for="surname">Фамилия</label>
    <input v-model="surname" placeholder="Surname..." type="text" class="form-control" id="surname">
  </div>
  <div class="form-group">
    <label for="patronymic">Отчество</label>
    <input v-model="patronymic" placeholder="Patronymic..." type="text" class="form-control" id="patronymic">
  </div>
  <div class="form-group">
    <label for="status">Отдел</label>
    <select id="inputState" class="form-control" v-model="status">
        <option value="">Choose...</option>
        <option v-for="item in org" :key="item.id" :value="item.id">{{item.name}}</option>
    </select>
  </div>
  <button @click="showChange()" class="btn btn-primary">Выбрать карточку</button>
</form>
        <div class="cards text-center">
            <div 
                class="card d-inline-block m-2" 
                style="width: auto;"
                v-for="worker in WORKERS"
                 :key="worker.id"
                >

                <img src="../assets/logo.png" class="card-img-top" alt="...">
                <div class="card-body">
                    <h5 class="card-title">{{worker.name}} {{worker.surname}} {{worker.patronymic}}</h5>
                    <p class="card-text">{{worker.status}}.</p>
                </div>
                <div class="d-sm-inline-flex justify-content-center m-2">
                    <button @click="onChange(worker.id)" v-if="change" class="btn btn-warning mr-2">Изменить</button>
                    <button @click="onDelete(worker.id)" class="btn btn-danger ml-2">Удалить</button>
                </div>
            </div>
            
        </div>
    </div>
</template>

<script>
import axios from "axios";
    export default {
      data() {
          return {
              change: false,
              WORKERS: [],
              org: [],

              name: '',
              surname: '',
              patronymic: '',
              status: '',
          }
      },
      mounted () {
          this.mount()
          axios.get('http://localhost:4667/org')
                .then(res => this.org = res.data)
      },
      methods: {
          onDelete(id){
              axios.delete('http://localhost:4667/WORKERS/' + id)
              .then(() => this.mount())
          },
          showChange() {
              this.change=!this.change
          },
          onChange(id){
              let newWorker = this.WORKERS[id-1]

              if (this.name.length > 0) {
                  newWorker.name = this.name
              }
               if (this.surname.length > 0) {
                  newWorker.surname = this.surname
              }
              if (this.patronymic.length > 0) {
                  newWorker.patronymic = this.patronymic
              }
              if (this.status !== -null) {
                  newWorker.status = this.status
              }   
              
          },
          mount() {
              axios.get('http://localhost:4667/WORKERS')
                .then(res => this.WORKERS = res.data)
          }
      }  
    }
</script>

<style scoped>
@media screen and (max-width: 450px) {
    h1, h2, h3, h4, h5, h6 {
        font-size: 12px;
    }
    .h1, .h2, .h3, .h4,.h5, .h6 {
        font-size: 12px;
    }
}
</style>