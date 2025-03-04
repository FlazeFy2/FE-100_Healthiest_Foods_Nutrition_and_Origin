<script setup>
    import { ref, onMounted } from "vue"
    import { readCsv } from "@/utils/data_prepare"
    import O_PieChartComponent from "@/components/organisms/O_PieChartComponent.vue"
    import { countWordFrequencies } from "@/utils/analyze";

    const labels_calorie_comparison = ref([])
    const series_calorie_comparison = ref([])
    const labels_protein_comparison = ref([])
    const series_protein_comparison = ref([])
    const labels_fiber_comparison = ref([])
    const series_fiber_comparison = ref([])
    const labels_vitc_comparison = ref([])
    const series_vitc_comparison = ref([])

    onMounted(async () => {
        const filePath = "/src/assets/Top 100 Healthiest Food in the World.csv" 
        try {
            const data_raw = await readCsv(filePath,['Calories','Protein (g)','Fiber (g)','Vitamin C (mg)'])
            
            // Exploratory Data Analysis (EDA) - Pie Chart Share of Calorie Level for Healthiest Food
            data_raw['Calories Level'] = data_raw['Calories'].map(dt => {
                if(dt <= 200){
                    return "Low"
                } else if(dt > 200 && dt <= 400){
                    return "Medium"
                } else {
                    return "High"
                }
            })
            const calorie_comparison = countWordFrequencies(data_raw['Calories Level'])
            labels_calorie_comparison.value = Object.keys(calorie_comparison)
            series_calorie_comparison.value = Object.values(calorie_comparison)

            // Exploratory Data Analysis (EDA) - Pie Chart Share of Protein for Healthiest Food
            data_raw['Protein Level'] = data_raw['Protein (g)'].map(dt => {
                if(dt < 10){
                    return "Low"
                } else if(dt < 20){
                    return "Medium"
                } else {
                    return "High"
                }
            })
            const protein_comparison = countWordFrequencies(data_raw['Protein Level'])
            labels_protein_comparison.value = Object.keys(protein_comparison)
            series_protein_comparison.value = Object.values(protein_comparison)

            // Exploratory Data Analysis (EDA) - Pie Chart Share of Fiber for Healthiest Food
            data_raw['Fiber Level'] = data_raw['Fiber (g)'].map(dt => {
                if(dt < 2.5){
                    return "Low"
                } else if(dt <= 5){
                    return "Medium"
                } else {
                    return "High"
                }
            })
            const fiber_comparison = countWordFrequencies(data_raw['Fiber Level'])
            labels_fiber_comparison.value = Object.keys(fiber_comparison)
            series_fiber_comparison.value = Object.values(fiber_comparison)
            
            // Exploratory Data Analysis (EDA) - Pie Chart Share of Vitamin C for Healthiest Food
            data_raw['Vitamin C Level'] = data_raw['Vitamin C (mg)'].map(dt => {
                if(dt < 30){
                    return "Low"
                } else if(dt <= 70){
                    return "Medium"
                } else {
                    return "High"
                }
            })
            const vitc_comparison = countWordFrequencies(data_raw['Vitamin C Level'])
            labels_vitc_comparison.value = Object.keys(vitc_comparison)
            series_vitc_comparison.value = Object.values(vitc_comparison)
        } catch (error) {
            console.error("Failed to load CSV:", error)
        }
    })
</script>

<template>
    <div class="row">
        <div class="col-lg-4 col-md-6 col-sm-12 col-12 mx-auto">
            <!-- Exploratory Data Analysis (EDA) - Pie Chart Calories Comparison -->
            <O_PieChartComponent 
                :series="series_calorie_comparison" 
                :labels="labels_calorie_comparison" 
                second_title="Calorie Comparison" 
                content="This compare total food by its calorie level"
            />
        </div>
        <div class="col-lg-4 col-md-6 col-sm-12 col-12 mx-auto">
            <!-- Exploratory Data Analysis (EDA) - Pie Chart Protein Comparison -->
            <O_PieChartComponent 
                :series="series_protein_comparison" 
                :labels="labels_protein_comparison" 
                second_title="Protein Comparison" 
                content="This compare total food by its protein level"
            />
        </div>
        <div class="col-lg-4 col-md-6 col-sm-12 col-12 mx-auto">
            <!-- Exploratory Data Analysis (EDA) - Pie Chart Fiber Comparison -->
            <O_PieChartComponent 
                :series="series_fiber_comparison" 
                :labels="labels_fiber_comparison" 
                second_title="Fiber Comparison" 
                content="This compare total food by its fiber level"
            />
        </div>
        <div class="col-lg-4 col-md-6 col-sm-12 col-12 mx-auto">
            <!-- Exploratory Data Analysis (EDA) - Pie Chart Vitamin C Comparison -->
            <O_PieChartComponent 
                :series="series_vitc_comparison" 
                :labels="labels_vitc_comparison" 
                second_title="Vitamin C Comparison" 
                content="This compare total food by its vitamin c level"
            />
        </div>
    </div>
</template>


