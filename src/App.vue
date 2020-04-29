<template>
  <div id="app">
    <div class="ticketWrapper">
      <form @submit.prevent="onSubmit">
        <div>
          <label class="colLabel" for="">Type</label>
          <input type="text" ref="type" v-model="form.type">
        </div>
        <div>
          <label class="colLabel" for="">Description</label>
          <input type="text" ref="description" v-model="form.description">
        </div>
         <div>
          <label class="colLabel" for="">Fine</label>
          <input type="text" ref="fine" v-model="form.fine">
        </div>
        <div>
          <label class="colLabel" for="">Paid</label>
          <input type="radio" id="paid" v-model="form.isPaid" value="true" ref="paid">Yes
          <input type="radio" id="paid" v-model="form.isPaid" value="false" ref="unpaid" >No
        </div>
        <div>
          <button v-on:click="addTickets">{{btnFromAction}}</button>
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
            <td>{{ticket.isPaid ? "Yes" : "No"}}</td>
            <td>
              <button v-on:click="paidTicket(index)">{{ticket.isPaid ? "UnPaid":"Paid"}}</button>
              <button v-on:click="editTicket(index)">edit</button>
              <button v-on:click="deleteTicket(index)">delete</button>
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
      btnFromAction :'Add',
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
    onSubmit(){},
    addTickets() {
      
      if(this.form.type==="")
      {
        alert('please enter type')
        this.$refs.type.focus()
      }
      else if(this.form.description==="")
      {
        alert('please enter description')
        this.$refs.description.focus()
      }
      else if(this.form.fine==="")
      {
        alert('please enter fine')
        this.$refs.fine.focus()
      }
      else
      {
        const ticket ={
          type:this.form.type,
          description:this.form.description,
          fine:this.form.fine,
          isPaid:this.form.isPaid==="true"
        }
        
        this.tickets=[ ...this.tickets,ticket]
        this.resetForm()
      }
    },
    resetForm() {
      this.form.type='',
      this.form.description=''
      this.form.fine=''
      this.btnFromAction='Add'
      this.$refs.paid.checked=false;
      this.$refs.unpaid.checked=false;
    },
    editTicket(index){
      const ticketEdit = this.tickets[index]
      this.form.type = ticketEdit.type
      this.form.description=ticketEdit.description
      this.form.fine = ticketEdit.fine
      this.btnFromAction='Update'
      if(ticketEdit.isPaid)
      {
        this.$refs.paid.checked=true;
      }
      else{
        this.$refs.unpaid.checked=true;
      }
      this.deleteTicketItem(index)
    },
    paidTicket(index){
      this.tickets[index].isPaid=!this.tickets[index].isPaid;
    },
    deleteTicket(index)
    {
     this.deleteTicketItem(index)
    },
    deleteTicketItem(index)
    {
      this.tickets.splice(index,1)
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
.ticketWrapper
{
  text-align: left;
}
</style>
