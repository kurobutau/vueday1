<template>
  <div id="app">
    <div class="add-ticket-wrapper">
      <form @submit.prevent="onSubmit">
        <div>
          <label for="">Type</label>
          <input type="text" v-model="form.type">
        </div>
        <div>
          <label for="">description</label>
          <input type="text" v-model="form.description">
        </div>
         <div>
          <label for="">fine</label>
          <input type="text" v-model="form.fine">
        </div>
        <div>
          <button v-on:click="addTickets">Add</button>
        </div>
      </form>
    </div>
    <div class="tickets-wrapper">
      <table border="1">
        <thead>
          <tr>
            <th>type</th>
            <th>description</th>
            <th>fine</th>
            <th>paid</th>
            <th>aciton</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(ticket,index) in tickets" :key="index">
            <td>{{ticket.type}}</td>
            <td>{{ticket.description}}</td>
            <td>{{ticket.fine}}</td>
            <td>{{ticket.isPaid}}</td>
            <td>
              <button v-on:click="editTicket">edit</button>
              <button v-on:click="deleteTicket">delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  data:function()
  {
    return{
      form:{
        type:'',
        description : '',
        fine:0,
        isPaid : false
      },
      tickets:[
      ],
    }
  },
  methods : {
    addTickets() {
      const ticket ={
        type:this.form.type,
        description:this.form.description,
        fine:this.form.fine,
        isPaid:false
      }
      this.tickets=[ ...this.tickets,ticket]
      this.resetForm()
    },
    resetForm() {
      this.form.type='',
      this.form.description=''
      this.form.fine=''
    },
    editTicket(){
      alert('edit')
    },
    deleteTicket()
    {
      alert('delete')
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
