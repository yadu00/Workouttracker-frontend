<template>
  <div class="container">
    <div class="box">
      <div class="profileimg">
        
                <v-icon size="100px">mdi-account-circle</v-icon>
<h1>Name</h1>
      </div>
      <div class="about">
        <p>About</p>
      </div>
      <div class="info">
      <p>Certification: {{ trainer.certification }}</p>
      <p>Experience: {{ trainer.experienceYears }}</p>
      <p>Mobile No: {{ trainer.mobile }}</p>
      <p>Email: {{ trainer.email }}</p>
      </div>
      <div class="button">
                <div class="rate">
                  <v-icon>mdi-currency-inr</v-icon><span style="font-size: 30px;font-weight: bolder;">1000</span>/month</div>
        <button id="paynow">Pay Now</button>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex';

export default {
  computed: {
    ...mapGetters(['getuser_id']),  // Map the getter directly
  },
  data(){
    return{
      trainer:{
        name: "",
        certification: "",
        experienceYears: "",
        mobile: "",
        email: "",
      },
    }
  },methods:{
    async viewTrainer() {
      try {
        const payload = {
          user_id: this.getuser_id,
        };
        const result = await this.$store.dispatch("User/viewtrainer", payload);
        if (result.success) {
          this.trainer = result.data;
        } else {
          alert(`Error: ${result.error}`);
        }
      } catch (error) {
        console.error("Error loading Trainer:", error);
      }
    },
  },mounted(){
    this.viewTrainer();
  }
}
</script>

<style scoped>
.container{
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.box{
  width: 50%;
  height: 80%;
  display: flex;
  flex-direction: column;
  border: 1px solid black;
  border-radius: 20px;
   justify-content: center;
  align-items: center;
}
.profileimg{
  width: 100%;
  height: 20%;
  display: flex;
  justify-content: center;
  align-items: center;
  border-top-right-radius: 20px;
    border-top-left-radius: 20px;

}
.about{
  width: 100%;
  height: 30%;
  display: flex;
  flex-direction: column;
  background-color: rgb(178, 171, 185);
  /* align-items: center; */
  font-size: larger;
    padding: 10px 30px;


  
}
.info{
  width: 100%;
  height: 30%;
  display: flex;
  flex-direction: column;
  background-color: rgb(249, 249, 249);
  padding: 10px 30px;
  font-size: larger;
}
.button{
  width: 100%;
  height: 20%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
 

}
.rate{
  display: flex;
  align-items: center;
}
#paynow{
   width: 20%;
  height: 45%;
   border-radius: 35px;
    background-color: blue;
    color: white;
}
</style>