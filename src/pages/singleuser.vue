<template>
  <v-container class="py-6">
    <v-row class="mb-6" align="center" justify="space-between">
      <div>
        <h1 class="text-h4 mb-2">Patient overview</h1>
        <p class="text-body-2 text-secondary">Current information about your relative in the care of X facility</p>
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

          <div class="text-subtitle-2 mb-2">Last updated</div>
          <div class="text-body-2">{{ user.lastUpdated }}</div>

          <v-divider class="my-4" />

          <div class="text-subtitle-2 mb-3">Recent events</div>
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
              <div class="text-h6 font-medium">Profile summary</div>
              <div class="text-body-2 text-secondary">Basic contact and status details.</div>
            </div>
          </div>

          <v-row>
            <v-col cols="12" sm="6">
              <div class="text-subtitle-2 mb-2">Name</div>
              <div class="text-body-1">{{ user.name }}</div>
            </v-col>
            <v-col cols="12" sm="6">
              <div class="text-subtitle-2 mb-2">Status</div>
              <div class="text-body-1">{{ user.status }}</div>
            </v-col>
            <v-col cols="12" sm="6">
              <div class="text-subtitle-2 mb-2">Last updated</div>
              <div class="text-body-1">{{ user.lastUpdated }}</div>
            </v-col>
          </v-row>
        </v-card>

        <v-card class="pa-4 mb-4">
          <div class="text-h6 font-medium mb-4">Chat history</div>
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
          <div class="text-h6 font-medium mb-4">Current preferences</div>
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
          <div class="text-h6 font-medium mb-4">Active medications</div>
          <v-table>
            <template #default>
              <thead>
                <tr>
                  <th class="text-start">Medication</th>
                  <th class="text-start">Schedule</th>
                  <th class="text-end">Amount</th>
                  <th class="text-start">Reson</th>
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
  name: 'Laura Laine',
  status: 'All OK',
  lastUpdated: '5 minutes ago',
  avatar: 'https://ui-avatars.com/api/?name=LL',
}

const events: EventItem[] = [
  { id: 1, title: 'General nurse check', time: 'Today, 08:15' },
  { id: 2, title: 'Doctor visit', time: 'Yesterday, 16:40' },
  { id: 3, title: 'Family visit', time: '2 days ago' },
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
  { id: 1, sender: 'Sami - nurse', message: 'Sure, no problem', time: '08:10' },
  { id: 2, sender: 'me', message: 'Would it be possible to schedule a family visit for tomorrow at noon', time: '08:20' },
  { id: 3, sender: 'Pentti - doctor', message: 'All looking good so far', time: '08:15' },
]

const preferences: PreferenceItem[] = [
  { id: 1, label: 'DNR', value: 'No' },
  { id: 2, label: 'Limitation on care', value: 'None' },
  { id: 3, label: 'Other notables', value: '-' },
]

const newsletterSubscriptions: NewsletterSubscription[] = [
  { id: 1, name: 'Burana', days: 'Daily', lines: 1, description: "For general pain managemenet" },
  { id: 2, name: 'Ketamine', days: 'Wednesday', lines: 15, description: "For fun" },
  { id: 3, name: 'Ketipinor', days: 'Hourly', lines: 5, description: "For fun" },
]
</script>
