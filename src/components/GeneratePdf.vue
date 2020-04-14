<template>
  <div class="mainArea">
  

  <!-- about modal  -->
   
      <div class="container">
        <div class="col-md-10 offset-md-1">
             <textarea class="form-control" ref="userText" id="userText" placeholder="Start writing your note here!">

             </textarea>
       </div>

      </div>

Linebreaks PDF


    
    <div class="go-to-options">
      <ul>
        <li v-tooltip.right="'Home Page'"><a @click="goHome"><font-awesome-icon icon="sticky-note" /></a></li>
        <li v-tooltip.right="'When you finish your note click here to download it'"><a @click="generateYourFile"> <font-awesome-icon icon="download" /></a></li>
        <li v-tooltip.right="'About this tool, click to read!'"> <a @click="modalShow = !modalShow"> <font-awesome-icon icon="question" /></a></li>
      </ul>
    </div>
   
    <b-modal v-model="modalShow" hide-footer="true" id="modal-lg" size="lg"> 
      <h2>Online Notes Taker</h2>
      <p>This an online free tool to take notes speedily and cleanly way, there is no login required.</p>
      <p>How it works:</p>
      <ul>
        <li>* Write your notes.</li> <br>
        <li>* Save it using the download icon on the left(it will be saved as an pdf) </li>
      </ul>
      <p>This website is responsive so you can use it in all your devices..</p>
      <h3>Important:</h3>
      <p>We do not collect any of your notes in our database, so feel free and NOTE IT. </p>
      <router-link to="/contact">Contact US</router-link>

    </b-modal>


     

    <Footer />

  </div>
</template>

<script>
import jsPDF from "jspdf";
import Footer from "./Footer.vue"

 
 
 export default {
   name: 'GeneratePdf',
   props: {
    msg: String,
  },

  components: {
     Footer,
  },

  data() {
    return {
      modalShow: false,
    }
    
  },

   methods: {
     generateYourFile() {

       const pdf = new jsPDF();
       const date = new Date();


       // get data from input
       const entredData = this.$refs.userText.value;
       // file name
         const filename =
         "yourNote_" +
         date.getFullYear() +
         ("0" + (date.getMonth() + 1)).slice(-2) +
         ("0" + date.getDate()).slice(-2) +
         ("0" + date.getHours()).slice(-2) +
         ".pdf";
      if (entredData == 0) {
         alert('You did not write anything to be saved!')
       }
      else {

       pdf.text(entredData, 5, 10, {
          width: 200,
          maxWidth: 200,
          //align: 'justify'
          });
      
      pdf.save(filename);

      }
     },

     goHome(){
          this.$router.push('/')
     }
   },

 }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.go-to-options {
position: fixed;
top: 17px;
left: 45px;
z-index: 2;
background-color:#fff;
box-shadow: 0 0 13px 0#303030;
padding: 17px;
border-bottom-left-radius: 0;
border-top-left-radius: 0;
}

.go-to-options ul {
margin-top: 21px;
}

.go-to-options li {
  display: block;
  cursor: pointer;
  margin-bottom: 34px;
}

.go-to-options .svg-inline--fa:hover{
  border-bottom: 2px solid;
  
}

.go-to-options .svg-inline--fa {
    font-size: 4rem;
}
.mainArea textarea{
 height: 400px;
 border: 2px solid #2c3e50;
 margin-top: 15px;
 box-shadow: 0 0 13px 0#303030;
}
.modal-footer {
  display: none !important;
}
h3 {
  margin: 40px 0 0;
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
</style>
