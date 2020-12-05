<template>
    <div>
        <div class="dropdown">
            <b-dropdown id="dropdown-1" text="Dropdown Button" class="m-md-2">
                <b-dropdown-item v-for="country in countries" :key="country.country">
                    {{country.country}}
                </b-dropdown-item>
            </b-dropdown>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    data(){
        return{
            countries: []
        }
    },
    created() {
        this.loadAllCountries();
    },

    methods: {
        loadAllCountries() {
            axios({
                method: 'GET',
                url: 'https://covid-193.p.rapidapi.com/statistics',
                headers: {
                    'x-rapidapi-key': '668a33eddbmshfe3f9fcc783a777p156da6jsn80afade4d5b1',
                    'x-rapidapi-host': 'covid-193.p.rapidapi.com'
                }
            })
            .then(response => {
                this.countries = response.data.response
                console.log(response.data)
            })
            .catch(error => {
                console.log(error)
            })
        }
    }
    
}
</script>