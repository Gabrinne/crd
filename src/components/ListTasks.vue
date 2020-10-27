<template>
  <div>
    <h2> {{ title }} </h2>

    <div class="row mb-4 mt-4">
      <div class="col">
      <form class="form form-inline">
      <input  v-model="filter" type="text" class="form-control" placeholder="pesquisar" >
    </form>
      </div>


    <div class="col">
    <form @submit.prevent="onSubmit()" class="form form-inline ">
      <input type="text" placeholder="Nome Usuário" class="form-control" v-model="task.name">
      <button class="btn btn-success ml-2" type="submit">Enviar</button>
    </form>
    </div>

    </div>


    <table class="table table-dark">
      <thead>
        <tr >
          <th>Id</th>
          <th>Nome</th>

          <th width="180px">Ações</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in filtered" :key="index">
          <td>{{task.id}}</td>
          <td>{{ task.name}} </td>

          <td>
            <a href="#" @click.prevent="edit(task.id)" class="btn btn-info">Editar</a>
            <a href="" @click.prevent="deleteTask(task.id)" class="btn btn-danger">Deletar</a>
          </td>
        </tr>
      </tbody>
    </table>



  </div>
</template>

<script>
export default {
 data() {
   return {
     title: 'Lista de Usuários',
      task: {
        id: null,
        name: '',
      },
      updating: false,
      updateIndex: '',
      filter: ''
   }
 },
 props: {
   tasks: {
     required: true,
     type: Array
   }
 },



 methods: {
   onSubmit() {

    this.updating ? this.update() : this.save()

   },
   save() {
    this.task.id = this.tasks.length + 1
     this.tasks.push(this.task)
     this.clearForm()
   },
   edit(id) {
     this.updateIndex = this.findIndexTask(id)
     this.task = this.tasks[this.updateIndex]

     this.updating = true
   },
   update() {
     this.tasks[this.updateIndex] = this.task
     this.updating = false
     this.clearForm()

   },

   deleteTask(id){
     let index = this.findIndexTask(id)
      this.tasks.splice(index, 1)
   },
   findIndexTask(id) {
     for (let index = 0; index < this.tasks.length; index++) {
          if(this.tasks[index].id == id)
          return index
      }
   },

   clearForm() {
      this.task = {
         id: null,
        name: '',

      }
   }

 },

 computed: {
   filtered () {
     if (this.filter === '')
       return this.tasks

       return this.tasks.filter(task => {
          return task.name.toLowerCase().indexOf(this.filter.toLowerCase()) > -1
       })

   }
 }
}
</script>

<style>

</style>
