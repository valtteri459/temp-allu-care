<template>
  <v-container class="py-6">
    <div class="mb-6">
      <h1 class="text-h4">Hoitoyksikön asiakkaat</h1>
      <p class="text-body-2 text-secondary">Lista hoitoyksikön asiakkaista, joita nykyinen käyttäjä voi hallinnoida.</p>
    </div>

    <v-card>
      <v-card-title>
        <div class="text-h6">Asiakkaat</div>
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
            :to="item.link"
          >
            Näytä tiedot
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
  link: string
}

const router = useRouter()

const headers = [
  { title: 'Nimi', key: 'name' },
  { title: 'Tila', key: 'status' },
  { title: 'Toiminnot', key: 'actions', sortable: false },
]

const users: User[] = [
  { id: 1, name: 'Aino Korhonen', status: 'OK', link: "/singleuser" },
  { id: 2, name: 'Eero Nieminen', status: 'Saattohoidossa', link: "/singlethree" },
  { id: 3, name: 'Pentti Korhonen', status: 'Kipeä', link: "/singletwo" },
  { id: 4, name: 'Mikko Laine', status: 'Kriittinen', link: "/singlefour" },
  { id: 5, name: 'Anna Mäkinen', status: 'Muu', link: "/singlefive" },
]

const getStatusColor = (status: string): string => {
  switch (status) {
    case 'OK':
      return 'success'
    case 'Saattohoidossa':
      return 'grey'
    case 'Kipeä':
      return 'warning'
    case 'Kriittinen':
      return 'error'
    default:
      return 'primary'
  }
}
</script>
