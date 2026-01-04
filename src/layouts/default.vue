<template>
  <v-app>
    <v-layout>
      <v-navigation-drawer
        color="#F8F8FA"
        expand-on-hover
        permanent
        rail
        :scrim="false"
      >
        <v-list>
          <v-list-item
            prepend-avatar="../assets/flux_logo.png"
            subtitle="Movement and data flow"
            title="Flux"
          />
        </v-list>

        <v-divider />

        <v-list density="compact" nav>
          <v-list-item prepend-icon="mdi-view-dashboard" title="Dashboard" to="/" value="dashboard" />
          <v-list-item prepend-icon="mdi-cart" title="Marketplace" to="/marketplace" value="marketplace" />
          <v-list-item prepend-icon="mdi-truck-cargo-container" title="Orders" to="/orders" value="orders" />
          <v-list-item prepend-icon="mdi-transit-connection-horizontal" title="Tracking" to="/tracking" value="tracking" />
          <v-list-item prepend-icon="mdi-account" title="Customers" to="/customers" value="customers" />
          <br/>
          <v-divider />
          <v-list-item prepend-icon="mdi-cog" title="Settings" to="/settings" value="settings" />
          <v-list-item 
            prepend-icon="mdi-weather-night" 
            title="Dark Mode"
          >
            <template v-slot:append>
              <v-switch 
                v-model="isDark" 
                inset 
                hide-details
              ></v-switch>
            </template>
          </v-list-item>
        </v-list>
      </v-navigation-drawer>

      <v-main class="fill-height" style="overflow:auto">
        <v-container fluid>
          <router-view />
        </v-container>
      </v-main>
    </v-layout>
  </v-app>
</template>

<script lang="ts" setup>
  //
</script>

<style>
/* Ensure the html and body tags take up the full height */
html, body, #app, .v-application {
  height: 100%;
  margin: 0;
}
</style>
