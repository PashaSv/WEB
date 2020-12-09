<template>
  <div id="app">
    <header>

      <nav class="navbar navbar-expand-md navbar-dark bg-dark">
        <a class="navbar-brand" href="#">Navbar</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span @click="show = true" class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav ml-auto">
            <li class="nav-item">
              <span @click="show = true" class="nav-link">Главная</span>
            </li>
            <li class="nav-item">
              <span @click="show = false" class="nav-link">Сотрудники</span>
            </li>
          </ul>
        </div>
      </nav>
    </header>

    <main class="container border mt-4 md-4 p-2">
        <HOME v-if="show"/>
        <WORKERS v-if="!show"/>
    </main>

    <footer class="
              bd-highlight 
              text-center border
              border-info rounded-top
              border-bottom-0
              d-sm-flex m-3
              ">
      <div class="p-2 flex-fill bd-highlight">Свобода Павел Евгеньевич </div>
      <div class="p-2 flex-fill bd-highlight">09.12.2020</div>
      <div class="p-2 flex-fill bd-highlight">
        <a href="https://bootstrap-4.ru/docs/4.5/components/alerts/" target="_blank">Bootstrap</a>
      </div>
    </footer>
  </div>
</template>

<script>
import HOME from "./components/Home"
import WORKERS from "./components/WORKERS"
export default {
  name: 'App',
  data() {
    return {
      show: true
    }
  },
  components: {
   HOME, WORKERS
  }
}
</script>

<style>
    li span {
     cursor:pointer; 
    }
</style>
