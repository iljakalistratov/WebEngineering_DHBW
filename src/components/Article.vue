<template>
    <div id="wrapper2" class="wiki-wrapper" v-if="typeof this.article != 'undefined'"> 
      <t1>{{ this.city }}</t1>
      <div class="articleW"> {{ this.article }} </div>
      <a @click="readArticle()">
          <img src="../assets/play.png" style="width:30px; height: auto;"/>
      </a>
    </div>
</template>

<script>
export default {
    name: 'Article',

    methods: {
        getArticle (ort) {
      
            const wtf = require('wtf_wikipedia')

            wtf.fetch(ort, 'de').then((doc) => {
                this.setArticle(doc.sections()[0].text());

            })

        this.city = ort;
        this.$forceUpdate();
        },

        setArticle (result) {
            this.article = result;
            console.log(this.article);
        },

        readArticle(){

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


</style>