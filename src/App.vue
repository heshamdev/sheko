<template>
  <div id="app" style=" display: flex; min-height: 63vh; flex-direction: column;">
    <div class="container" style="flex: 1 0 auto;">
      <div v-if="!Encrypt && !Decrypt">
        <ul>
          <li><h4>Project Security</h4></li>
          <li><h4>Student Name : Mohamed Ibrahim</h4></li>
          <li><h4>TA : Salma Roshdy</h4></li>
        </ul>
        <img src="shekoandhesham.jpg" width="300" v-if="true">
      </div>
      <div class="row center" v-if="!Encrypt && !Decrypt" style="padding-top: 100px;">
        <div class="col s12 push-s2">
          <a class="waves-effect waves-light btn indigo darken-4 col" @click="Encrypt = true; Decrypt = false">Encryption</a>
          <a class="waves-effect waves-light btn indigo darken-4" @click="Decrypt = true ;Encrypt = false">Decryption</a>
        </div>
      </div>
     <div v-if = "Encrypt">
       <div v-if= "!flage">
        <div class="row">
        <h3>Sheko Encryption :)</h3>
          <div class="input-field col s12">
            <textarea id="textarea2" v-model="textarea2" class="materialize-textarea" data-length="120"></textarea>
            <label for="textarea2">Your Message !</label>
        </div>
      </div>
  
      <div class="row">
         <div class="input-field col s12">
            <input id="input_text" type="text" v-model="monoKey" data-length="10">
            <label for="input_text">Please Enter The Key !</label>
          </div>
          <div class="col s12"> <a class="waves-effect waves-light btn indigo darken-4" @click="monoEncryption">Send</a></div>
      </div>
  </div>
<div class="preloader-wrapper active" v-if = "flage2">
    <div class="spinner-layer spinner-red-only">
      <div class="circle-clipper left">
        <div class="circle"></div>
      </div><div class="gap-patch">
        <div class="circle"></div>
      </div><div class="circle-clipper right">
        <div class="circle"></div>
      </div>
    </div>
  </div>
  <div v-if = "flage1">
    <h3 class="center">The Result</h3>
      <ul>
        <li><strong>Cipher Text :</strong> {{ cipher_text }}</li>
        <li><strong>Key :</strong> {{ monoKey }}</li>
      </ul>
  </div>
     </div>
     <div v-if="Decrypt">
       <div v-if= "!flage">
        <div class="row">
        <h3>Sheko Decryption :)</h3>
          <div class="input-field col s12">
            <textarea id="textarea2" v-model="textarea2" class="materialize-textarea" data-length="120"></textarea>
            <label for="textarea2">Your Message !</label>
        </div>
      </div>
  
      <div class="row">
         <div class="input-field col s12">
            <input id="input_text" type="text" v-model="monoKey" data-length="10">
            <label for="input_text">Please Enter The Key !</label>
          </div>
          <div class="col s12"> <a class="waves-effect waves-light btn indigo darken-4" @click="monoDecryption">Send</a></div>
      </div>
  </div>
<div class="preloader-wrapper active" v-if = "flage2">
    <div class="spinner-layer spinner-red-only">
      <div class="circle-clipper left">
        <div class="circle"></div>
      </div><div class="gap-patch">
        <div class="circle"></div>
      </div><div class="circle-clipper right">
        <div class="circle"></div>
      </div>
    </div>
  </div>
  <div v-if = "flage1">
    <h3 class="center">The Result</h3>
      <ul>
        <li><strong>Cipher Text :</strong> {{ cipher_text }}</li>
        <li><strong>Key :</strong> {{ monoKey }}</li>
      </ul>
  </div>
   <div v-if = "flage7">
    <h3 class="center">The Result</h3>
      <ul>
        <li><strong>Plain Text :</strong> {{ plain_text }}</li>
        <li><strong>Key :</strong> {{ monoKey }}</li>
      </ul>
  </div>
     </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
require('howler');
export default {
  name: 'app',
  components: {
    HelloWorld
  },
  head : {
    title : 'Sheko | Encryption'
  },
  data() {
    return {
      textarea2 : '',
      cipher_text : '',
      monoKey : '',
      plain_text : '',
      flage : false,
      flage1 : false,
      flage2 : false,
      flage7 : false,
      Decrypt : false,
      Encrypt : false
    }
  },
  methods :{
    monoEncryption(){  
     const vm = this
     vm.flage2 = true;
     vm.flage = true;
        setTimeout(()=>{
         vm.cipher_text = '';
         var alphabetic = ['A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z'];
         let i;
         let j;
         let m;
         let MKey = vm.monoKey;
         var orginal_index;
         var new_index;
         var PlainText = vm.textarea2.toUpperCase();

         if(MKey.length == 26){
         for(i=0; i < PlainText.length; i++){
            for(j=0; j < alphabetic.length; j++)
            {
              if(PlainText.charAt(i) == " "){
                vm.cipher_text = vm.cipher_text + " ";
              }
              if(PlainText.charAt(i) == alphabetic[j]){
                 vm.cipher_text = vm.cipher_text + MKey.charAt(j);
                
              }
            }

         } 
       }else if(MKey.length < 26 && MKey.length > 0){
        for(m=0; m < alphabetic.length; m++)
        {
            MKey = MKey.toUpperCase();
          if(!(MKey.includes(alphabetic[m]))){
             MKey = MKey + alphabetic[m];
          }
        }
           for(i=0; i < PlainText.length; i++){
            for(j=0; j < alphabetic.length; j++)
            {
              if(PlainText.charAt(i) == " "){
                vm.cipher_text = vm.cipher_text + " ";
              }
              if(PlainText.charAt(i) == alphabetic[j]){
                 vm.cipher_text = vm.cipher_text + MKey.charAt(j);
                
              }
            }

         } 
       }else{
          console.log('error');
       }
       vm.flage2 = false
        vm.flage1 = true;

        },3000);
          
         
          
            },
            monoDecryption(){  
     const vm = this
     vm.flage2 = true;
     vm.flage = true;
        setTimeout(()=>{
         vm.cipher_text = '';
         var alphabetic = ['A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z'];
         let i;
         let j;
         let m;
         let MKey = vm.monoKey;
         var orginal_index;
         var new_index;
         var CipherText = vm.textarea2.toUpperCase();
         if(MKey.length == 26){
         for(i=0; i < CipherText.length; i++){
            for(j=0; j < MKey.length; j++)
            {
              if(CipherText.charAt(i) == " "){
                vm.plain_text = vm.plain_text + " ";
              }
              if(CipherText.charAt(i) == MKey[j]){
                console.log('key : '+MKey[j]+' :'+j);
                console.log('cipher : '+ CipherText.charAt(i)+' :'+i);
                 vm.plain_text = vm.plain_text + alphabetic[j];
                
              }
            }

         } 
       }else if(MKey.length < 26 && MKey.length > 0){
        for(m =0; m < alphabetic.length; m++)
        {
          MKey = MKey.toUpperCase();
          if(!(MKey.includes(alphabetic[m]))){
             MKey = MKey + alphabetic[m];
          }
        }
           for(i=0; i < CipherText.length; i++){
            for(j=0; j < MKey.length; j++)
            {
              if(CipherText.charAt(i) == " "){
                vm.plain_text = vm.plain_text + " ";
              }
              if(CipherText.charAt(i) == MKey[j]){
                 vm.plain_text = vm.plain_text + alphabetic[j];
                
              }
            }

         } 
       }else{
          console.log('error');
       }
       vm.flage2 = false;
       vm.flage7 = true;
},3000);
          
         
          
            }
  },
  mounted(){
   var sound = new Howl({
                src: './theweeknd.mp3',
                autoplay: true,
                loop: true,
                volume: 0.5,
                onend: function() {
                    console.log('Finished!');
                }
            });
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.preloader-background {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #eee;
  
  position: fixed;
  z-index: 100;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;  
}

</style>
