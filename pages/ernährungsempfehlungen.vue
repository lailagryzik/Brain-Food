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
          description: "Wasser ist wichtig für den Körper",
          stress: 1,
          concentration: 1,
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
          description: "Wallnüsse sind gut für das Gehirn",
          stress: 2,
          concentration: 3,
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
          title: "Vollkornprodukte",
          src: "https://cdn.pixabay.com/photo/2016/03/05/22/21/baked-1239259_960_720.jpg",
          description: "Vollkornprodukte halten lange satt",
          stress: 3,
          concentration: 4,
          nutrition: {
            makro: ["Komplexe Kohlenhydrate"],
            mikro: ["Magnesium", "Zink", "Eisen"],
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
