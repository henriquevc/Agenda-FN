<template>
  <q-layout view="lHh Lpr lFf" max-width="760px" style="max-width: 560px; margin: 0 auto;">
    <h6>Agenda Fernando de Noronha</h6>
    <q-page-container>
      <router-view />
    </q-page-container>
    <q-tabs class="fixed-bottom q-mb-md">
      <q-route-tab
        icon="fitness_center"
        label="Academia"
        to="/academia"
        exact
      />
      <q-route-tab
        icon="home"
        label="Home"
        to="/"
        exact
      />
    </q-tabs>
  </q-layout>
</template>

<script>
export default {
    name: 'MainLayout',
    data () {
        return {
            leftDrawerOpen: false
        }
    }
}
</script>
