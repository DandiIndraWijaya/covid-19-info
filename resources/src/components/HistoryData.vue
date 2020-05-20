
<script>
import { Line } from 'vue-chartjs'

export default {
    extends: Line,
    name: 'History',
    data: function(){
        return {
            chartdata: {
            labels: ['January', 'February'],
            datasets: [
                {
                label: 'Data One',
                backgroundColor: '#f87979',
                data: [40, 80]
                }
            ]
            },
            options: {
            responsive: true,
            maintainAspectRatio: false
            }
        }
    },
    methods: {
        
            
       
    },
    mounted(){
        this.$root.$on('emitCountry', country => {
            console.log(country);
            this.renderChart(this.chartdata, this.options);
        });
    }
}
</script>

<style>

</style>