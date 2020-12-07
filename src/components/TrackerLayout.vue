<template>
    <div class="container">
        <div class="my-2 push-right">
            <input class="mx-1 p-2 rounded-lg" placeholder="Search by country" v-model="country">
            <b-button size="md" variant="success" class="my-2 my-sm-0" type="submit" @click="onClickSearch">Search</b-button>
            <b-button size="md" variant="info" class="my-2 my-sm-0 mx-1" type="submit" @click="getStatistics">Worldwide</b-button>
        </div>
            
        <div class="jumbotron jumbotron-fluid bg-dark shadow rounded">
            <div class="container">
                <h3 class="display-4 ">{{ h3 }}</h3>
                <h2 class="lead text-warning">Covid-19 Statistics</h2>
            </div>

            <div class="" v-for="statistics in formatStatistic" :key="statistics.country">
                <h1 class="text-warning">{{ statistics.country }}</h1>
            </div>

            <div class="container-fluid">
                <div class="row">
                    <div class="col-sm-6 mt-1">
                        <Card v-for="statistics in formatStatistic"
                            :key="statistics.time" 
                            title="Cases" 
                            :value1="statistics.cases.new" 
                            :value2="statistics.cases.total" 
                        />
                    </div>

                    <div class="col-sm-6 mt-1">
                        <Card v-for="statistics in formatStatistic" 
                            :key="statistics.time" 
                            title="Deaths"
                            :value1="statistics.deaths.new" 
                            :value2="statistics.deaths.total" 
                        />
                    </div>
                </div>

                <div class="row">
                    <div class="col-sm-6 offset-sm-3 mt-1 mt-lg-4">
                        <Card v-for="statistics in formatStatistic" 
                            :key="statistics.time" 
                            title="Recovered"
                            :value2="statistics.cases.recovered"  
                        />
                    </div>
                </div>
            </div>

            <div class="row mt-5">
                <div class="col-sm-4 offset-md-4 text-center">
                    <span class="text-warning">Date: {{ timestamp }}</span>
                </div>
            </div>
                
        </div>
    </div>
</template>

<script>
import axios from "axios";

import Card from './Card.vue';


export default {
    components: {
        Card,
    },
    props: {
        h3: String,
        p: String
    },
    data: () => ({
       statistics: {},
       timestamp: '',
       country: ''
    }),
    created() {
        this.getStatistics()
        setInterval(this.getNow, 1000);
    },
    computed: {
        formatStatistic() {
            return Object.values(this.statistics)
        },

    },
    methods: {
        getStatistics() {
            //get all countries covid statistics
            const statistics = localStorage.getItem("statistics")

            if(statistics) {
                this.statistics = JSON.parse(statistics)
                return
            }
            axios({
                method: 'GET',
                url: process.env.VUE_APP_API_URL,
                params: {country: 'All'},
                headers: {
                    'x-rapidapi-key': process.env.VUE_APP_API_KEY,
                    'x-rapidapi-host': process.env.VUE_APP_API_HOST
                }

            })
                .then(response => {
                    this.statistics = response.data.response
                    // console.log(response.data.response)
                })
                .catch(error => {
                    console.log(error)
                })
        },
        onClickSearch() {
            //Search by country name
            if(!this.country) return
            axios({
                method: 'GET',
                url: process.env.VUE_APP_API_URL,
                params: {country: this.country},
                headers: {
                    'x-rapidapi-key': process.env.VUE_APP_API_KEY,
                    'x-rapidapi-host': process.env.VUE_APP_API_HOST
                }
            })
                .then(response => {
                    this.statistics = response.data.response
                    this.country = ''
                    // console.log(response.data.response)
                })
                .catch(error => {
                    console.log(error)
                })
        },
        getNow() {
            //get local time and date
            const today = new Date();
            const date = today.getDate() + '/' + (today.getMonth() + 1) + '/' + today.getFullYear();
            const time = today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
            const dateTime = date + ' ' + time;
            this.timestamp = dateTime;
        }
    },
    
    
};
</script>