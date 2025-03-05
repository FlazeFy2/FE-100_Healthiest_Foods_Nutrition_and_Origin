<script setup>
  import A_TextComponent from "@/components/atoms/A_TextComponent.vue"
  import M_DescriptiveStatistic from "@/components/molecules/M_DescriptiveStatistic.vue"
  import O_TableComponent from "@/components/organisms/O_TableComponent.vue"
  import { readBody, readHeader } from "@/utils/data_prepare";
  import { onMounted, ref } from "vue";
  import ShowTreeMap from "@/components/usecases/ShowTreeMap.vue"
  import ShowPieChart from "@/components/usecases/ShowPieChart.vue"
  import ShowColumnChart from "./usecases/ShowColumnChart.vue";

  const header_dataset = ref([])
  const body_dataset = ref([])

  onMounted(async () => {
    const filePath = "/src/assets/Top 100 Healthiest Food in the World.csv" 
    try {
      const data_header = await readHeader(filePath)
      const data_body = await readBody(filePath)

      // Data Prepare
      const data_header_clean = data_header.filter(dt => dt !== "Unnamed: 0")
      header_dataset.value = data_header_clean.map(header => ({
        label: header,
        field: header,
        sortable: true
      }))      
      const data_body_clean = data_body.map(row => {
        return Object.fromEntries(
            Object.entries(row).filter(([key]) => data_header_clean.includes(key))
        )
      })
      body_dataset.value = data_body_clean
    } catch (error) {
      console.error("Failed to load CSV:", error)
    }
  })
</script>

<template>
  <div class="greetings">
    <A_TextComponent title="100 Healthiest Foods Nutrition and Origin" />
    <div class="row">
      <div class="col-lg-6 col-md-6 col-sm-12 col-12">
        <A_TextComponent second_title="About" />
        <A_TextComponent content="This dataset compiles information on 100 of the world's healthiest foods, providing a detailed nutritional breakdown and historical context for each item. It aims to be a valuable resource for nutritionists, data scientists, and health enthusiasts interested in exploring the relationships between various foods, their nutritional content, and their cultural significance."/>
        <A_TextComponent content="Each entry includes the food's name, key nutritional highlight, serving size, place of origin, and detailed nutritional information per 100g serving. The nutritional data covers essential metrics such as calories, protein content, fiber content, vitamin C levels, and an antioxidant score. This comprehensive approach allows for in-depth analysis and comparison of different foods across various health parameters."/>
      </div>
      <div class="col-lg-6 col-md-6 col-sm-12 col-12">
        <A_TextComponent second_title="Source" />
        <a href="https://www.kaggle.com/datasets/prajwaldongre/top-100-healthiest-food-in-the-world" target="_blank" rel="noopener">Kaggle</a>
        <a href="https://github.com/FlazeFy2/DS-100_Healthiest_Foods_Nutrition_and_Origin" target="_blank" rel="noopener">Jupiter Notebook</a>
      </div>
    </div>
    
    <hr>
    <div class="d-flex justify-content-start mt-3">
      <button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="#collapseOne" aria-expanded="true" aria-controls="collapseOne">Dataset</button>
      <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#collapseTwo" aria-expanded="false" aria-controls="collapseTwo">Descriptive Statistic</button>
      <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#collapseThree" aria-expanded="false" aria-controls="collapseThree">Tree Map</button>
      <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#collapseFour" aria-expanded="false" aria-controls="collapseFour">Pie Chart</button>
      <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#collapseFive" aria-expanded="false" aria-controls="collapseFive">Column Chart</button>
    </div>

    <div class="accordion" id="accordionExample">
      <div class="accordion-item">
        <div id="collapseOne" class="accordion-collapse collapse show" data-bs-parent="#accordionExample">
          <A_TextComponent second_title="Dataset" />
          <O_TableComponent :header="header_dataset" :body="body_dataset"/>
        </div>
      </div>

      <div class="accordion-item">
        <div id="collapseTwo" class="accordion-collapse collapse" data-bs-parent="#accordionExample">
          <A_TextComponent second_title="Descriptive Statistic" />
          <div class="row">
            <div class="col-lg-4 col-md-6 col-sm-12 col-12 mx-auto">
              <M_DescriptiveStatistic target_col="Calories"/>
            </div>
            <div class="col-lg-4 col-md-6 col-sm-12 col-12 mx-auto">
              <M_DescriptiveStatistic target_col="Protein (g)"/>
            </div>
            <div class="col-lg-4 col-md-6 col-sm-12 col-12 mx-auto">
              <M_DescriptiveStatistic target_col="Fiber (g)"/>
            </div>
            <div class="col-lg-4 col-md-6 col-sm-12 col-12 mx-auto">
              <M_DescriptiveStatistic target_col="Vitamin C (mg)"/>
            </div>
            <div class="col-lg-4 col-md-6 col-sm-12 col-12 mx-auto">
              <M_DescriptiveStatistic target_col="Antioxidant Score"/>
            </div>
          </div>
        </div>
      </div>

      <div class="accordion-item">
        <div id="collapseThree" class="accordion-collapse collapse" data-bs-parent="#accordionExample">
          <A_TextComponent second_title="Tree Map" />
          <ShowTreeMap/>
        </div>
      </div>

      <div class="accordion-item">
        <div id="collapseFour" class="accordion-collapse collapse" data-bs-parent="#accordionExample">
          <A_TextComponent second_title="Pie Chart" />
          <ShowPieChart/>
        </div>
      </div>

      <div class="accordion-item">
        <div id="collapseFive" class="accordion-collapse collapse" data-bs-parent="#accordionExample">
          <A_TextComponent second_title="Column Chart" />
          <ShowColumnChart/>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
  a {
    color: #42b883;
    font-weight: 500;
    font-size: 14px;
    background-color:rgba(66, 184, 131, 0.25);
    border-radius: 20px;
    padding: 7px 12px;
    margin-right: 6px;
  }
</style>
