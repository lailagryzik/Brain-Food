<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card class="logo py-4 d-flex justify-center">
      <!--Todo: add images here -->
      </v-card>
      <v-card class="pa-4">
        <v-card-title class="headline">
          Anmeldung:
        </v-card-title>
        <v-card-text> 
          <!--Hinweis-->
          <p> 
            Bitte melden Sie sich mit Ihren Zugangsdaten an.
            </br>Die Zugangsdaten haben Sie postalisch von Ihrer Krankenversicherung erhalten.
          </p>
          <p>
            Falls Sie noch keine Zugangsdaten haben, wenden Sie sich bitte an Ihre Krankenversicherung.
          </p> 
  
          <hr class="my-3" />        
          <br />
          <!--Name und Passwort Feld -->
          <v-text-field
            v-model="name"
            label="Name"
            required
          ></v-text-field>
          <v-text-field
            v-model="versicherungsnummer"
            label="Versicherungsnummer"
            type="number"
            required
          ></v-text-field>
          <v-text-field
            v-model="birthdate"
            label="Geburtsdatum"
            type="date"
            required
          ></v-text-field>
          <v-text-field
            v-model="password"
            :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
            :type="show1 ? 'text' : 'password'"
            name="input-10-1"
            label="Passwort"
            @click:append="show1 = !show1"
          ></v-text-field>


        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn 
            color="primary" 
            nuxt @click="login"
    
            :disabled="name?.length<=4 || password!='123456789'"
          > anmelden </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: "IndexPage",
  data() {
    return {
      name: "",
      versicherungsnummer: "",
      birthdate: "",
      password: "",
      show1: false,
    };
  },
  //Methoden für die Anmeldung
  methods: {
    login() {
      localStorage.setItem("name", this.name);
      localStorage.setItem("versicherungsnummer", this.versicherungsnummer);
      localStorage.setItem("birthdate", this.birthdate);
      localStorage.setItem("isLoggedIn", true);
      this.$router.push("/startseite");
    },
  },
  //wird ausgeführt beim Laden der Seite
  mounted() {
    this.name = localStorage.getItem("name");
    this.versicherungsnummer = localStorage.getItem("versicherungsnummer");
    this.isLoggedIn = localStorage.getItem("isloggedin")== "true";
    console.log("is logged in", this.isLoggedIn);
    if (this.isLoggedIn) {
      this.$router.push("/startseite");
    }
  },
};
</script>
