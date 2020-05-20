<template>
    <div id="statistics">
        <div class="loading">
            <center>
                <h1>Fetching Data...</h1>
            </center>
        </div>

        <div class="data">
            <div class="card time">
                <table>
                    <tr>
                        <td>Day </td>
                        <td>:</td>
                        <td>{{ day }}</td>
                    </tr>
                    <tr>
                        <td>time </td>
                        <td>:</td>
                        <td>{{ time }}</td>
                    </tr>
                </table>
            </div>
            <div class="card case">
                <center>
                    <font class="title">Cases</font>
                </center>
                <hr>
                <table>
                    <tr>
                        <td class="active-case">New </td>
                        <td>:</td>
                        <td>{{ newCases }}</td>
                    </tr>
                    <tr>
                        <td class="active-case">Active </td>
                        <td>:</td>
                        <td>{{ activeCases }}</td>
                    </tr>
                    <tr>
                        <td class="critical-case">Critical </td>
                        <td>:</td>
                        <td>{{ criticalCases }}</td>
                    </tr>
                    <tr>
                        <td class="recovered-case">Recovered </td>
                        <td>:</td>
                        <td>{{ recoveredCases }}</td>
                    </tr>
                    <tr>
                        <td class="total-case">Total </td>
                        <td>:</td>
                        <td>{{ totalCases }}</td>
                    </tr>
                </table>
            </div>

            <div class="card death">
                <center>
                    <font class="title">Deaths</font>
                </center>
                <hr>
               <table>
                   <tr>
                       <td>New</td>
                       <td>:</td>
                       <td>{{ newDeaths }}</td>
                   </tr>
                   <tr>
                       <td>Total</td>
                       <td>:</td>
                       <td>{{ totalDeaths }}</td>
                   </tr>
               </table>
            </div>

            <div class="card test">
                <center>
                    <font class="title">Tests</font>
                </center>
                <hr>
                <center>{{ tests }}</center>
            </div>
        </div>       
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Statistics',
    data: function(){
        return{
            newCases: '',
            activeCases: '',
            criticalCases: '',
            recoveredCases: '',
            totalCases: '',
            newDeaths: '',
            totalDeaths: '',
            tests: '',
            day: '',
            time: ''
        }
    },
    methods: {
        showStatistics(country){
            document.querySelector('.data').style.display = "none";
            document.querySelector('.loading').style.display = "block";
            
            axios({
                    "method":"GET",
                    "url":"https://covid-193.p.rapidapi.com/statistics",
                    "headers":{
                    "content-type":"application/octet-stream",
                    "x-rapidapi-host":"covid-193.p.rapidapi.com",
                    "x-rapidapi-key":"5613c62dbbmsha8b136aae9e5a3dp16431ejsn867af4e887d6",
                    "useQueryString":true
                    },
                    "params":{
                        "country":country
                    }
                })
                .then(response => {
                    document.querySelector('.loading').style.display = "none";

                    this.newCases = response.data.response[0].cases.new;
                    this.activeCases = response.data.response[0].cases.active;
                    this.criticalCases = response.data.response[0].cases.critical;
                    this.recoveredCases = response.data.response[0].cases.recovered;
                    this.totalCases = response.data.response[0].cases.total;

                    this.newDeaths = response.data.response[0].deaths.new;
                    this.totalDeaths = response.data.response[0].deaths.total;

                    this.tests = response.data.response[0].tests.total;

                    this.day = response.data.response[0].day;
                    this.time = response.data.response[0].time;

                    document.querySelector('.data').style.display = "block";
                    console.log(response);
                })
        }
    },
    mounted(){
        this.$root.$on('emitCountry', country => {this.showStatistics(country)});
    }
}
</script>

<style>

#statistics{
    background-color: gainsboro;
}

.data{
    display: none;
}

.loading{
    margin-top: 20%;
    display: none;
}

.title{
    font-weight: bold;
}
.card{
    background-color: white;
    margin: 20px;
    width: max-content;
    padding: 10px;
}

.time{
    font-size: 10px;
}

.active-case{

}

.recovered-case{

}

.critical-case{

}

.death{
    
}
</style>