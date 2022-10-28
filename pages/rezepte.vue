<template>
  <v-container>
    <v-container fluid v-if="this.isLoggedIn">
      <v-row
        ><v-text-field
          class="mx-2"
          label="Suche"
          single-line
          solo
          placeholder="Filter"
          v-model="searchInput"
        ></v-text-field>
        <v-select
          class="mx-2"
          v-model="selectedDayFilter"
          :items="DayFilter"
          solo
          label="Nährstoffe"
        ></v-select>
        <v-select
          class="mx-2"
          v-model="selectedZutatFilter"
          :items="ZutatFilter"
          solo
          label="Nährstoffe"
        ></v-select>
      </v-row>
      <v-row dense>
        <v-col v-for="r in filteredRezepte" :key="r.title" :cols="6">
          <v-card>
            <template slot="progress">
              <v-progress-linear
                color="deep-purple"
                height="10"
                indeterminate
              ></v-progress-linear>
            </template>

            <v-card-title>{{ r.title }}</v-card-title>

            <v-card-text>
              <div v-for="(el, index) of r.description" :key="index">
                {{ el }}
              </div>
            </v-card-text>
            <v-expansion-panels flat class="mt-n3">
              <v-expansion-panel>
                <v-expansion-panel-header> Zutaten </v-expansion-panel-header>
                <v-expansion-panel-content>
                  <v-simple-table>
                    <template v-slot:default>
                      <thead></thead>
                      <tbody>
                        <tr v-for="item in r.zutaten" :key="item.name">
                          <td>{{ item.name }}</td>
                          <td>{{ item.menge }}</td>
                        </tr>
                      </tbody>
                    </template>
                  </v-simple-table>
                </v-expansion-panel-content>
              </v-expansion-panel>
            </v-expansion-panels>
            <v-divider class="mx-4 mb-n3"></v-divider>

            <v-card-actions class="mt-5">
              <v-chip
                class="mx-1"
                v-for="(tageszeit, index) of r.tageszeit"
                :key="index"
                >{{ tageszeit }}</v-chip
              >
              <v-spacer></v-spacer>
              <v-btn
                filled
                :color="
                  favorites.map((el) => el.title).includes(r.title)
                    ? 'primary'
                    : 'black'
                "
                text
                @click="favorite(r)"
              >
                <v-icon>mdi-heart</v-icon>
              </v-btn></v-card-actions
            >
          </v-card>
        </v-col>
      </v-row>
    </v-container>
    <v-container v-else>
      <v-btn to="/">Bitte einloggen</v-btn>
    </v-container>
  </v-container>
</template>

<script>
export default {
  name: "IndexPage",
  data() {
    return {
      isLoggedIn: false,
      searchInput: "",
      selectedDayFilter: "Kein Filter",
      DayFilter: [
        //Methode für Zeiten Filter
        "Kein Filter",
        "Frühstück",
        "Mittagessen",
        "Abendessen",
        "Snack",
      ],
      selectedZutatFilter: "Kein Filter",
      //Methode für Zutaten Filter
      rezepte: [
        //Anzeige der Rezepte
        {
          title: "Powermüsli",
          description: [
            "1. Das Obst waschen, schneiden und in eine Schale geben",
            "2. Joghurt, Agavensirup, Hafer- sowie Dinkelflocken, Leinsamen, Weizenkeime und Sonnenblumenkerne dazugeben und umrühren.",
          ],
          zutaten: [
            {
              name: "Sojajoghurt",
              menge: "120 g",
            },

            {
              name: "Agavensirup",
              menge: "1 EL",
            },
            {
              name: "Feine Haferflocken",
              menge: "3 EL",
            },
            {
              name: "Dinkelflocken",
              menge: "3 EL",
            },
            {
              name: "Leinsamen",
              menge: "1 EL",
            },
            {
              name: "Weizenkeime",
              menge: "1 EL",
            },
            {
              name: "Sonnenblumenkerne",
              menge: "1 EL",
            },
          ],
          tageszeit: ["Frühstück"],
        },

        {
          title: "Brain-Juice",
          description: [
            "1. Blaubeeren waschen und mit den restlichen Zutaten in einen Mixer geben",
            "2. Zutaten fein pürieren und mit Agavensirup abschmecken",
          ],
          zutaten: [
            {
              name: "Sojajoghurt",
              menge: "125 g",
            },

            {
              name: "Orangensaft",
              menge: "100 ml",
            },
            {
              name: "Feine Haferflocken",
              menge: "1 EL",
            },
            {
              name: "Blaubeeren",
              menge: "50 g",
            },
            {
              name: "Agavensirup",
              menge: "1-2 TL",
            },
          ],
          tageszeit: ["Snack", "Frühstück"],
        },
        {
          title: "Energiekugeln",
          description: [
            "1. Haferflocken in einer Schüssel mit Orangensaft einweichen",
            "2. Kleingeschnittene Aprikosen und Pflaumen dazugeben und mit Mandeln und Sesam im Mixer fein pürieren",
            "3. Aus dem Teig mit angefeuchteten Händen Bälle formen und in Kakao, Sesam oder Mandeln wälzen",
          ],
          zutaten: [
            {
              name: "Feine Haferflocken",
              menge: "20 g",
            },

            {
              name: "Orangensaft",
              menge: "2 EL",
            },
            {
              name: "Getrocknete Aprikosen",
              menge: "50 g",
            },
            {
              name: "Getrocknete Pflaumen",
              menge: "25 g",
            },
            {
              name: "Gemahlene Mandeln",
              menge: "15 g",
            },
            {
              name: "Sesam",
              menge: "15 g",
            },
            {
              name: "Kakaopulver, Sesam oder Gemahlene Mandeln",
              menge: "1 EL",
            },
          ],
          tageszeit: ["Snack"],
        },
        {
          title: "Apfelringli",
          description: [
            "1. Wasser in eine Schüssel füllen und mit einer Prise Salz und dem Saft einer halben Zitrone mischen",
            "2. Die Äpfel schälen, das Kerngehäuse entfernen, in Scheiben schneiden und 10 Min. in Zitronenwasser legen",
            "3. Ringe zum Abtropfen auf ein Gitter legen",
            "4. Für 2 Stunden lang bei 50 Grad im Backofen bei leicht geöffneter Klappe trocknen lassen. ",
          ],
          zutaten: [
            {
              name: "Apfel",
              menge: "5",
            },

            {
              name: "Salz",
              menge: "Prise",
            },
            {
              name: "Zitrone",
              menge: "1/2",
            },
            {
              name: "Wasser",
              menge: "1 Liter",
            },
          ],
          tageszeit: ["Snack"],
        },
        {
          title: "Lachs doch mal",
          description: [
            "1. Reis kochen und in der Zeit retsliche Zutaten vorbereiten",
            "2. Den Lachs waschen, trocken tupfen und mit etwas Öl kurz heiß braten",
            "3. Für 10 Minuten auf 100 Grad im Backofen garen",
            "4. Algen 20 Minuten kochen, abgießen und mit Öl, Salz und Pfeffer würzen",
            "5. Algen und Lachs auf dem Reis anrichten",
          ],
          zutaten: [
            {
              name: "Lachsfilet",
              menge: "120 g",
            },

            {
              name: "Avocado-Öl",
              menge: "2 EL",
            },
            {
              name: "Nori Algen",
              menge: "50 g",
            },
            {
              name: "Reis",
              menge: "50 g",
            },
          ],
          tageszeit: ["Abendessen"],
        },
        {
          title: "Avocadosuppe",
          description: [
            "1. Avocados halbiere, entkernen, schälen und in Stücke schneiden",
            "2. Avocado mit Kokosmilch und Zitronensaft pürieren",
            "3. Suppe im Topf heiß werden lassen, nicht kochen",
            "4. Suppe kräftig würzen und mit Schnittlauch garnieren",
          ],
          zutaten: [
            {
              name: "Avocado",
              menge: "2",
            },

            {
              name: "Zitronensaft",
              menge: "1 EL",
            },
            {
              name: "Kokosmilch",
              menge: "200 ml",
            },
            {
              name: "Schnittlauch",
              menge: "5 Stängel",
            },
          ],
          tageszeit: ["Mittagessen"],
        },

        {
          title: "Nudeln mit Brokkoli",
          description: [
            "1. Nudeln nach Packungsanleitung kochen",
            "2. Brokkoli waschen, in kleine Röschen teilen und in Salzwasser 5 Minuten garen",
            "3. Knoblauch hacken, Brokkoli abgießen und beides anbraten",
            "4. Nudeln abgießen und mit der Brokkoli-Knoblauch-Mischung vermengen",
            "5. Würzen und mit Sonnenblumenkernen garnieren",
          ],
          zutaten: [
            {
              name: "Vollkornudeln",
              menge: "200 g",
            },

            {
              name: "Brokkoli",
              menge: "150 g",
            },
            {
              name: "Knoblauch",
              menge: "1/2 Zehe",
            },
            {
              name: "Sonnenblumenkerne",
              menge: "1 EL",
            },
          ],
          tageszeit: ["Mittagessen"],
        },
        {
          title: "Hafer-Rührei",
          description: [
            "1. Haferflocken in der Pfanne anrösten",
            "2. Eier mit Salz und Pfeffer verquirlen und in die Pfanne geben",
            "3. Tomaten waschen, vierteln und in die Pfanne geben",
            "4. Rührei bei mittlerer Hitze 5 Minuten garen",
            "5. Mit Schnittlauch garnieren",
          ],
          zutaten: [
            {
              name: "Feine Haferflocken",
              menge: "40 g",
            },

            {
              name: "Ei",
              menge: "2",
            },
            {
              name: "Hafermilch",
              menge: "25 ml",
            },
            {
              name: "Cocktailtomaten",
              menge: "5",
            },
            {
              name: "Schnittlauch",
              menge: "5 Stängel",
            },
          ],
          tageszeit: ["Frühstück", "Mittagessen"],
        },
        {
          title: "Bananen-Smoothie",
          description: [
            "1. Alle Zutaten in einen Mixer geben und fein pürieren",
          ],
          zutaten: [
            {
              name: "Banane",
              menge: "2",
            },

            {
              name: "Hafermilch",
              menge: "100 ml",
            },
            {
              name: "Zimt",
              menge: "1 TL",
            },
            {
              name: "Eiswürfel",
              menge: "4",
            },
          ],
          tageszeit: ["Snack", "Frühstück"],
        },
        {
          title: "Süßkartoffelchips",
          description: [
            "1. Süßkartoffeln waschen, schälen und in dünne Scheiben schneiden",
            "2. Scheiben in Öl tunken und auf einem Backblech verteilen",
            "3. Für 20 Minuten bei 180 Grad im Backofen backen und danach salzen",
          ],
          zutaten: [
            {
              name: "Süßkartoffel",
              menge: "300 g",
            },

            {
              name: "Öl",
              menge: "1 EL",
            },
            {
              name: "Salz",
              menge: "1 TL",
            },
          ],
          tageszeit: ["Snack"],
        },
        {
          title: "Penne statt Pennen",
          description: [
            "1. Nudeln nach Packungsanleitung kochen",
            "2. Brokkoli waschen, in kleine Röschen teilen und in Salzwasser 5 Minuten garen",
            "3. Knoblauch und Zwiebeln hacken und in Öl anbraten",
            "4. Brokkoli abgießen, getrocknete Tomaten kleinschneiden und mit der Knoblauch-Zwiebel-Mischung vermengen",
            "5. Nudeln abgießen, alles vermengen und würzen",
            "6. Mit Rucola garnieren",
          ],
          zutaten: [
            {
              name: "Knoblauch",
              menge: "1 Zehe",
            },

            {
              name: "Zwiebel",
              menge: "1",
            },
            {
              name: "Brokkoli",
              menge: "400 g",
            },
            {
              name: "Ricotta",
              menge: "100 g",
            },
            {
              name: "Getrocknete Tomaten",
              menge: "25 g",
            },
            {
              name: "Rucola",
              menge: "1 Bund",
            },
            {
              name: "Vollkorn Penne",
              menge: "350 g",
            },
          ],
          tageszeit: ["Abendessen"],
        },
        {
          title: "Kichererbsen-Avocado Salat",
          description: [
            "1. Grapefruit entsaften und mit Honig und Öl vermischen",
            "2. Avocado schälen, in Scheiben schneiden und mit der Marinade vermengen",
            "3. Kichererbsen und Koriander hinzugeben",
            "4. Mit Salz und Pfeffer würzen",
            "5. Mit Sesam garnieren",
          ],
          zutaten: [
            {
              name: "Grapefruit",
              menge: "1",
            },

            {
              name: "Honig",
              menge: "3 TL",
            },
            {
              name: "Öl",
              menge: "2 EL",
            },
            {
              name: "Sesam",
              menge: "1 EL",
            },
            {
              name: "Koriander",
              menge: "1 Bund",
            },
            {
              name: "Avocado",
              menge: "1",
            },
            {
              name: "Kichererbsen",
              menge: "1 Dose",
            },
          ],
          tageszeit: ["Abendessen"],
        },
      ],
      favorites: [],
    };
  },
  mounted() {
    this.favorites = JSON.parse(localStorage.getItem("favorites")) || [];
    this.isLoggedIn = localStorage.getItem("isLoggedIn") === "true";
  },
  methods: {
    favorite(rezept) {
      if (this.favorites.map((el) => el.title).includes(rezept.title)) {
        this.favorites = this.favorites.filter(
          (el) => el.title !== rezept.title
        );
      } else {
        this.favorites.push(rezept);
      }
      localStorage.setItem("favorites", JSON.stringify(this.favorites));
    },
  },
  //Methode zum Zeiten Filter
  computed: {
    filteredRezepte() {
      let filtered = this.rezepte;
      if (this.selectedDayFilter !== "Kein Filter") {
        filtered = filtered.filter((r) =>
          r.tageszeit.includes(this.selectedDayFilter)
        );
      }
      if (this.searchInput !== "") {
        filtered = filtered.filter(
          (r) =>
            r.tageszeit.includes(this.selectedDayFilter) ||
            r.description.toLowerCase().includes(this.searchInput.toLowerCase())
        );
      }
      if (this.selectedZutatFilter !== "Kein Filter") {
        filtered = filtered.filter((r) =>
          r.zutaten.map((el) => el.name).includes(this.selectedZutatFilter)
        );
      }
      return filtered;
    }, //Methode zum Zutaten Filter
    ZutatFilter() {
      let zutaten = [];
      zutaten.push("Kein Filter");
      this.rezepte.forEach((r) => {
        r.zutaten.forEach((z) => {
          if (!zutaten.includes(z.name)) {
            zutaten.push(z.name);
          }
        });
      });
      return zutaten;
    },
  },
};
</script>
