<template>
  <div >

<div  id="frame1">
  <label for="fname">Name:</label><br>
  <input type="text" id="fname" class="form-control" v-model="userData.name"><br><br>
  <label for="lname">Age:</label><br>
  <input type="number" id="age" name="age" v-model.number="userData.age"><br><br>
  <label for="salary">Salary:</label><br>
  <input  type="number" id="male" name="salary" step="any" min="0" v-model.number="userData.salary"><br><br>
<label for="Programer">Software engineer</label><br>
<input type="checkbox" id="vehicle1" name="vehicle1" value="true" v-model.number="userData.programer"><br><br>

<label for="Letter">Favorite Letter:</label><br>
<input type="text" id="FLetter" name="FLetter" maxlength="1"  v-model.number="userData.letter">
<br><br>

<div class="card" v-if="isSubmitted">
    <div class="card-body">
        <h4 class="card-title">Result</h4>
 
          <p ><b>{{ stringChain }}</b></p>
    </div>
</div>
<button class="btn btn-primary"
        @click.prevent="getData">Submit!
</button>
</div> <br><br>
<div  id="frame1" v-if="isSubmitted">
  <label for="fname2">Result Edit:</label><br>
  <input type="text" id="fname2" class="form-control" v-model="userData.result"><br><br>
<br><br>

<button class="btn btn-primary"
        @click.prevent="setData">Submit edit!
</button>

</div>
 

  </div>
  
</template>

<script>
    export default {
        data() {
            return {
                 userData: {
                    name: '',
                    age: 0,
                    salary : 0.0,
                    programer : true,
                    letter : '',
                    result : ''
                },Subited:{
                  name: '',
                    age: 0,
                    salary : 0.0,
                    programer : true,
                    letter : '',
                    result : ''
                },
                isSubmitted: false,
                stringChain: ''
            }
        },methods: {
            getData() {
               this.isSubmitted = true;
               this.stringChain = this.userData.name + "|" + this.userData.age + "|" + this.userData.salary + "|" + this.userData.programer + "|" + this.userData.letter;
               this.userData.result = this.stringChain;
               var model = this.userData;
               sessionStorage.setItem("Sended",JSON.stringify(this.userData));
               this.Subited = model;
            },
            setData(){
              var subited = JSON.parse(sessionStorage.getItem("Sended"));
              var dataSplit = this.userData.result.split('|');
              this.userData.name = dataSplit[0];
              this.userData.age = parseInt(dataSplit[1]);
              this.userData.salary = parseFloat(dataSplit[2]);
              this.userData.programer = (dataSplit[3]=="true");
              this.userData.letter = dataSplit[4];
              debugger;
              if(!(this.validateData(subited))){
                  alert('Data changed');
              }
              this.isSubmitted = false;
            },
            validateData(data){
              debugger;
              if(data.name == this.userData.name && 
              data.age == this.userData.age &&
              data.salary == this.userData.salary &&
              data.programer == this.userData.programer &&
              data.letter == this.userData.letter
              ){
                return true;
              }else{
                return false;
              }
            }
        }
    }



</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#frame1{
  text-align: left;
  align-content: left;
}
</style>
