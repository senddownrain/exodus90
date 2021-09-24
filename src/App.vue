<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
    <v-toolbar-title>Exodus</v-toolbar-title>
    
     
      <v-spacer></v-spacer>
      
      <!-- сегодня -->
       <v-btn text ><router-link to="/">  <v-icon color="white">mdi-checkbox-marked-circle</v-icon> </router-link></v-btn>
       <!-- список -->
       <v-btn text><router-link to="/list">  <v-icon color="white">mdi-format-list-checkbox</v-icon> </router-link></v-btn>
      <!-- добавить день -->
      <v-btn text><router-link to="/add"> <v-icon color="white">mdi-plus-circle</v-icon> </router-link></v-btn>
       <!-- добавить неделю -->
       <v-btn text><router-link to="/addweek"><v-icon color="white">mdi-beaker-plus-outline</v-icon></router-link></v-btn>
       
    </v-app-bar>

     <v-main>
      <router-view></router-view>
      
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    drawer: false
  }),
};
</script>
