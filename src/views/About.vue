<style scoped>

h1 {
    margin-bottom: 1vw;
}
.office-img{
  margin:50px;
}
.bold {
    -webkit-text-stroke-width: medium;
}

.about-card {
  max-width:900px;
}

.v-card {
    display: inline-block;
}

.margin {
    margin: 10px !important;
}

.mx-auto {
    margin-top: 10vw;
    margin-bottom: 10vw;
}

.v-image {
    z-index: 0;
}
.pleads {
  width: 50%;
}

.col-b {
    width: 33%;
    display: -webkit-inline-box;
    -webkit-box-pack: center;
}

.col-100 {
    width: 100%;
}

p {
    display: inline;
    text-align: left !important;
}

h4 {
    text-align: left;
    color: #313233;
}

.text-center {
    text-align: center;
}

.gray {
    color: gray;
}
.fav {
  height: 50px;
  width: 50px;
}
</style>

<template>

<v-card class="mt-5 mb-5 about-card">
    <v-img class="center fav" src="@/assets/graphics/finetting.png" />
    <v-card-text class="text-justify font-weight-medium  text-body-2">

        <br>
        <v-divider class="mb-5"></v-divider>
        <div class="pt-10">
        <br>

        <hr>
        <h4 class="mt-10">
          <b>Project objective:</b>
        </h4>
        <br>
            <br> <b> Create a social community  </b> a place where you can share your thoughs and ideas to other investors and fintech enthusiasts, our platform target is specific to fintech industry.

        <hr>
        <h4 class="mt-10"><b>Why we are different from other social platforms?</b></h4>
        <br>
      </div>
        <br>
        <v-list-item>
            <v-list-item-content>
              <v-list-item> ● We are trying to build a fintech community that is non-toxic  </v-list-item>
              <v-list-item> ● We offer a free to use product because we care about others. </v-list-item>
              <v-list-item> ● We listen to feedback. </v-list-item>
              <v-list-item> ● We are interested in our users ideas and thougths. </v-list-item>
              <v-list-item> ● We offer you a place to build your network specific to fintech sector </v-list-item>
            </v-list-item-content>
        </v-list-item>
        icons: <a href="https://www.flaticon.com/free-icons/fintech" title="fintech icons">Fintech icons created by berkahicon - Flaticon</a>
        <hr>
        <h4 class="mt-10"><b>Project leads:</b></h4>
        <br>

        <br>
    </v-card-text>
    <v-row>
          <v-col cols="6" >
              <div>
                  <v-img
                  alt="Abraham Felix"
                  class="pleads center rounded-lg"
                  src="@/assets/ab-felix.png"
                   />
              </div>
              <div>
               <p><b> <a target="_blank" href="https:/www.github.com/abraham-felix"> Abraham Felix</a> </b></p>
               <br>
               <p> Front-end  </p>
               <br>
               <p><b>Mexico</b></p>
              </div>
          </v-col>
          <v-col cols="6">
              <div >
                  <v-img
                  alt="Abraham Felix"
                  class="pleads center rounded-lg"
                  src="@/assets/kevin-naf.jpg"
                    />
              </div>
              <div>
              <p> <b> <a target="_blank" href="https:/www.github.com/kevinnafziger"> Kevin Nafziger </a> </b></p>
              <br>
              <p> CEO & Back-end </p>
              <br>
              <p><b>USA</b></p>
             </div>
           </v-col>
          <br>
          <br>
          </v-row>
</v-card>

</template>
