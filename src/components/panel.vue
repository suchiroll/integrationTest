<template>
  <div class="wrapper">
   <div class = "panel" v-for="(item, index) in info.content" >
      <div class = "imagediv" ><img class = "image" v-bind:src = "info.content[index].main_image_url+'?w=400&h=270'"> </div>

      <div class = "title"><p> <a v-bind:href = "info.content[index].original_url"> {{info.content[index].title}} </a> </p> </div>
    </div>
  </div>
</template>

<script>
import JQuery from 'jquery';
let $ = JQuery;
import axios from 'axios';
var jsonp = require('jsonp');

export default {
  name: 'panel',
 
  data(){
    return{
      info: []
    }
  },
 
  created() {
    console.log("createed");
    this.info = this.dataResult();
    }, 

    methods: {
      dataResult(){
      /*  $.getJSON('https://api.idio.co/1.0/content/.json?key=URN4QXKCG3QD3Y5MS51A&callback=', function(el){
            console.log("hkk");
            this.info = el;
        }.bind(this));*/

        jsonp('https://api.idio.co/1.0/content/.json?key=URN4QXKCG3QD3Y5MS51A&callback=', null, function(err,data){
            if(err){
              console.error(err.message);
            } else {
              this.info = data;
              console.log(this.info);
            }
        }.bind(this));
      },
    }
  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://fonts.googleapis.com/css?family=Roboto:900');

.panel{
  height: 500px;
  width: 400px;
  background-color: white;
  box-shadow: 0px 1px 5px #888888;
  display: inline-block;
   margin: 50px;
   overflow: hidden;
}

.image{
  background-color: gray;
  margin: 0px;
}

.imagediv{
  width: 400px;
  height: 270px;
}

.title{
 
  padding-right: 30px;
  font-family: 'Roboto', sans-serif;
  width: 100%;
  text-transform: uppercase;

}

a:hover{
  color: #FA48A7;
}

a{
  color: #262626;
  text-decoration: none;

}


p{
  padding-left: 30px;
  padding-right: 30px;
  font-size: 28px;
}
</style>
