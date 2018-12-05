<template>
  <div class="wrapper">
   <div class = "panel" v-for="(item, index) in info.content" > <!-- iterate through items in content arr -->
      <div class = "imagediv" ><img class = "image" v-bind:src = "info.content[index].main_image_url+'?w=400&h=270'"> </div> <!-- gets image url -->

      <div class = "title"><p> <a v-bind:href = "info.content[index].original_url"> {{info.content[index].title}} </a> </p> </div> <!-- gets link and title url -->
    </div>
  </div>
</template>

<script>
//require
var jsonp = require('jsonp');

export default {
  name: 'panel',
 
  data(){
    return{
      info: [] //to store info 
    }
  },
 
  created() {
    //set data
    this.info = this.dataResult();
    }, 

    methods: {
      //loading jsonp data from url to info 
      dataResult(){
        jsonp('https://api.idio.co/1.0/content/.json?key=URN4QXKCG3QD3Y5MS51A&callback=', null, function(err,data){
            if(err){
              console.error(err.message);
            } else {
              this.info = data;
              console.log(this.info); //just checking 
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
