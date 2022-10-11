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
          v-model="selectedMakroFilters"
          :items="makroFilters"
          solo
          label="Makronährstoffe"
        ></v-select>
        <v-select
          class="mx-2"
          v-model="selectedMikroFilters"
          :items="mikroFilters"
          solo
          label="Mikronährstoffe"
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
                      <v-card class="pa-3" height="100%">
                        <div v-if="!f.nutrition?.makro">
                          Keine makro nährwerte
                        </div>
                        <div v-else>
                          <b> makro:</b> {{ f.nutrition?.makro?.join(", ")
                          }}<br />
                        </div>
                        <div v-if="!f.nutrition?.mikro">
                          Keine makro nährwerte
                        </div>
                        <div v-else>
                          <b> makro:</b> {{ f.nutrition?.mikro?.join(", ")
                          }}<br />
                        </div>
                      </v-card>
                    </v-overlay>
                  </v-fade-transition>
                  <v-card-title v-text="f.title"></v-card-title>
                </v-img>

                <v-card-actions>
                  <v-spacer></v-spacer>
                  {{ f.description }}
                  <v-btn icon>
                    <v-icon>mdi-heart</v-icon>
                  </v-btn>
                </v-card-actions>
              </v-card>
            </template></v-hover
          >
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
      selectedMakroFilters: "kein Filter", //default filter wert für mikro
      selectedMikroFilters: "kein Filter", //default filter wert für mikro
      makroFilters: ["kein Filter", "Fett", "Kohlenhydrate", "Protein"], //erlaubte filter werte
      mikroFilters: ["kein Filter", "Magnesium", "Zink", "Selen"], //erlaubte filter werte
      food: [
        {
          title: "Wasser",
          src: "https://cdn.pixabay.com/photo/2014/12/24/05/02/drop-of-water-578897_960_720.jpg",
          description: "Wasser ist wichtig für den Körper",
          nutrition: {},
        },
        {
          title: "Nüsse",
          src: "https://cdn.pixabay.com/photo/2019/01/31/21/31/nut-3967992_960_720.jpg",
          description: "Wallnüsse sind gut für das Gehirn",
          nutrition: {
            makro: ["Protein", "Fett", "Kohlenhydrate"],
            mikro: [
              "Magnesium",
              "Zink",
              "Kalium",
              "Selen",
              "VitaminE",
              "VitaminB1",
              "VitaminB6",
            ],
          },
        },
        {
          title: "Vollkornprodukte",
          src: "https://cdn.pixabay.com/photo/2016/03/05/22/21/baked-1239259_960_720.jpg",
          description: "Vollkornprodukte halten lange satt",
          nutrition: {
            makro: ["Kohlenhydrate"],
            mikro: ["Magnesium", , "Zink", "Eisen"],
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
      if (this.selectedMakroFilters != "kein Filter") {
        filtered = filtered.filter((f) =>
          f.nutrition?.makro?.includes(this.selectedMakroFilters)
        );
      }
      if (this.selectedMikroFilters != "kein Filter") {
        filtered = filtered.filter((f) =>
          f.nutrition?.mikro?.includes(this.selectedMikroFilters)
        );
      }
      return filtered;
    },
  },
};
</script>
