<template>
  <main>
    <b-container fluid>
      <b-container>
        <div>
          <b-carousel
            id="carousel-1"
            v-model="slide"
            :interval="5000"
            controls
            indicators
            background="#ababab"
            style="text-shadow: 1px 1px 2px #333;"
            @sliding-start="onSlideStart"
            @sliding-end="onSlideEnd"
          >

            <b-carousel-slide
              img-src="https://res.cloudinary.com/ddg48u9sp/image/upload/v1597329134/sonya.jpg"
            ></b-carousel-slide>
            <b-carousel-slide
              caption="Omlin signe à Montpellier"
              img-src="https://res.cloudinary.com/ddg48u9sp/image/upload/v1597329134/cornelia.jpg"
            ></b-carousel-slide>
            <b-carousel-slide
              img-src="https://res.cloudinary.com/ddg48u9sp/image/upload/v1597329134/ep34.jpg"
            ></b-carousel-slide>
            <b-carousel-slide
              img-src="https://res.cloudinary.com/ddg48u9sp/image/upload/v1597329134/roy.jpg"
            ></b-carousel-slide>
            <b-carousel-slide
              img-src="https://res.cloudinary.com/ddg48u9sp/image/upload/v1597329134/faiza.jpg"
            ></b-carousel-slide>
          </b-carousel>
        </div>
        <b-button v-on:click="openCloudinaryWidget" class="OrangeCustom">Upload</b-button>
        <!--
        <b-row align-v="center">

          <b-col lg="4" md="4" sm="12" xs="12" class="test">One of three columns</b-col>
          <b-col lg="4" md="4" sm="12" xs="12" class="test">One of three columns</b-col>
          <b-col lg="4" md="4" sm="12" xs="12" class="test">One of three columns</b-col>
          <b-col lg="12" md="12" sm="12" xs="12"><b-button v-on:click="openCloudinaryWidget">Greet</b-button></b-col>
          <cld-image cloudName="ddg48u9sp" publicId="PNG_transparency_demonstration_1_jjhsfx.png"  />
        </b-row>
        <b-embed
          type="video"
          aspect="16by9"
          src="https://res.cloudinary.com/ddg48u9sp/video/upload/v1597956988/Generique_light.mp4"
          allowfullscreen
          controls
        ></b-embed>-->
        <cld-video public-id="Generique_light"   controls="controls" width="100%">
        </cld-video>

      </b-container>
    </b-container>

  </main>
</template>
<script>


export default {
  layout: 'navbar',
  data (){
    return {
      slide: 0,
      sliding: null,
    }
  },
  async fetch(){
    /*const url = this.$cloudinary()
      .url('sample', { crop: 'scale', width: 200 })*/
  },
  head () {
    return {
      title: 'DataMHSC',
      script : [{src: 'https://widget.cloudinary.com/v2.0/global/all.js'}]
    }
  },
  components:{
  },
  methods:{
    openCloudinaryWidget(){
      const widget = this.createCloudinaryWidget()
      widget.open()
    },
    createCloudinaryWidget() {
      const newWidget = cloudinary.createUploadWidget(
        {
          cloudName: "ddg48u9sp",
          uploadPreset: "wxpgd7vw",
          multiple: false,
          maxFiles: 5,
          cropping: true,
          croppingAspectRatio: 1,
          croppingCoordinateMode: "face",

        },
        (error, result) => {
          if (!error && result && result.event === "success") {
            console.log('Done! Here is the image info: ', result.info);
          }
          else{
            console.log(error,result)
          }
        }
      )
      return newWidget
    },
    onSlideStart(slide) {
      this.sliding = true
    },
    onSlideEnd(slide) {
      this.sliding = false
    }
  }
}
</script>

<style scoped>

#carousel-1{
  border: 1px solid;
  border-image: linear-gradient(180deg, rgba(10,46,83,1) 31%, rgba(255,149,0,1) 100%) 1;
}
.container {
  margin-top: 40px;
  //min-height: 100vh;
  //display: flex;
  //justify-content: center;
  //align-items: center;
  text-align: center;
}
.test{
  background-color: red;
}

.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
