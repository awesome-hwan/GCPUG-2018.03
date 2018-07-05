<template>

<b-container class="bv-example-row" style="">
    <b-navbar toggleable="md" type="dark" variant="info">

  <b-navbar-toggle target="nav_collapse"></b-navbar-toggle>
  <b-navbar-brand href="#">NavBar</b-navbar-brand>

  <b-collapse is-nav id="nav_collapse">

    <b-navbar-nav>
      <b-nav-item href="#">Link</b-nav-item>
      <b-nav-item href="#" disabled>Disabled</b-nav-item>
    </b-navbar-nav>

    <!-- Right aligned nav items -->
    <b-navbar-nav class="ml-auto">

      <b-nav-form>
        <i class="fas fa-address-book"></i>
        <b-form-input size="sm" class="mr-sm-2" type="text" placeholder="Search"/>
        <b-button size="sm" class="my-2 my-sm-0" type="text">Search</b-button>
      </b-nav-form>

      <b-nav-item-dropdown text="Lang" right>
        <b-dropdown-item href="#">EN</b-dropdown-item>
        <b-dropdown-item href="#">ES</b-dropdown-item>
        <b-dropdown-item href="#">RU</b-dropdown-item>
        <b-dropdown-item href="#">FA</b-dropdown-item>
      </b-nav-item-dropdown>

      <b-nav-item-dropdown right>
        <!-- Using button-content slot -->
        <template slot="button-content">
          <em>User</em>
        </template>
        <b-dropdown-item href="#">Profile</b-dropdown-item>
        <b-dropdown-item href="#">Signout</b-dropdown-item>
      </b-nav-item-dropdown>
    </b-navbar-nav>

  </b-collapse>
</b-navbar>

<!-- navbar-1.vue -->
    <b-row>
        <b-col sm="9">
          <b-container fluid>
              <b-row class="my-1">
                <b-col sm="3">
                 <input id="input-large1" name="hash" v-model="hash.tag1" size="lg" type="text" placeholder="Enter your name" v-on:keyup.enter="passHash1">                 
                </b-col>
                <b-col sm="3">
                 <input id="input-large2" name="hash" v-model="hash.tag2" size="lg" type="text" placeholder="Enter your name" v-on:keyup.enter="passHash2">                 
                </b-col>
                <b-col sm="3">
                 <input id="input-large3" name="hash" v-model="hash.tag3" size="lg" type="text" placeholder="Enter your name" v-on:keyup.enter="passHash3">                 
                </b-col>
                <b-col sm="3">
                 <input id="input-large4" name="hash" v-model="hash.tag4" size="lg" type="text" placeholder="Enter your name" v-on:keyup.enter="getHash">                 
                </b-col>
              </b-row>
          </b-container>
            <div>
              <b-form-textarea id="textarea1"                              
                              placeholder="Enter something"
                              :rows="27"
                              v-model="text"
                              :max-rows="27">
                              
              </b-form-textarea>
            </div>
          </form>
          <i class="fas fa-address-book"></i>
        </b-col>
        
        <b-col sm="3">
         <div class="box" v-for="data in datalist">
         <!-- <div class="box" > -->
          <b-card title >{{ data.title }} 
            <p class="card-text">
              {{ data.body }}
              </p>
              </b-card>
            </div>
        </b-col>
    </b-row>
</b-container> 
</template>
<script defer src="https://use.fontawesome.com/releases/v5.0.9/js/all.js" integrity="sha384-8iPTk2s/jMVj81dnzb/iFR2sdA7u06vHJyyLlAd4snFpCl/SnyUjRrbdJsw1pGIl" crossorigin="anonymous"></script>
<script>

export default {

  
  data:   function data() {    
    return   {
          hash: [
            {tag1: ''},
            {tag2: ''},
            {tag3: ''},
            {tag4: ''}
          ],
          datalist: [],
          text: ''
        } 
    },
    methods: {
    

    getHash () {
    
     console.log(this.hash.tag1, this.hash.tag2, this.hash.tag3, this.hash.tag4);
     
     this.$http.get(`http://35.189.132.166:5000/setting?tag=java&tag=android&tag=camera&tag=save`) 
     this.$http.get(`http://35.189.132.166:5000/setting?tag= #{this.hash.tag1} &tag= #{this.hash.tag2} &tag= #{this.hash.tag3} &tag= #{this.hash.tag4} `) 
     //  this.$http.get('http://35.189.132.166:5000/setting?tag='+this.hash.tag1+'&tag='+this.hash.tag2+'&tag='+this.hash.tag3+'&tag='+this.hash.tag4 )
     .then(function(response) {
       console.log(response)
        return response.json();        
     })
     .then(data => {
       this.datalist = Object.values(data);
       console.log( Object.values(data))
     })     
     .catch(function(error){
      console.log(error)
     })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  max-width:100%;
}
.col-sm-12 {
  padding: 0;
  padding-top:5px;
}

.col-sm-9 {
  margin-left: 5px;
}

.col-sm-3 {
  margin-left: -10px;
  height:100%;
  padding-right: 0px;
}

.bg-light {
  margin-right: -15px;
  margin-left: -15px;
  height: 45px;
  background-color:#f7b731 !important;
}

.navbar-brand {
  margin-left: 45%;
}

.form-control:focus {
  box-shadow:none;
  border-color:none;
}

.row {
  background-color:white;
  flex-wrap: nowrap;
}

#textarea1 {
  margin-top: 8px;
  margin-bottom: 15px;
}

#textarea3 {
  background-color: #d2dae2;
  height: 622px;
}

.form-control-lg {
  margin-top: 6px;
}

#input-large {
  margin-top: 4px;
  width: 100%;
  display: block;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height:1.5;
  color:#495057;
  background-clip:padding-box;
  border: 1px solid #cde4da;
  border-radius: 0.25rem;
  transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}

#input-large:focus {
  border-color: none;
}

.col-sm-9 {
  margin-left: 5px;
}

.col-sm-3 {
  margin-left: -10px;
  height:100%;
}

.bg-info {
  margin-right: -15px;
  margin-left: -15px;
  height: 45px;
}

.form-control:focus {
  box-shadow:none;
  border-color:none;
}

.row {
  background-color:#d1d8e0;
  flex-wrap: nowrap;
}

#textarea1 {
  margin-top: 8px;
  margin-bottom: 30px;
}

.form-control-lg {
  margin-top: 6px;
}

#input-large {
  margin-top: 4px;
  width: 100%;
  display: block;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height:1.5;
  color:#495057;
  background-clip:padding-box;
  border: 1px solid #cde4da;
  border-radius: 0.25rem;
  transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}


</style>

