<template>
  <q-layout view="lHh Lpr lFf" max-width="760px" style="max-width: 560px; margin: 0 auto;">
    <div class="text-center text-h4 q-my-md">Agenda Fernando de Noronha</div>
    <q-tabs class="q-mb-md">
      <q-route-tab
        icon="fitness_center"
        label="Academia"
        to="/"
        exact
      />
    </q-tabs>
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
    name: 'MainLayout'
}
</script>
