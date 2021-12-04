<template>
    <div id="wrapper2" class="wiki-wrapper">
      <t1></t1>
      <div class="articleW"> {{ this.article }} </div>
      <a>
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

        this.$forceUpdate();
        },

        setArticle (result) {
            this.article = result;
            console.log(this.article);
        },
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
    }

</style>