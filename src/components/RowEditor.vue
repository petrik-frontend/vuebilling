<template>
    <tr>
        <td v-if="!edit">{{ row.title }}</td>
        <td v-if="!edit">{{ row.price }}</td>
        <td v-if="!edit">{{ row.quantity }}</td>
        <td v-if="!edit">
            <button @click="DeleteRow">X</button>
            <button @click="EditRow">Edit</button>
        </td>
        <td v-if="!edit">{{ row.price * row.quantity}}</td>
        
        <td v-if="edit"><input type="text" v-model="newRow.title"></td>
        <td v-if="edit"><input type="number" v-model="newRow.price"></td>
        <td v-if="edit"><input type="number" v-model="newRow.quantity"></td>
        <td v-if="edit"><button @click="Action">{{ buttonTitle }}</button></td>
        <td v-if="edit"></td>
    </tr>

</template>

<script>
export default {
    props: ['row'], 
    data() {
        return {
            editStage: false,
            newRow: {
                title: this.row == null ? '' : this.row.title,
                price: this.row == null ? null : this.row.price,
                quantity: this.row == null ? null : this.row.quantity
            }
        }
    },
    methods: {
        Action() {
            if (this.row == null) {
                this.$emit('add-new-row', {...this.newRow})            
            } else {
                this.$emit('save-row', {
                    old: {...this.row},
                    new: {...this.newRow}
                })
                this.editStage = false
            }
        },
        EditRow () {
            this.editStage = true
        },
        DeleteRow () {
            this.$emit('delete-row', this.row.title)
        }
    },
    computed: {
        edit () {
            return this.row == null || this.editStage
        },
        buttonTitle() {
            return this.row == null ? 'Add' : 'Save'
        }
    }
}
</script>

<style>

</style>