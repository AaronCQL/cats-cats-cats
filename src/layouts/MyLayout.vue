<template>
  <q-layout view="hHh lpR fFf">

    <q-header bordered class="bg-teal-8 text-white">
      <q-toolbar>

        <q-toolbar-title>
          <span class="text-weight-regular">Cats</span>
          <span class="text-weight-light">Cats</span>
          <span class="text-weight-thin">Cats</span>
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-page-container class="bg-blue-grey-1">
      <router-view />
    </q-page-container>

  </q-layout>
</template>

<script>
export default {

}
</script>