<template>
    <div class="card mb-4 p-3">
        <div id="chart">
            <apexchart type="pie" :options="chartOptions" :series="series"></apexchart>
        </div>
        <br>
        <A_TextComponent :second_title="second_title" />
        <hr>
        <A_TextComponent :content="content" />
    </div>
</template>
  
<script>
    import VueApexCharts from "vue3-apexcharts"
    import A_TextComponent from "@/components/atoms/A_TextComponent.vue"
    
    export default {
        components: {
            apexchart: VueApexCharts,
            A_TextComponent
        },
        props: {
            series: {
                type: Array,
                required: true
            },
            labels: {
                type: Array,
                required: true
            },
            second_title: {
                type: String,
                default: ""
            },
            content: {
                type: String,
                default: ""
            }
        },
        computed: {
            chartOptions() {
                return {
                    chart: {
                        width: 380,
                        type: "pie"
                    },
                    labels: this.labels,
                    legend: {
                        position: "bottom"
                    },
                    responsive: [
                        {
                            breakpoint: 480,
                            options: {
                                chart: {
                                    width: 200
                                },
                            }
                        }
                    ]
                }
            }
        }
    }
</script>
  
<style scoped>
    #chart {
        max-width: 100%;
        margin: auto;
    }
</style>
  