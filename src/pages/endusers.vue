<template>
  <v-container class="py-6">
    <div class="d-flex flex-column gap-4">
      <div>
        <h1 class="text-h4">Sinun läheiset</h1>
        <p class="text-body-2 text-secondary">Jos sinun läheisiä ei näy listalla, ole yhteydessä hoitopaikan henkilökuntaan.</p>
      </div>

      <v-row align="stretch" dense>
        <v-col cols="12" md="6" lg="4" v-for="user in users" :key="user.id">
          <v-card class="h-100" :to="user.link">
            <v-card-title class="gap-4">
              <v-avatar size="56">
                <v-img :src="user.avatar" alt="Profile image" />
              </v-avatar>
              <div>
                <div class="text-subtitle-1 font-medium">{{ user.name }}</div>
                <div class="text-body-2 text-secondary">{{ user.status }}</div>
              </div>
            </v-card-title>

            <v-card-text>
              <div class="text-caption text-uppercase mb-2">Viimeksi päivitetty</div>
              <div class="text-body-2">{{ user.lastUpdated }}</div>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </div>
  </v-container>
</template>

<script lang="ts" setup>
interface UserProfile {
  id: number
  name: string
  status: string
  lastUpdated: string
  avatar: string
  link: string
}

const users: UserProfile[] = [
  {
    id: 1,
    name: 'Aino Korhonen',
    status: 'Kaikki OK',
    lastUpdated: '20 minuuttia sitten',
    avatar: 'https://ui-avatars.com/api/?name=AK',
    link: '/singleuser'
  },
  {
    id: 2,
    name: 'Pentti Korhonen',
    status: 'Matala kuume',
    lastUpdated: '12 minuuttia sitten',
    avatar: 'https://ui-avatars.com/api/?name=PK',
    link: '/singletwo'
  },
]
</script>
