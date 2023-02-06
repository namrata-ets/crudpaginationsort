<template>
  <v-container>
        <h1 class="display-2 font-weight-bold mb-3 text-center my-5">
          Airline Reservation System
        </h1>   
        
  <div>
    <v-data-table
      :headers="headers"
      :options.sync="options"
      :loading="loading"
      class="elevation-1"
    ></v-data-table>
  </div>

  </v-container>
</template>
<script>

import axios from 'axios';
  export default {
    name: 'HelloWorld',
    data () {
      return {
         totalPassengers: 0,
        passengers: [],
        loading: true,
        options: {},
        headers: [
          {
            text: 'Airline Name',
            align: 'start',
            sortable: false,
            value: 'name',
          },
          { text: 'Passenger Name', value: 'calories' },
          { text: 'Number of Trips', value: 'fat' },
        ],
        airlineData: [],
        reqObj: {
          name: "John Doe",
          trips: 250,
          airline: 5,
          airlineName: "",
        },
      }
    },
    watch: {
      options: {
        handler () {
          this.getDataFromApi()
        },
        deep: true,
      },
    },
    methods:{

      async getDataFromApi() {

        this.loading = true

        await axios
        .get(`https://api.instantwebtools.net/v1/passenger?page=3889&size=10`)
        .then((response) => (this.airlineData = response.data))
        .catch((error) => console.log(error));
        console.log(this.airlineData);
       
        this.totalPassengers = this.airlineData.totalPassengers;
        console.log("The total number of passengers till date is: "+this.totalPassengers);
        this.loading = false;
        this.getPassengersData();
      },

async getPassengersData(){
    await axios
        .get(`https://api.instantwebtools.net/v1/passenger?page=3889&size=10`)
        .then((response) => (this.passengers = response.data.data))
        .catch((error) => console.log(error));
        console.log("Passenger data fetched from API is: "+this.passengers);
  },
}
}
</script>
