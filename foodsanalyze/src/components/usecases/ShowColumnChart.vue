<script setup>
  import { ref, onMounted } from "vue"
  import { readCsv } from "@/utils/data_prepare"
  import O_ColumnChartComponent from "../organisms/O_ColumnChartComponent.vue"

  const labels_calorie_top = ref([])
  const series_calorie_top = ref([])
  const labels_protein_top = ref([])
  const series_protein_top = ref([])
  const labels_fiber_top = ref([])
  const series_fiber_top = ref([])
  const labels_vitaminC_top = ref([])
  const series_vitaminC_top = ref([])
  const labels_antioxidant_top = ref([])
  const series_antioxidant_top = ref([])

  onMounted(async () => {
    const filePath = "/src/assets/Top 100 Healthiest Food in the World.csv" 
    try {
      const data_raw = await readCsv(filePath,['Food','Calories','Protein (g)','Fiber (g)','Vitamin C (mg)','Antioxidant Score'])

      // Convert to array of objects
      const dataArray = data_raw['Food'].map((food, index) => ({
        food,
        calories: Number(data_raw['Calories'][index]),
        protein: Number(data_raw['Protein (g)'][index]),
        fiber: Number(data_raw['Fiber (g)'][index]),
        vitaminC: Number(data_raw['Vitamin C (mg)'][index]),
        antioxidant: Number(data_raw['Antioxidant Score'][index])
      }))

      // Function to get top 7 based on a key
      const getTop = (key) => [...dataArray].sort((a, b) => b[key] - a[key]).slice(0, 7)

      // Exploratory Data Analysis (EDA) - Column Chart 7 Top Food By Its Calorie
      const topCalories = getTop("calories")
      labels_calorie_top.value = topCalories.map(item => item.food)
      series_calorie_top.value = [{ name: "Calories", data: topCalories.map(item => item.calories) }]

      // Exploratory Data Analysis (EDA) - Column Chart 7 Top Food By Its Protein
      const topProtein = getTop("protein")
      labels_protein_top.value = topProtein.map(item => item.food)
      series_protein_top.value = [{ name: "Protein (g)", data: topProtein.map(item => item.protein) }]

      // Exploratory Data Analysis (EDA) - Column Chart 7 Top Food By Its Fiber
      const topFiber = getTop("fiber")
      labels_fiber_top.value = topFiber.map(item => item.food)
      series_fiber_top.value = [{ name: "Fiber (g)", data: topFiber.map(item => item.fiber) }]

      // Exploratory Data Analysis (EDA) - Column Chart 7 Top Food By Its Vitamin C
      const topVitaminC = getTop("vitaminC")
      labels_vitaminC_top.value = topVitaminC.map(item => item.food)
      series_vitaminC_top.value = [{ name: "Vitamin C (mg)", data: topVitaminC.map(item => item.vitaminC) }]

      // Exploratory Data Analysis (EDA) - Column Chart 7 Top Food By Its Antioxidant
      const topAntioxidant = getTop("antioxidant")
      labels_antioxidant_top.value = topAntioxidant.map(item => item.food)
      series_antioxidant_top.value = [{ name: "Antioxidant Score", data: topAntioxidant.map(item => item.antioxidant) }]
    } catch (error) {
      console.error("Failed to load CSV:", error)
    }
  })
</script>

<template>
  <div class="row">
    <div class="col-lg-6 col-md-6 col-sm-12 col-12 mx-auto">
      <!-- Exploratory Data Analysis (EDA) - Column Chart Top 7 Food By Its Calorie -->
      <O_ColumnChartComponent 
        :series="series_calorie_top" 
        :labels="labels_calorie_top" 
        second_title="Top 7 Food By Its Calorie" 
        content="This chart shows the top 7 food by its calorie"
      />
    </div>
    <div class="col-lg-6 col-md-6 col-sm-12 col-12 mx-auto">
      <!-- Exploratory Data Analysis (EDA) - Column Chart Top 7 Food By Its Protein -->
      <O_ColumnChartComponent 
        :series="series_protein_top" 
        :labels="labels_protein_top" 
        second_title="Top 7 Foods by Protein" 
        content="This chart shows the top 7 foods by protein"
      />
    </div>
    <div class="col-lg-6 col-md-6 col-sm-12 col-12 mx-auto">
      <!-- Exploratory Data Analysis (EDA) - Column Chart Top 7 Food By Its Fiber -->
      <O_ColumnChartComponent 
        :series="series_fiber_top" 
        :labels="labels_fiber_top" 
        second_title="Top 7 Foods by Fiber" 
        content="This chart shows the top 7 foods by fiber."
      />
    </div>
    <div class="col-lg-6 col-md-6 col-sm-12 col-12 mx-auto">
      <!-- Exploratory Data Analysis (EDA) - Column Chart Top 7 Food By Its Vitamin C -->
      <O_ColumnChartComponent 
        :series="series_vitaminC_top" 
        :labels="labels_vitaminC_top" 
        second_title="Top 7 Foods by Vitamin C" 
        content="This chart shows the top 7 foods by Vitamin C."
      />
    </div>
    <div class="col-lg-6 col-md-6 col-sm-12 col-12 mx-auto">
      <!-- Exploratory Data Analysis (EDA) - Column Chart Top 7 Food By Its Antioxidant Score -->
      <O_ColumnChartComponent 
        :series="series_antioxidant_top" 
        :labels="labels_antioxidant_top" 
        second_title="Top 7 Foods by Antioxidant Score" 
        content="This chart shows the top 7 foods by Antioxidant Score."
      />
    </div>
  </div>
</template>


