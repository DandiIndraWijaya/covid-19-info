<template>
    <div class="listCountries">
        <center><h4>List Countries</h4></center>
        <ul>
            <li v-for="(row, index) in countries" :key="index">
                <center>
                    <button class="btn-country">
                        <font>{{row}}</font>
                    </button>
                </center>
            </li>
        </ul>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'ListCountries',
    data: function(){
        return{
            countries: []
        }
    },
    methods: {
        getCountries(){
            axios({
                    "method":"GET",
                    "url":"https://covid-193.p.rapidapi.com/countries",
                    "headers":{
                    "content-type":"application/octet-stream",
                    "x-rapidapi-host":"covid-193.p.rapidapi.com",
                    "x-rapidapi-key":"5613c62dbbmsha8b136aae9e5a3dp16431ejsn867af4e887d6",
                    "useQueryString":true}
                }).then(response => this.countries = response.data.response );
        }
    },
    mounted() {
        this.getCountries()
    }
}
</script>

<style>
ul{
    list-style-type: none;
    padding: 0;
    margin: 0;
}

.btn-country{
    width: 90%;
    text-align: center;
    color: white;
    height: 28px;
    border: none;
    outline: none;
    margin-bottom: 5px;
    cursor: pointer;
    background-color: skyblue;
    font-size: 14px;
    transition: width 0.5s, height 0.5s;
}

.btn-country:hover{
    width: 100%;
    height: 46px;
    font-size: 20px;
}

.btn-country font{
    
}
</style>