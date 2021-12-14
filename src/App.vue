<template>
  <div id="app">
    <table border="1">
      <thead>
        <tr>
          <th>Név</th>
          <th>Ár (Ft)</th>
          <th>DB</th>
          <th>Operations</th>
        </tr>
      </thead>
      <tbody>
        
        <tr v-for="row in rows" v-bind:key="row.title">
          <td v-if="row.title != editedRow.old.title">{{ row.title }}</td>
          <td v-if="row.title != editedRow.old.title">{{ row.price }}</td>
          <td v-if="row.title != editedRow.old.title">{{ row.quantity }}</td>
          <td v-if="row.title != editedRow.old.title">
            <button @click="DeleteRow(row.title)">X</button>
            <button @click="EditRow(row)">Edit</button>
          </td>
          <td v-if="row.title == editedRow.old.title">
            <input type="text" v-model="editedRow.new.title">
          </td>
          <td v-if="row.title == editedRow.old.title">
            <input type="number" v-model="editedRow.new.price">
          </td>
          <td v-if="row.title == editedRow.old.title">
            <input type="number" v-model="editedRow.new.quantity">
          </td>
          <td v-if="row.title == editedRow.old.title">
            <button @click="SaveRow">Save</button>
          </td>
        </tr>

        <tr>
          <td><input type="text" v-model="newRow.title"></td>
          <td><input type="number" v-model="newRow.price"></td>
          <td><input type="number" v-model="newRow.quantity"></td>
          <td><button @click="AddNew">Add</button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
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
    AddNew () {
      this.rows.push({... this.newRow})
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
    SaveRow () {
      let editedRow = {...this.editedRow}
      this.rows = this.rows.map(function (item) {
        if (item.title != editedRow.old.title) {
          return item
        }
        return {...editedRow.new}
      })
      this.editedRow.old.title = ''
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
