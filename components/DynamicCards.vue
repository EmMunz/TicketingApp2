<template>
<div>
   <div>a
<!-- v-for is like a for loop it loops through an array it enables us to display things according to the number of elements we have in the array  -->
    <div v-for="(item,index) in ticketArray" :key="index">
<!-- We are creating a row because we want to have rows of our data -->
  
       <v-col cols="12" md="4">
             <v-card>
               <v-card-title>{{item.Description}}</v-card-title>
                <v-card-subtitle>{{item.name}}</v-card-subtitle>
                 <v-card-text>{{item.TicketInfo}}</v-card-text>
            </v-card>
       </v-col>
      
   
    </div>
  <v-card>
   <v-card-title>Please log in your ticket</v-card-title>
   <!-- The v-model links to the variables that will store the data in the text-fields  -->
    <v-text-field v-model="name" label="Please enter your name">
    </v-text-field>
    <v-text-field 
    v-model="Description" 
    label="Description">
    </v-text-field>
    <v-text-field 
    v-model="TicketInfo" 
    label="TicketInfo">
    </v-text-field>
    <!-- Right upon clicking the button the submit function is called, and all the instructions are executed in this function -->
    <v-btn dense rounded color="primary" @click="submit()">Submit</v-btn>
  </v-card>
   </div>
</div>
</template>
<script>
export default {
    data(){
        return{
        //Creating variables that will store the data in the text fields
        name:null,
        Description: null,
        TicketInfo: null,
        //we are getting the object and pushing it into the ticket array
        ticketArray:[]
        }
    },
    methods: {
    //When the submit function is called the data fields in it are pushed into the ticket array
        submit(){
    //A local variable has been declared and contains data for the object
        let objectData={
         name:this.name,
         Description:this.Description,
         TicketInfo:this.TicketInfo
        }
    //We are going to use the array to push the object data, we are basically pushing data into the array
    this.ticketArray.push(objectData);
        }
    }
    }

</script>