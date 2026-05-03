<template>
  <v-container class="py-6">
    <v-row class="mb-6" align="center" justify="space-between">
      <div>
        <h1 class="text-h4 mb-2">Asiakkaan tiedot</h1>
        <p class="text-body-2 text-secondary">Nykyiset tiedot omaisen/asiakkaan tilasta hoivayksikössä</p>
      </div>
    </v-row>

    <v-row dense>
      <v-col cols="12" lg="4">
        <v-card class="pa-4">
          <div class="d-flex align-center gap-4 mb-4">
            <v-avatar size="72">
              <v-img :src="user.avatar" alt="Profile image" />
            </v-avatar>
            <div>
              <div class="text-h6 font-medium">{{ user.name }}</div>
              <div class="text-body-2 text-secondary">{{ user.status }}</div>
            </div>
          </div>

          <v-divider class="my-4" />

          <div class="text-subtitle-2 mb-2">Viimeksi päivitetty</div>
          <div class="text-body-2">{{ user.lastUpdated }}</div>

          <v-divider class="my-4" />

          <div class="text-subtitle-2 mb-3">Viimeaikaiset tapahtumat</div>
          <v-list dense>
            <v-list-item v-for="event in events" :key="event.id">
              <v-list-item-content>
                <v-list-item-title class="font-medium">{{ event.title }}</v-list-item-title>
                <v-list-item-subtitle class="text-body-2 text-secondary">{{ event.time }}</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-list>
        </v-card>
      </v-col>

      <v-col cols="12" lg="8">
        <v-card class="pa-4 mb-4">
          <div class="d-flex justify-space-between align-center mb-4">
            <div>
              <div class="text-h6 font-medium">Yleiset potilastiedot</div>
            </div>
          </div>

          <v-row>
            <v-col cols="12" sm="6">
              <div class="text-subtitle-2 mb-2">Nimi</div>
              <div class="text-body-1">{{ user.name }}</div>
            </v-col>
            <v-col cols="12" sm="6">
              <div class="text-subtitle-2 mb-2">Tila</div>
              <div class="text-body-1">{{ user.status }}</div>
            </v-col>
            <v-col cols="12" sm="6">
              <div class="text-subtitle-2 mb-2">Viimeksi päivitetty</div>
              <div class="text-body-1">{{ user.lastUpdated }}</div>
            </v-col>
          </v-row>
        </v-card>

        <v-card class="pa-4 mb-4">
          <div class="text-h6 font-medium mb-4">Keskusteluhistoria</div>
          <div class="d-flex flex-column gap-3">
            <div
              v-for="message in chatHistory"
              :key="message.id"
              class="pa-3 rounded-lg"
              :class="message.sender === 'me' ? 'bg-primary-lighten4' : 'bg-surface'">
              <div class="text-body-2 font-medium">{{ message.sender === 'me' ? 'You' : message.sender }}</div>
              <div class="text-body-1 mb-2">{{ message.message }}</div>
              <div class="text-caption text-secondary">{{ message.time }}</div>
            </div>
          </div>
        </v-card>

        <v-card class="pa-4 mb-4">
          <div class="text-h6 font-medium mb-4">Nykyiset hoitotiedot</div>
          <v-list dense>
            <v-list-item v-for="pref in preferences" :key="pref.id">
              <v-list-item-content>
                <v-list-item-title class="font-medium">{{ pref.label }}</v-list-item-title>
                <v-list-item-subtitle class="text-body-2 text-secondary">{{ pref.value }}</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-list>
        </v-card>

        <v-card class="pa-4">
          <div class="text-h6 font-medium mb-4">Aktiiviset lääkitykset</div>
          <v-table>
            <template #default>
              <thead>
                <tr>
                  <th class="text-start">Lääke</th>
                  <th class="text-start">Aikataulu</th>
                  <th class="text-end">Määrä</th>
                  <th class="text-start">Peruste</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="subscription in newsletterSubscriptions" :key="subscription.id">
                  <td>{{ subscription.name }}</td>
                  <td>{{ subscription.days }}</td>
                  <td class="text-end">{{ subscription.lines }}</td>
                  <td>{{ subscription.description }}</td>
                </tr>
              </tbody>
            </template>
          </v-table>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts" setup>
interface User {
  name: string
  status: string
  lastUpdated: string
  avatar: string
}

interface EventItem {
  id: number
  title: string
  time: string
}

interface ChatMessage {
  id: number
  sender: string
  message: string
  time: string
}

const user: User = {
  name: 'Eero Nieminen',
  status: 'Saattohoidossa',
  lastUpdated: '5 minuuttia sitten',
  avatar: 'https://ui-avatars.com/api/?name=EN',
}

const events: EventItem[] = [
  { id: 1, title: 'Hoitajan yleistarkistus', time: 'Tänään, 08:15' },
  { id: 2, title: 'Lääkärikäynti', time: 'Eilen, 16:40' },
  { id: 3, title: 'Perhevierailu', time: '2 päivää sitten' },
]

interface PreferenceItem {
  id: number
  label: string
  value: string
}

interface NewsletterSubscription {
  id: number
  name: string
  days: string
  lines: number
  description: string
}

const chatHistory: ChatMessage[] = [
  { id: 1, sender: 'Sami - hoitaja', message: 'Käy hyvin', time: '08:10' },
  { id: 2, sender: 'Minä', message: 'Olisiko mahdollista tulla vierailemaan huomenna iltapäivästä', time: '08:20' },
  { id: 3, sender: 'Pentti - lääkäri', message: 'Kaikki kunnossa', time: '08:15' },
]

const preferences: PreferenceItem[] = [
  { id: 1, label: 'DNR', value: 'On.' },
  { id: 2, label: 'Limitation on care', value: 'Ei ole' },
  { id: 3, label: 'Other notables', value: 'Lääkkeet tauolla.' },
]

const newsletterSubscriptions: NewsletterSubscription[] = [
  { id: 1, name: 'Burana', days: 'Tauolla', lines: 1, description: "Kivun hallintaan" },
  { id: 2, name: 'Amlodipiini', days: 'Tauolla', lines: 1, description: "Verenpaineen alennukseen" },
  { id: 3, name: 'Atorvastatiini', days: 'Tauolla', lines: 1, description: "Kolesterolin hallintaan" },
  { id: 4, name: 'Panadol', days: 'Päivittäin 8:00 14:00 20:00', lines: 1, description: "Kivun hallintaan" },
  { id: 4, name: 'Morfiini', days: 'Päivittäin joka tunti', lines: 1, description: "Kivun hallintaan" },
  { id: 5, name: 'Furesis', days: 'Tauolla', lines: 1, description: "nestetasojen hallintaan" },
  { id: 6, name: 'Lisävitamiini', days: 'Tauolla', lines: 1, description: "Lisäravinteet" },
  { id: 7, name: 'Norspan (Buprenorfiini)', days: 'Tauolla', lines: 1, description: "Krooniseen kipuun" },
  { id: 7, name: 'bisoprolol', days: 'Tauolla', lines: 1, description: "Sydämmen tahdistus" },
]
</script>
