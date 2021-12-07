<template>
    <div id="wrapper2" class="wiki-wrapper" > 
      <t1>{{ this.city }}</t1>
      <p class="articleW"> {{ this.article }} </p>
      <a class="clicker" @click="readArticle()">
          <img class="clicker" src="../assets/play.png" style="width:30px; height: auto;"/>
      </a>
    </div>
</template>

<script>
export default {
    name: 'Article',

    methods: {

        // Fetch function for wikipedia article
        getArticle (ort) {
      
            const wtf = require('wtf_wikipedia')

            wtf.fetch(ort, 'de').then((doc) => {
                this.setArticle(doc.sections()[0].text());

            })

            this.city = ort;
            this.$forceUpdate();
        },

        // set fetched article as variable
        setArticle (result) {
            this.article = result;
            console.log(this.article);
        },

        //Text to speech synthesis of article
        readArticle(){
            let synth = window.speechSynthesis;
            let textToRead = this.article;

            let utterThis = new SpeechSynthesisUtterance(textToRead);

            utterThis.lang = 'de-DE';

            if(synth.speaking){
                synth.cancel();
            }
            else{
                synth.speak(utterThis);
            }
        }
    }
}
</script>

<style scoped>
    
    #wrapper2 {
    display: inline-block;
    padding: 10px 25px;
    background-color: rgba(0 , 0, 0, 0.7);
    border-radius: 20px;
    margin: 30px 0px;

    box-shadow: 3px 4px rgba(0, 0, 0, 0.3);

    color: whitesmoke;
    }

    t1 {
        font-size: 25px;
        text-decoration: underline whitesmoke;
        padding-bottom: 100px;
    }

    .clicker {

        margin-bottom: 7px;
        cursor: pointer;
    }


</style>