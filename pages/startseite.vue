<template>
  <v-container>
    <v-row v-if="today">
      <v-col>
        <v-sheet height="500">
          <v-calendar :now="today" :value="today" color="primary">
            <template v-slot:day="{ date }">
              <v-row class="fill-height">
                <template v-if="tracked[date]">
                  <v-card flat small class="mx-auto pa-0 mt-4">
                    <!--smileys from very sad to happy based on numbers from 1-5-->
                    <v-icon v-if="tracked[date] == 1" color="red"
                      >mdi-emoticon-dead</v-icon
                    >
                    <v-icon v-else-if="tracked[date] == 2" color="pink"
                      >mdi-emoticon-sad</v-icon
                    >
                    <v-icon v-else-if="tracked[date] == 3" color="orange"
                      >mdi-emoticon-neutral</v-icon
                    >
                    <v-icon v-else-if="tracked[date] == 4" color="yellow"
                      >mdi-emoticon-happy</v-icon
                    >
                    <v-icon v-else-if="tracked[date] == 5" color="green"
                      >mdi-emoticon-excited</v-icon
                    >
                  </v-card>
                </template>
              </v-row>
            </template>
          </v-calendar>
        </v-sheet>
      </v-col>
    </v-row>
    <v-row> <v-col>Wie geht es Ihnen heute? </v-col> </v-row>
    <v-row class="mx-auto pa-3">
      <v-col>
        <v-icon color="red" @click="setEmotion(1)">mdi-emoticon-dead</v-icon>
      </v-col>
      <v-col>
        <v-icon color="pink" @click="setEmotion(2)">mdi-emoticon-sad</v-icon>
      </v-col>
      <v-col>
        <v-icon color="orange" @click="setEmotion(3)"
          >mdi-emoticon-neutral</v-icon
        >
      </v-col>
      <v-col>
        <v-icon color="yellow" @click="setEmotion(4)"
          >mdi-emoticon-happy</v-icon
        >
      </v-col>
      <v-col>
        <v-icon color="green" @click="setEmotion(5)"
          >mdi-emoticon-excited</v-icon
        >
      </v-col>
      <v-col>
        <v-icon v-if="tracked[date] == 1" color="red">mdi-emoticon-dead</v-icon>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "Startseite",
  data: () => ({
    today: new Date(),
    tracked: {
      "2022-10-05": 1,
      "2022-10-06": 2,
      "2022-10-07": 3,
      "2022-10-08": 4,
      "2022-10-09": 5,
    },
    name: "",
    versicherungsnummer: "",
  }),
  mounted() {
    this.name = localStorage.getItem("name");
    let localTracked = localStorage.getItem("tracked");
    if (localTracked) {
      this.tracked = JSON.parse(localTracked);
    }
  },
  methods: {
    setEmotion(emotion) {
      let year_month_date = this.today.toISOString().split("T")[0];

      this.tracked[year_month_date] = emotion;
      this.tracked = JSON.parse(JSON.stringify(this.tracked));
      localStorage.setItem("tracked", JSON.stringify(this.tracked));
    },
  },
};
</script>
