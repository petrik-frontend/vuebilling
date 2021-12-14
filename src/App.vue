<template>
  <div id="app">
    <table border="1">
      <thead>
        <tr>
          <th>Név</th>
          <th>Ár (Ft)</th>
          <th>DB</th>
          <th>Operations</th>
          <th>Összérték (Ft)</th>
        </tr>
      </thead>
      <tbody>
        <RowEditor
          v-for="row in rows"
          v-bind:key="row.title" 
          :row="row"
          @save-row="SaveRow"
          @delete-row="DeleteRow"
        /> 
        <RowEditor @add-new-row="AddNewRow"/>
        <tr><th colspan="4">Össz total</th><td>{{ total }}</td></tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import RowEditor from './components/RowEditor.vue'
export default {
  name: 'App',
  components: {
    RowEditor
  },
  data() {
    return {
      newRow: {
        title: '',
        price: null,
        quantity: null
      },
      editedRow: {
        old: {
          title: '',
          price: null,
          quantity: null
        }, 
        new: {
          title: '',
          price: null,
          quantity: null
        } 
      },
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
      ]
    }
  },
  methods: {
    AddNewRow (row) {
      let exists = false
      this.rows.forEach(function(item){
        if (item.title == row.title) {
          exists = true
        }
      })
      if (!exists) {
        this.rows.push({...row})
      }
      else {
        if (row.price == null || row.price=="") {
          this.rows.map(function(item){
            if (item.title == row.title) {
              item.quantity = 
              parseInt(item.quantity) + 
              parseInt(row.quantity)
            }
            return item
          })
        }
        else {
          this.rows = this.rows.map(function (item){
            if (item.title != row.title) {
              return item
            }
            return row
          })
        }
      }
    },
    DeleteRow(title) {
      this.rows = this.rows.filter(function (item){
        return item.title != title
      })
    },
    EditRow(editedRow) {
      this.editedRow.old = {...editedRow}
      this.editedRow.new = {...editedRow}
    },
    SaveRow (editedRow) {
      this.rows = this.rows.map(function (item) {
        if (item.title != editedRow.old.title) {
          return item
        }
        return {...editedRow.new}
      })
      this.editedRow.old.title = ''
    }
  },
  computed: {
    total() {
      let total = 0
      this.rows.forEach(function(item){
        total += item.price * item.quantity
      })
      return total
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
