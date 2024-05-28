<template>
    <v-bottom-navigation :elevation="16" grow >
        <v-btn value="recent" to="/">
          <v-icon>mdi-email-open-heart-outline</v-icon>
          <span>Inicio</span>
        </v-btn>

        <v-btn value="nearby" to="/posts/gallery">
          <v-icon>mdi-image-multiple</v-icon>
          <span>Galeria</span> 
        </v-btn>
    </v-bottom-navigation>
</template>