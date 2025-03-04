<script setup>
  import { ref, onMounted } from "vue"
  import { readCsv } from "@/utils/data_prepare"
  import { countWordFrequencies } from "@/utils/analyze"
  import O_TreeMapComponent from "@/components/organisms/O_TreeMapComponent.vue"
  import A_TextComponent from "@/components/atoms/A_TextComponent.vue"
  
  const series_qty_tree = ref([])
  const series_originated_from_tree = ref([])

  onMounted(async () => {
    const filePath = "/src/assets/Top 100 Healthiest Food in the World.csv" 
    try {
      const data_qty_raw = await readCsv(filePath,['Quantity'])
      const data_originated_from_raw = await readCsv(filePath,['Originated From'])

      // Exploratory Data Analysis (EDA) - Tree Map Top 20 Quantity Comparison
      const most_raw_tree = countWordFrequencies(data_qty_raw['Quantity'], 20)
      series_qty_tree.value = [
        {
          data: Object.entries(most_raw_tree).map(([key, value]) => ({
            x: key,
            y: value
          }))
        }
      ]

      // Exploratory Data Analysis (EDA) - Tree Map Top 20 Originated From Comparison
      const most_originated_from_tree = countWordFrequencies(data_originated_from_raw['Originated From'], 20)
      series_originated_from_tree.value = [
        {
          data: Object.entries(most_originated_from_tree).map(([key, value]) => ({
            x: key,
            y: value
          }))
        }
      ]
    } catch (error) {
      console.error("Failed to load CSV:", error)
    }
  })
</script>

<template>
  <div class="d-flex justify-content-between">
    <A_TextComponent second_title="Tree Map" />
    <button class="btn btn-link rounded-pill" type="button" data-bs-toggle="collapse" data-bs-target="#collapseTreeStats" aria-expanded="false" aria-controls="collapseExample">Show Content</button>
  </div>
  <div class="collapse ps-3" id="collapseTreeStats">
    <div class="row">
      <div class="col-lg-6 col-md-6 col-sm-12 col-12 mx-auto">
        <!-- Exploratory Data Analysis (EDA) - Tree Map Top 20 Quantity Comparison -->
        <O_TreeMapComponent 
          :series="series_qty_tree" 
          second_title="Top 20 Quantity Comparison" 
          content="This show food comparison by its quantity"
        />
      </div>
      <div class="col-lg-6 col-md-6 col-sm-12 col-12 mx-auto">
        <!-- Exploratory Data Analysis (EDA) - Tree Map Top 20 Originated From Comparison -->
        <O_TreeMapComponent 
          :series="series_originated_from_tree" 
          second_title="Top 20 Originated From Comparison" 
          content="This show food comparison by its originated from"
        />
      </div>
    </div>
  </div>
</template>


