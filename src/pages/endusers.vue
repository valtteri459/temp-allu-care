<template>
  <v-container class="py-6">
    <div class="d-flex flex-column gap-4">
      <div>
        <h1 class="text-h4">Your relatives</h1>
        <p class="text-body-2 text-secondary">If your relatives are not on this list, contact your care facility to add them.</p>
      </div>

      <v-row align="stretch" dense>
        <v-col cols="12" md="6" lg="4" v-for="user in users" :key="user.id">
          <v-card class="h-100" :to="'/singleuser'">
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
              <div class="text-caption text-uppercase mb-2">Last updated</div>
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
}

const users: UserProfile[] = [
  {
    id: 1,
    name: 'Aino Korhonen',
    status: 'All OK',
    lastUpdated: '20 minutes ago',
    avatar: 'https://ui-avatars.com/api/?name=AK',
  },
  {
    id: 2,
    name: 'Pentti Korhonen',
    status: 'Minor fever',
    lastUpdated: '12 minutes ago',
    avatar: 'https://ui-avatars.com/api/?name=PK',
  },
]
</script>
