<template>
  <v-container>
    <!--add header-->
    <v-container fluid>
      <v-row dense>
        <v-col v-for="f in food" :key="f.title" :cols="3">
          <v-card>
            <v-img
              :src="f.src"
              class="white--text align-end"
              height="200px"
              width="275px"
            >
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
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      food: [
        {
          title: "Vitamin B12",
          src: "https://media.istockphoto.com/photos/man-writing-word-b12-on-chalkboard-picture-id1137347719?k=20&m=1137347719&s=612x612&w=0&h=HEuK4eRSudWFj257LZFTFtSKfGQnqq_jCsOrPPURbQk=",

          stress: 1,
          concentration: 5,
        },
        {
          title: "Vitamin B1",
          src: "https://media.istockphoto.com/vectors/vitamin-drop-b1-thiamine-pill-capsule-realistic-b1-thiamine-vitamin-vector-id1403794269?k=20&m=1403794269&s=612x612&w=0&h=VtnlM-liTtrf9zTFBCezG-drCdjk_8GQrycsmh7U0l4=",

          stress: 1,
          concentration: 5,
        },
        {
          title: "Vitamin B3",
          src: "https://media.istockphoto.com/photos/protection-from-illness-concept-on-blue-background-picture-id1214709586?k=20&m=1214709586&s=612x612&w=0&h=aNqfEKRnCKgJDP4Ylvi-6mqddmkzqlGlFTWfjCRtLH0=",

          stress: 1,
          concentration: 5,
        },
        {
          title: "Vitamin B6",
          src: "https://media.istockphoto.com/photos/man-writing-words-vitamin-b6-on-chalkboard-vitamin-b6-concept-picture-id1186174795?k=20&m=1186174795&s=612x612&w=0&h=tce7t4dFJaraRewXfaFl85QC1a8t_tdMATLwhTjo8qs=",

          stress: 1,
          concentration: 5,
        },

        {
          title: "Vitamin B9",
          src: "https://media.istockphoto.com/vectors/vitamin-b9-green-vector-id1389582766?k=20&m=1389582766&s=612x612&w=0&h=j1-_7xhZtXQls0Sm87P9qYdlhJwcymwGvXOwbQxEJrM=",

          stress: 1,
          concentration: 5,
        },
        {
          title: "Vitamin C",
          src: "https://media.istockphoto.com/vectors/vitamin-gold-shining-pill-capsule-icon-ascorbic-acid-shining-golden-vector-id1292419523?k=20&m=1292419523&s=612x612&w=0&h=ojSCl-pTUuElRWVj9WJLPgnajkePxQ9N25VUggnQsAA=",

          stress: 3,
          concentration: 4,
        },
        {
          title: "Omega-3",
          src: "https://media.istockphoto.com/photos/symbol-for-healthy-food-hand-turns-dice-and-changes-the-expression-6-picture-id1342287725?k=20&m=1342287725&s=612x612&w=0&h=p1APgQlW-CKsLpmW9hWW3vESmpzzBodtcmvLvUHF-LM=",

          stress: 4,
          concentration: 4,
        },
        {
          title: "Magnesium",
          src: "https://media.istockphoto.com/vectors/magnesium-vector-id1395554975?k=20&m=1395554975&s=612x612&w=0&h=lZG3z9QYTk48k7YY88nkh9-MVaG2qtEbS3R6-NgHtv8=",

          stress: 4,
          concentration: 3,
        },
        {
          title: "Kalium",
          src: "https://media.istockphoto.com/photos/potassium-written-red-heart-shape-on-blue-background-picture-id1252801766?k=20&m=1252801766&s=612x612&w=0&h=NSYvgNqLHPGyhIKEuyBrybvwEQQsoQ6bMFzh8dL5H9o=",

          stress: 4,
          concentration: 2,
        },
        {
          title: "Zink",
          src: "https://media.istockphoto.com/vectors/zinc-scientific-medical-research-vector-id1160757141?k=20&m=1160757141&s=612x612&w=0&h=dRZBWKa67YMAGPwBscLaQtwqdbGr4FQhnAcmaVZVv2s=",

          stress: 4,
          concentration: 4,
        },
        {
          title: "Eisen",
          src: "https://media.istockphoto.com/photos/iron-symbol-made-from-pills-on-purple-background-top-view-with-copy-picture-id1327526110?k=20&m=1327526110&s=612x612&w=0&h=48PcitQ0nnRGUC_erqM89CGv0DCp8IqoPsrIKxXFE7Y=",

          stress: 4,
          concentration: 4,
        },
        {
          title: "Selen",
          src: "https://media.istockphoto.com/vectors/mineral-se-selenium-blue-shining-pill-capsule-icon-substance-for-vector-id1346203274?k=20&m=1346203274&s=612x612&w=0&h=CjAh5NqjvHENYPWp5Og_k0cknjuGRdf8HWDTJl5dBWQ=",

          stress: 4,
          concentration: 4,
        },
        {
          title: "Vitamin E",
          src: "https://media.istockphoto.com/vectors/vitamin-e-icon-in-flat-style-pill-capsule-vector-illustration-on-vector-id1268157241?k=20&m=1268157241&s=612x612&w=0&h=AFwt_I45i13HDybiaAsA_MTGrNC3_qtrPm5z302xibc=",

          stress: 4,
          concentration: 3,
        },
      ],
    };
  },
  computed: {},
};
</script>
