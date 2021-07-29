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
    <br/>
    <h2 class="display-2 display-2 font-weight-thin mb-4">Pending tickets</h2>
        
<!-- v-for is like a for loop it loops through an array it enables us to display things according to the number of elements we have in the array  -->
   
  
 <!-- class pl can move the proximity to the margins -->
     <v-row>
    <div id="cards" class="pl-4" v-for="(item,index) in  pendingTickets" :key="index">
             <v-card>
               <v-card-title>CreatedBy: {{item.creator}}</v-card-title>
              <v-card-text>IssuedTo:    {{item.issuedTo}}</v-card-text>
               <v-card-text>Description:{{item.Description}}</v-card-text>
                <v-card-text>Info:      {{item.TicketInfo}}</v-card-text>
            </v-card>
    </div>
   </v-row>  
   <br/>
       <h2 class="display-2 font-weight-thin mb-4">Created Tickets</h2>
               <v-col cold="12" md="12">
    <v-card>
    <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">
            Created By:
          </th>
          <th class="text-left">
            Issued To:
          </th>
           <th class="text-left">
            Description:
          </th>
           <th class="text-left">
            TicketInfo:
          </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="item in ticketArray"
          :key="item.creator"
        >
          <td>{{ item.creator }}</td>
          <td>{{ item.issuedTo }}</td>
          <td>{{ item.Description }}</td>
          <td>{{ item.TicketInfo }}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
   </v-card>
   </v-col>
 
   <br/>
 
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
        pendingTickets:null,
        //This enables the dialog to close after you 
        dialog:false
        }
    },
    mounted(){
     this.getPendingTickets();
    },
    computed:{
      trackCreatedTickets(){
       return this.ticketArray;
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
        },
        getPendingTickets(){
          axios.get("http://localhost:3004/tickets").then(res=>{
            this.pendingTickets = res.data;
            console.log("Pending tickets received");
          })
        }
    }
    }

</script>
<style scoped>
#cards {
  padding-top: 1rem;
}
</style>