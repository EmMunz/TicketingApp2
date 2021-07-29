<template>
<div>
    <v-dialog
      v-model="dialog"
      persistent
      max-width="600px"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          color="primary"
          dark
          small
          dense
          v-bind="attrs"
          v-on="on"
        >
          Create Ticket
        </v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span class="text-h5">Ticketing</span>
        </v-card-title>
        <v-card-text>
          <v-container>
                <!-- The v-model links to the variables that will store the data in the text-fields  -->
    <v-text-field 
    v-model="creator" 
    label="Please enter your name">
    </v-text-field>
    <v-text-field 
    v-model="issuedTo" 
    label="Receipient">
    </v-text-field>
    <v-text-field 
    v-model="Description" 
    label="Description">
    </v-text-field>
    <v-text-field 
    v-model="TicketInfo" 
    label="TicketInfo">
    </v-text-field>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="red darken-1"
            text
            @click="closeDialog()"  
          >
            Close
          </v-btn>
          <v-btn
            color="green darken-1"
            text
           @click="submit()"
          >
            Post
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
       <h2 class="display-3">Pending tickets</h2>
        
<!-- v-for is like a for loop it loops through an array it enables us to display things according to the number of elements we have in the array  -->
   
  
 <!-- class pl can move the proximity to the margins -->
     <v-row>
    <div id="cards" class="pl-4" v-for="(item,index) in ticketArray" :key="index">
             <v-card>
               <v-card-title>CreatedBy: {{item.creator}}</v-card-title>
              <v-card-text>IssuedTo:    {{item.issuedTo}}</v-card-text>
               <v-card-text>Description:{{item.Description}}</v-card-text>
                <v-card-text>Info:      {{item.TicketInfo}}</v-card-text>
            </v-card>
    </div>
   </v-row>
    <!-- Right upon clicking the button the submit function is called, and all the instructions are executed in this function -->
  
</div>
</template>
<script>
import axios from "axios";
export default {
    data(){
        return{
        //Creating variables that will store the data in the text fields
        creator:null,
        issuedTo:null,
        Description: null,
        TicketInfo: null,
        //we are getting the object and pushing it into the ticket array
        ticketArray:[],
        //This enables the dialog to close after you 
        dialog:false
        }
    },
    methods: {
    //When the submit function is called the data fields in it are pushed into the ticket array
        submit(){
    //A local variable has been declared and contains data for the object
        let objectData={
         creator:this.creator,
         issuedTo:this.issuedTo,
         Description:this.Description,
         ticketInfo:this.ticketInfo,
         

         TicketInfo:this.TicketInfo
        }
         //We are going to use the array to push the object data, we are basically pushing data into the array
        this.ticketArray.push(objectData);
        //Send ticket to server or database
        axios.post("http://localhost:3004/tickets",objectData).then(res=>{
          console.log("Your ticket has been successfully posted",objectData);
        })
   
    //After we push data onto the array we want all the fields for the object to remain null
   this.creator=null,
   this.issuedTo=null,
    this.Description=null,
    this.TicketInfo=null,

    this.dialog=false
        },
        closeDialog(){
        this.name=null,
        this.Description=null,
        this.TicketInfo=null,

        this.dialog=false
        }
    }
    }

</script>
<style scoped>
#cards {
  padding-top: 1rem;
}
</style>