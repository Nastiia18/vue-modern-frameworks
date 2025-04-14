<template>
  <v-card flat>
    <v-card-title class="d-flex justify-space-between align-center bg-grey-lighten-2">
      <span class="text-h5">List of students</span>
      <v-btn
        class="me-2"
        prepend-icon="mdi-plus"
        rounded="lg"
        text="Add"
        border
        @click="openAddDialog"
      ></v-btn>
    </v-card-title>

    <v-card-text>
      <v-text-field
        v-model="search"
        label="Search"
        prepend-inner-icon="mdi-magnify"
        variant="outlined"
        hide-details
        single-line
      ></v-text-field>
    </v-card-text>

    <v-data-table :headers="headers" :items="students" :search="search">
      <template v-slot:item="{ item }">
        <tr>
          <td>{{ item.fullName }}</td>
          <td>{{ item.birthYear }}</td>
          <td>{{ item.phone }}</td>
          <td>{{ item.email }}</td>
          <td>
            <v-icon color="black" icon="mdi-pencil" size="small" @click="openEditDialog(item)"></v-icon>
            <v-icon color="black" icon="mdi-delete" size="small" @click="removeStudent(item)"></v-icon>
          </td>
        </tr>
      </template>
    </v-data-table>

    <v-dialog v-model="dialog" max-width="500">
      <v-card>
        <v-card-title>{{ isEditing ? 'Edit student' : 'Add a student' }}</v-card-title>
        <v-card-text>
          <v-text-field v-model="newStudent.fullName" label="Full name"></v-text-field>
          <v-text-field v-model="newStudent.birthYear" label="Year of birth" type="number"></v-text-field>
          <v-text-field v-model="newStudent.phone" label="Phone"></v-text-field>
          <v-text-field v-model="newStudent.email" label="Email"></v-text-field>
        </v-card-text>
        <v-card-actions>
          <v-btn text @click="closeDialog">Cancel</v-btn>
          <v-spacer></v-spacer>
          <v-btn color="primary" text @click="saveNewStudent">{{ isEditing ? 'Save' : 'Add' }}</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-card>
</template>

<script setup>
import { ref } from 'vue'

const search = ref('')
const dialog = ref(false)
const isEditing = ref(false)
const newStudent = ref({ fullName: '', birthYear: '', phone: '', email: '' })

const headers = [
  { key: 'fullName', title: 'Full name' },
  { key: 'birthYear', title: 'Year of birth' },
  { key: 'phone', title: 'Phone' },
  { key: 'email', title: 'Email' },
  { key: 'actions', title: 'Actions', sortable: false }
]

const students = ref([
  { fullName: 'Бондар Анастасія', birthYear: 2005, phone: '+380671234567', email: 'nastiabondar@example.com' },
  { fullName: 'Круш Ірина', birthYear: 2004, phone: '+380661234567', email: 'ira@example.com' },
  { fullName: 'Бабаєва Вікторія', birthYear: 2002, phone: '+380631234567', email: 'babaka@example.com' },
  { fullName: 'Бажанова Богдана', birthYear: 2003, phone: '+380671987654', email: 'ищпвфтф@example.com' },
  { fullName: 'Буднік Ніна', birthYear: 2005, phone: '+380501234567', email: 'тштф@example.com' },
])

const openAddDialog = () => {
  isEditing.value = false
  newStudent.value = { fullName: '', birthYear: '', phone: '', email: '' }
  dialog.value = true
}

const saveNewStudent = () => {
  if (!newStudent.value.fullName || !newStudent.value.birthYear || !newStudent.value.phone || !newStudent.value.email) return
  students.value.unshift({ ...newStudent.value })
  closeDialog()
}

const closeDialog = () => {
  dialog.value = false
}
const removeStudent = (item) => {
  const index = students.value.indexOf(item)
  if (index !== -1) {
    students.value.splice(index, 1)
  }
}
const openEditDialog = (item) => {
  isEditing.value = true
  newStudent.value = { ...item }
  dialog.value = true
}

</script>
