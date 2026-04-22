<template>
  <v-container class="py-6">
    <div class="mb-6">
      <h1 class="text-h4">Patients in this care unit</h1>
      <p class="text-body-2 text-secondary">List of patients manageable from current station</p>
    </div>

    <v-card>
      <v-card-title>
        <div class="text-h6">Patients</div>
      </v-card-title>

      <v-data-table
        :headers="headers"
        :items="users"
        :items-per-page="5"
        class="elevation-1"
      >
        <template #[`item.status`]="{ item }">
          <v-chip
            :color="getStatusColor(item.status)"
            size="small"
            variant="flat"
          >
            {{ item.status }}
          </v-chip>
        </template>

        <template #[`item.actions`]="{ item }">
          <v-btn
            size="small"
            color="primary"
            variant="outlined"
            @click="viewDetails(item)"
          >
            View details
          </v-btn>
        </template>
      </v-data-table>
    </v-card>
  </v-container>
</template>

<script lang="ts" setup>
import { useRouter } from 'vue-router'

interface User {
  id: number
  name: string
  status: string
}

const router = useRouter()

const headers = [
  { title: 'Name', key: 'name' },
  { title: 'Status', key: 'status' },
  { title: 'Actions', key: 'actions', sortable: false },
]

const users: User[] = [
  { id: 1, name: 'Aino Korhonen', status: 'OK' },
  { id: 2, name: 'Eero Nieminen', status: 'Out temporarily' },
  { id: 3, name: 'Salla Virtanen', status: 'Sick' },
  { id: 4, name: 'Mikko Laine', status: 'Critical' },
  { id: 5, name: 'Anna Mäkinen', status: 'Other' },
]

const getStatusColor = (status: string): string => {
  switch (status) {
    case 'OK':
      return 'success'
    case 'Out temporarily':
      return 'grey'
    case 'Sick':
      return 'warning'
    case 'Critical':
      return 'error'
    default:
      return 'primary'
  }
}

const viewDetails = (user: User) => {
  router.push('/singleuser')
}
</script>
