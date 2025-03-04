<script setup>
  import A_TextComponent from "@/components/atoms/A_TextComponent.vue"
  import M_DescriptiveStatistic from "@/components/molecules/M_DescriptiveStatistic.vue"
</script>

<template>
  <div class="greetings">
    <A_TextComponent title="100 Healthiest Foods Nutrition and Origin" />
    <A_TextComponent second_title="About" />
    <A_TextComponent content="The dataset offers a comprehensive view of consumer shopping trends, aiming to uncover patterns and behaviors in retail purchasing. It contains detailed transactional data across various product categories, customer demographics, and purchase channels"/>
    <A_TextComponent second_title="Source" />
    <a href="https://www.kaggle.com/datasets/prajwaldongre/top-100-healthiest-food-in-the-world" target="_blank" rel="noopener">Kaggle</a>
    <a href="https://github.com/FlazeFy2/DS-100_Healthiest_Foods_Nutrition_and_Origin" target="_blank" rel="noopener">Jupiter Notebook</a>
    
    <hr>
    <div class="d-flex justify-content-between">
      <A_TextComponent second_title="Descriptive Statistic" />
      <button class="btn btn-link rounded-pill" type="button" data-bs-toggle="collapse" data-bs-target="#collapseDescriptiveStats" aria-expanded="false" aria-controls="collapseExample">Show Content</button>
    </div>
    <div class="collapse" id="collapseDescriptiveStats">
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
