<template>
  <div id="app">
    <div class="container">
      <div>
        <h1>{{title}}</h1>
      </div>
      <div class="row">
        <div class="form-group w-100">
          <label for="name">Имя</label>
          <input type="text" class="form-control" id="name" v-model="name">
        </div>
        <div class="form-group w-100">
          <label for="surname">Фамилия</label>
          <input type="text" class="form-control" id="surname" v-model="surname">
        </div>
        <div class="form-group w-100">
          <label for="phone">Номер</label>
          <input type="text" class="form-control" id="phone" v-model="phone">
        </div>
        <div class="form-group w-100">
          <div class="btn btn-success" @click="onSave()">Сохранить</div>
        </div>
        <div class="form-group w-100">
          <div class="btn btn-success" @click="onLoad()">Получить</div>
        </div>
        <div class="Row" v-for="note in notes" :key="note.id">
            <div class="col-4">{{note.id}}</div>
            <div class="col-4">{{note.name}}</div>
            <div class="col-4">{{note.surname}}</div>
            <div class="col-4">{{note.phone}}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data(){
    return{
      title: 'Записная книжка',
      name: '',
      surname: '',
      phone: '',
      notes: [],
    };
  },
  methods: {
    onSave(){
      let note = {
        name: this.name,
        surname: this.surname,
        phone: this.phone
        }

      this.$http.post(`${process.env.VUE_APP_API_HOST}/notes`, note).then(res => console.log(res));
      this.onLoad();
    },
    onLoad(){
      this.$http.get(`${process.env.VUE_APP_API_HOST}/notes`)
          .then(res => res.json())
          .then(res => this.notes = res)
    }
  },


}
</script>

<style>

.Row{
  display: flex;
  justify-content: center;
  width: 100%;
  margin: 10px 0 10px 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
