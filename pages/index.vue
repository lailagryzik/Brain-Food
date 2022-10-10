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
          <p>
            Bitte melden Sie sich mit Ihren Zugangsdaten an.
            </br>Die Zugangsdaten haben Sie postalisch von Ihrer Krankenversicherung erhalten.
          </p>
          <p>
            Falls Sie noch keine Zugangsdaten haben, wenden Sie sich bitte an Ihre Krankenversicherung.
          </p>
  
          <hr class="my-3" />        
          <br />
          <!--name and password field -->
          <v-text-field
            v-model="name"
            label="Name"
            required
          ></v-text-field>
          <v-text-field
            v-model="versicherungsnummer"
            label="Versicherungsnummer"
            required
          ></v-text-field>
          <v-text-field
            v-model="birthdate"
            label="Geburtsdatum"
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
            :disabled="name!='Laila Gryzik' || password!='123456789'"
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
  methods: {
    login() {
      localStorage.setItem("name", this.name);
      localStorage.setItem("versicherungsnummer", this.versicherungsnummer);
      localStorage.setItem("birthdate", this.birthdate);
      this.$router.push("/startseite");
    },
  },
  mounted() {
    this.name = localStorage.getItem("name");
    this.versicherungsnummer = localStorage.getItem("versicherungsnummer");
    if(this.name && this.versicherungsnummer) {
      this.$router.push("/startseite");
    }
  },
};
</script>
