<template>
  <div id="app">
      <table>
  <tr v-for="row in rows" v-bind:key="row">
    <td>{(row.title)}</td>
    <td>>{(row.price)}</td>
    <td>>{(row.quantity)}</td>
  </tr>
  <tr>
      <th>Title</th>
  <th>Price</th>
  <th>Quantity</th>
  <th>Szum</th>

  </tr>
    <b-form-input v-model="text">title</b-form-input>
    <b-form-input v-model="text">price</b-form-input>
    <b-form-input v-model="text">quantity</b-form-input>
</table>
  </div>
</template>


<script>

export default {
  name: 'App',
  data() {
    return {
      rows: [
        {
          title: 'Kerék',
          price: 100,
          quantity: 12
        },
        {
          title: 'Teleszkóp',
          price: 1000,
          quantity: 300
        },
        {
          title: 'Kormány',
          price: 230,
          quantity: 5
        },
        {
          title: 'Ajtó',
          price: 45120,
          quantity: 321
        },
        methods:{
          addRow: function(){
            this.rows.push({});
          },
           addColumn: function(){
             this.Columns.name(Operations);
           this.Columns.push({});
           var törles = new Vue({
                 removeRow: function(row){
                this.rows.$remove(row);
    }
})
           var edit = new Vue({
                 editRow: function(row){
                this.rows.$edit(row);
    }
})
           }
    
      ]
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
