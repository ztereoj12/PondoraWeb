<template>
  <div id="app" class="container bg-dark">
   
      <div class="page-header">
        <h1 style="color:white;">Pondora</h1>
      </div>
      <div class="panel panel-default">
        <div class="panel-heading">
          <h3>Add Data</h3>
        </div>
        <div class="panel-body">

          <form class="form-inline" v-on:submit.prevent="addData">
           
             <div class="form-group">
              <label style="font-size:20px;" for="miliseconds">Time:</label>
              <input type="text" class="form-control" name="" v-model="datas.miliSeconds">
            </div>
             <div class="form-group">
              <label style="font-size:20px;" for="temperature">Temperature:</label>
              <input type="text" class="form-control" name="" v-model="datas.Temperature">
            </div> 
            <input type="submit" class="btn btn-primary" name="add data">
          </form>
        </div>
      </div>

      <div class="panel panel-default">
        <div class="panel panel-heading">
          <h3>Data</h3>
        </div>
         <div class="container">
          <table class="table table-dark table-hover table-responsive-sm table-responsive-md table-responsive-lg table-responsive-xl table-striped table-bordered">
            <thead>
              <tr style="background-color: green;">
                
                <th style="text-align: center;font-size: 18px;">Miliseconds</th>
                <th style="text-align: center;font-size: 18px;">Temperature</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="da in data">
                
                <td style="text-align: center;font-size: 15px;color:violet;">{{da.miliSeconds}}</td>
                <td style="text-align: center;font-size: 15px; color:violet;">{{da.Temperature}}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    
  </div>
</template>

<script>
  import Firebase from 'firebase'

  let config = {
    apiKey: "AIzaSyCQTeFObAHohgcGIXUvGnBJIiNuBBWU2ZU",
    authDomain: "vuejs-firebase-e9f77.firebaseapp.com",
    databaseURL: "https://vuejs-firebase-e9f77.firebaseio.com",
    projectId: "vuejs-firebase-e9f77",
    storageBucket: "vuejs-firebase-e9f77.appspot.com",
    messagingSenderId: "1054693549509"
  }

  let app = Firebase.initializeApp(config);
  let db = app.database();
  
  
  var today = new Date();
  var today_string = today.toString();
  var month = today_string.substring(3,7);
  var day = today_string.substring(8,10);
  var year = today_string.substring(11,15);
  
  var format_date = month+" "+day+","+" "+year;

  // var dd = today.getDate();
  // var mm = today.getMonth()+1;
  // var yy = today.getFullYear();

  // if(mm < 10){
  //   mm='0'+mm;
  // }
  // today = mm+' '+dd+','+' '+yy;
  

  let dataRef = db.ref('chart/pond 1/' +' '+format_date );


export default {
  
  data () {
    return {
      
      datas:{
        miliSeconds:'',
        Temperature:''
      }
    }
  },
  firebase:{
    data:dataRef
  },
  methods:{
      addData:function(){
        dataRef.push(this.datas)
        this.datas.miliSeconds = '';
        this.datas.Temperature = '';
      }
   }
  }

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
input[type="submit"]{
  margin-left: 5px;
}
input[type="submit"]:hover{
  background-color: green;
  color: white;

}
</style>
