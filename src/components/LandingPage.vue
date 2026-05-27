<template>
  <v-container class="fill-height d-flex flex-column justify-center" max-width="1100">
    <div>
      <!--<v-img
        class="mb-4 font-weight-bold"
        height="150"
        src="@/assets/logo.png"
      />-->

      <div class="mb-8 text-center">
        <div class="text-body-medium font-weight-light mb-n1">Tervetuloa palvelun demoon</div>
        <div class="text-display-medium font-weight-bold">Hand i hand</div>
      </div>

      <v-row>
        <v-col cols="12">
          <v-card
            class="py-4"
            color="surface-variant"
            image="https://cdn.vuetifyjs.com/docs/images/one/create/feature.png"
            rounded="lg"
            variant="tonal"
          >
            <template #prepend>
              <v-avatar class="ml-2 mr-4" icon="mdi-rocket-launch-outline" size="60" variant="tonal" />
            </template>

            <template #image>
              <v-img position="top right" />
            </template>

            <template #title>
              <div class="my-title my-uppercase text-headline-medium font-weight-bold">Aloita</div>
            </template>

            <template #subtitle>
              <div class="text-body-large">
                <!--Change this page by updating <v-kbd>{{ `<HelloWorld />` }}</v-kbd> in <v-kbd>components/HelloWorld.vue</v-kbd>.-->
                Valitse alhaalta esimerkkinäkymä tietystä näkökulmasta
              </div>
            </template>
          </v-card>
        </v-col>

        <v-col v-for="link in links" :key="link.link" cols="12">
          <v-card
            append-icon="mdi-open-in-new"
            class="py-4"
            color="surface-variant"
            :to="link.link"
            rel="noopener noreferrer"
            rounded="lg"
            :subtitle="link.subtitle"
            :title="link.title"
            variant="tonal"
          >
            <template #prepend>
              <v-avatar class="ml-2 mr-4" :icon="link.icon" size="60" variant="tonal" />
            </template>
          </v-card>
        </v-col>
      </v-row>
    </div>
  </v-container>
</template>

<script setup lang="ts">
  const links = [
    {
      link: '/endusers',
      icon: 'mdi-text-box-outline',
      subtitle: "Aloitussivu lähiomaisille",
      title: 'Lähiomaiset',
    },
    {
      link: 'professional',
      icon: 'mdi-star-circle-outline',
      subtitle: 'Esimerkki aloitussivu hoivayksikön ammattilaisille',
      title: 'Ammattilaiset',
    },
  ]
</script>
