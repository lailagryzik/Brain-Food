<template>
  <v-container>
    <!--add header-->
    <v-container fluid>
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
          v-model="selectedNutritionFilters"
          :items="NutritionFilters"
          solo
          label="Nährstoffe"
        ></v-select>
      </v-row>
      <v-row dense>
        <v-col v-for="f in filteredFood" :key="f.title" :cols="3">
          <v-hover>
            <template v-slot:default="{ hover }">
              <v-card>
                <v-img
                  :src="f.src"
                  class="white--text align-end"
                  height="200px"
                  width="275px"
                >
                  <v-expand-transition>
                    <div
                      dark
                      v-if="hover"
                      class="d-flex transition-fast-in-fast-out black darken-2 v-card--reveal white--text"
                      style="height: 100%"
                    ></div>
                  </v-expand-transition>
                  <v-fade-transition>
                    <v-overlay
                      v-if="hover"
                      absolute
                      color="primary"
                      class="black--text"
                    >
                      <v-card class="pa-7" height="200px" width="275px">
                        <div v-if="!f.nutrition?.makro">
                          Keine makro nährwerte
                        </div>
                        <div v-else>
                          <b> Makro:</b> {{ f.nutrition?.makro?.join(", ") }}
                        </div>
                        <br />
                        <div v-if="!f.nutrition?.mikro">
                          Keine mikro nährwerte
                        </div>
                        <div v-else>
                          <b> Mikro:</b> {{ f.nutrition?.mikro?.join(", ")
                          }}<br />
                        </div>
                        <br />
                      </v-card>
                    </v-overlay>
                  </v-fade-transition>
                  <v-card-title v-text="f.title"></v-card-title>
                </v-img>

                <v-card-actions>
                  <v-container>
                    <v-row>
                      <div>
                        Konzentrationssteigerung
                        <v-rating
                          length="5"
                          readonly
                          :value="f.concentration"
                        ></v-rating></div></v-row
                    ><v-row>
                      <div>
                        Stressreduktion
                        <v-rating
                          length="5"
                          readonly
                          :value="f.stress"
                        ></v-rating></div></v-row
                  ></v-container>
                </v-card-actions>
              </v-card> </template
          ></v-hover>
        </v-col>
      </v-row>
    </v-container>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      searchInput: "",
      selectedNutritionFilters: "kein Filter", //default filter wert für mikro
      selectedPurposeFilters: "kein Filter", //default filter wert für mikro
      NutritionFilters: [
        "kein Filter",
        "Fett",
        "Komplexe Kohlenhydrate",
        "Eiweiß",
        "Vitamin B1",
        "Vitamin B3",
        "Vitamin B6",
        "Vitamin B9",
        "Vitamin C",
        "Vitamin E",
        "Magnesium",
        "Kalium",
        "Eisen",
        "Zink",
        "Selen",
      ], //erlaubte filter werte
      PurposeFilters: [
        "kein Filter",
        "Stressreduktion",
        "Konzentrationssteigerung",
      ], //erlaubte filter werte
      food: [
        {
          title: "Wasser",
          src: "https://cdn.pixabay.com/photo/2014/12/24/05/02/drop-of-water-578897_960_720.jpg",

          stress: 5,
          concentration: 5,
          nutrition: {
            mikro: [
              "Spurenelemente",
              "Magnesium",
              "Natrium",
              "Kalium",
              "Kalzium",
              "Eisen",
              "Zink",
            ],
          },
        },
        {
          title: "Nüsse",
          src: "https://cdn.pixabay.com/photo/2019/01/31/21/31/nut-3967992_960_720.jpg",

          stress: 4,
          concentration: 4,
          nutrition: {
            makro: ["Protein", "Fett", "Komplexe Kohlenhydrate"],
            mikro: [
              "Magnesium",
              "Zink",
              "Kalium",
              "Selen",
              "Vitamin E",
              "Vitamin B1",
              "Vitamin B6",
            ],
          },
        },
        {
          title: "Vollkornprodukte/Getreide",
          src: "https://cdn.pixabay.com/photo/2016/03/05/22/21/baked-1239259_960_720.jpg",

          stress: 3,
          concentration: 4,
          nutrition: {
            makro: ["Komplexe Kohlenhydrate"],
            mikro: ["Magnesium", "Zink", "Eisen"],
          },
        },
        {
          title: "Pflanzliches Öl",
          src: "https://cdn.pixabay.com/photo/2015/10/02/15/59/olive-oil-968657_960_720.jpg",

          stress: 4,
          concentration: 1,
          nutrition: {
            makro: ["Fett"],
            mikro: ["Vitaminlieferant", "Vitamin E"],
          },
        },
        {
          title: "Fisch",
          src: "https://media.istockphoto.com/photos/grilled-halibut-with-spinach-leeks-and-pine-nuts-picture-id503337620?b=1&k=20&m=503337620&s=170667a&w=0&h=L-LJlhhsNNQVrY65U6Ogj4vRZyC8QitUJshHl-mgZ_I=",

          stress: 4,
          concentration: 4,
          nutrition: {
            makro: ["Fett"],
            mikro: [
              "Vitamin B3",
              "Vitamin B12",
              "Kalium",

              "Magnesium",
              "Selen",
              "Zink",
            ],
          },
        },
        {
          title: "Hülsenfrüchte",
          src: "https://media.istockphoto.com/photos/an-up-close-picture-of-organic-legumes-picture-id163729647?b=1&k=20&m=163729647&s=170667a&w=0&h=v5XfpyB03WccAkxooV60n7AJBwQQyGa-nzcmVDMPRww=",

          stress: 4,
          concentration: 4,
          nutrition: {
            makro: ["Komplexe Kohlenhydrate", "Eiweiß"],
            mikro: ["Magnesium", "Eisen", "Zink", "Vitamin B9"],
          },
        },
        {
          title: "Kartoffeln",
          src: "https://cdn.pixabay.com/photo/2016/08/11/08/43/potatoes-1585060__340.jpg",

          stress: 2,
          concentration: 2,
          nutrition: {
            makro: ["Komplexe Kohlenhydrate"],
            mikro: ["Vintamin B12", "Vitamin C", "Magnesium", "Kalium"],
          },
        },
        {
          title: "Obst",
          src: "https://cdn.pixabay.com/photo/2021/10/07/15/24/fruits-6688947__340.jpg",

          stress: 3,
          concentration: 4,
          nutrition: {
            makro: ["Komplexe Kohlenhydrate", "Eiweiß"],
            mikro: ["Vitamin B3", "Vitamin B6", "Vitamin C", "Kalium"],
          },
        },
        {
          title: "Samen/Kerne",
          src: "https://cdn.pixabay.com/photo/2019/04/06/17/46/nuts-4107883__340.jpg",

          stress: 4,
          concentration: 4,
          nutrition: {
            makro: ["Komplexe Kohlenhydrate", "Eiweiß", "Fett"],
            mikro: ["Vitamin B1", "Vitamin E", "Eisen", "Kalium"],
          },
        },
        {
          title: "Weizenkeime",
          src: "https://media.istockphoto.com/photos/wheat-sprouts-on-a-green-plate-picture-id183584384?k=20&m=183584384&s=612x612&w=0&h=e3GFVfiR1o5dEOOyY5HWDARPKJqjYlOH14_hn78O73s=",

          stress: 2,
          concentration: 3,
          nutrition: {
            makro: ["Komplexe Kohlenhydrate", "Eiweiß"],
            mikro: ["Vitamin B1", "Vitamin B9", "Vitamin E"],
          },
        },
        {
          title: "Blattgemüse",
          src: "https://cdn.pixabay.com/photo/2017/04/09/21/35/spinach-2216967_960_720.jpg",

          stress: 2,
          concentration: 3,
          nutrition: {
            makro: [],
            mikro: ["Vitamin E", "Vitamin B9", "Eisen"],
          },
        },
        {
          title: "Avocado",
          src: "https://cdn.pixabay.com/photo/2017/08/15/14/34/avocado-2644150__340.jpg",

          stress: 3,
          concentration: 2,
          nutrition: {
            makro: ["Fett"],
            mikro: ["Vitamin B6", "Vitamin B3", "Vitamin E"],
          },
        },
        {
          title: "Zitrusfrüchte",
          src: "https://cdn.pixabay.com/photo/2019/11/30/11/14/oranges-4663073__340.jpg",

          stress: 3,
          concentration: 3,
          nutrition: {
            makro: ["Komplexe Kohlenhydrate"],
            mikro: ["Vitamin C", "Vitamin E"],
          },
        },
        {
          title: "Zitrusfrüchte",
          src: "https://cdn.pixabay.com/photo/2019/11/30/11/14/oranges-4663073__340.jpg",

          stress: 3,
          concentration: 3,
          nutrition: {
            makro: ["Komplexe Kohlenhydrate"],
            mikro: ["Vitamin C", "Vitamin E"],
          },
        },
        {
          title: "Zwiebelgemüse",
          src: "hhttps://cdn.pixabay.com/photo/2016/03/05/22/59/onions-1239423__340.jpg",

          stress: 2,
          concentration: 2,
          nutrition: {
            makro: [],
            mikro: ["Selen", "Vitamin E"],
          },
        },
      ],
    };
  },
  computed: {
    filteredFood() {
      let filtered = this.food.filter(
        (f) =>
          f.title.toLowerCase().includes(this.searchInput.toLowerCase()) ||
          f.description
            .toLowerCase()
            .includes(this.searchInput.toLowerCase()) ||
          f.nutrition?.makro
            ?.join(" ")
            .toLowerCase()
            .includes(this.searchInput.toLowerCase()) ||
          f.nutrition?.mikro
            ?.join(" ")
            .toLowerCase()
            .includes(this.searchInput.toLowerCase())
      );
      if (this.selectedNutritionFilters != "kein Filter") {
        filtered = filtered.filter(
          (f) =>
            f.nutrition?.makro?.includes(this.selectedNutritionFilters) ||
            f.nutrition?.mikro?.includes(this.selectedNutritionFilters)
        );
      }
      if (this.selectedPurposeFilters != "kein Filter") {
        filtered = filtered.filter((f) =>
          f.nutrition?.purpose?.includes(this.selectedPurposeFilters)
        );
      }
      return filtered;
    },
  },
};
</script>
