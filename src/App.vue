<template>
  <!-- 下拉菜单 -->
  <div class="dropdown-container" @click="toggleDropdown">
  <div class="dropdown-trigger">
    More Research
    <span><img src="/arrow.png" alt="arrow" class="dropdown-arrow" /></span>
  </div>

  <div v-if="showDropdown" class="dropdown-menu">
    <a
      v-for="item in menuItems"
      :key="item.name"
      :href="item.link"
      target="_blank"
      class="dropdown-item"
    >
      {{ item.name }}<span v-if="item.hot" class="hot-icon">🔥</span>
    </a>
  </div>
</div>

  <div class="container">
    <main>
      <h1>Where am I?</h1>
      <h2>Cross-View Geo-localization<br/>with Natural Language Descriptions</h2>
      <p class="authors">
        <a href="https://openreview.net/profile?id=~Junyan_Ye1" target="_blank">Junye Yan<sup>1,2</sup></a>,
        <a href="https://openreview.net/profile?id=~Honglin_Lin2" target="_blank">Honglin Lin<sup>2,3</sup></a>,
        <a href="https://openreview.net/profile?id=~Leyan_Ou1" target="_blank">Leyan Ou<sup>1</sup></a>,<br/>
        <a href="https://openreview.net/profile?id=~Dairong_Chen1" target="_blank">Dairong Chen<sup>4</sup></a>,
        <a href="https://openreview.net/profile?id=~Zihao_Wang37" target="_blank">Zihao Wang<sup>1</sup></a>,
        <a href="https://openreview.net/profile?id=~Qi_Zhu19" target="_blank">Qi Zhu<sup>1</sup></a>,
        <a href="https://openreview.net/profile?id=~Conghui_He2" target="_blank">Conghui He<sup>2</sup></a>,
        <a href="https://openreview.net/profile?id=~Weijia_Li2" target="_blank">Weijia Li<sup>1,2</sup></a>
      </p>

      <p class="authors"><sup>1</sup>Sun Yat-sen University, <sup>2</sup>Shanghai AI Lab,<br/><sup>3</sup>Beijing University of Posts and Telecommunications, <sup>4</sup>Wuhan University</p>

      <p class="venue">International Conference on Computer Vision (ICCV), 2025</p>

      <div class="link-buttons">
      <a href="https://openreview.net/forum?id=wciU4BEuzw" class="tag-button">📄 Paper</a>
      <a href="#" class="tag-button">🧬 arXiv</a>
      <a href="#" class="tag-button">
        <img src="/github2.png" alt="github" style="height: 1.5em; vertical-align: middle;" /> Code</a>
      <a href="#" class="tag-button">💻 Dataset</a>
      <a href="#" class="tag-button">🙌 Visualize</a>
      <a href="#leaderboard" class="tag-button">🏆 Leaderboard</a>
      </div>

      <div class="spacer"></div>

      <h1>Introduction</h1>


      <p class="abstract">
        Answering questions with Chain-of-Thought (CoT) has significantly enhanced the reasoning capabilities of Large Language Models (LLMs), yet its impact on Large Multimodal Models (LMMs) still lacks a systematic assessment and in-depth investigation.
        <br /><br />
In this paper, we introduce <strong>MME-CoT</strong> , a specialized benchmark evaluating the CoT reasoning performance of LMMs, spanning six domains: math, science, OCR, logic, space-time, and general scenes. As the first comprehensive study in this area, we propose a thorough evaluation suite incorporating three novel metrics that assess the reasoning quality, robustness, and efficiency at a fine-grained level.
<br /><br />
Leveraging curated high-quality data and a unique evaluation strategy, we conduct an in-depth analysis of state-of-the-art LMMs, uncovering several key insights: <strong>(1) Models with reflection mechanism demonstrate a superior CoT quality,</strong> with Kimi k1.5 outperforming GPT-4o and demonstrating the highest quality results; <strong>(2) CoT prompting often degrades LMM performance on perception-heavy tasks,</strong> suggesting a potentially harmful overthinking behavior; <strong>(3) Although the CoT quality is high, LMMs with reflection exhibit significant inefficiency in both normal response and self-correction phases. </strong>We hope MME-CoT serves as a foundation for advancing multimodal reasoning in LMMs.
      </p>

      <img class="teaser" src="/img2.png" alt="Teaser image" style="border: none; width: 500px; height: auto;">

    </main>
    <div class="spacer2"></div>
    <h1 id="leaderboard" style="font-size: 20px;">Leaderboard</h1>

    <div class="spacer2"></div>

     <vue3-easy-data-table
      table-class="my-table"
      :headers="headers"
      :items="tableItems"
      show-index
      alternating
      header-text-direction="center"
      body-text-direction="center"
      :rows-per-page="10"
     />

     <div class="carousel-container" style="margin-top: 30px">
      <Splide :options="{ type: 'loop', perPage: 1, autoplay: true }">
       <SplideSlide>
        <img src="/fig1_2.png" alt="Slide 1" />
       </SplideSlide>
       <SplideSlide>
        <img src="/fig2_2.png" alt="Slide 2" />
       </SplideSlide>
       <SplideSlide>
        <img src="/fig3_2.png" alt="Slide 3" />
       </SplideSlide>
     </Splide>
    </div>
    <div class="spacer"></div>

  </div>

  <footer class="page-footer">
  <div class="footer-content">
    This website is adapted from
    <a href="https://mathverse-web.github.io/" class="text-blue-500 hover:underline">MathVerse</a>
    and
    <a href="https://nerfies.github.io/" class="text-blue-500 hover:underline">Nerfies</a>,<br>
    licensed under a
    <a href="https://creativecommons.org/licenses/by-sa/4.0/" class="text-blue-500 hover:underline">
    Creative Commons Attribution-ShareAlike 4.0 International License</a>.
  </div>

</footer>

</template>

<script setup>
import { Splide, SplideSlide } from '@splidejs/vue-splide'
import '@splidejs/vue-splide/css'
import 'vue3-easy-data-table/dist/style.css'
import Vue3EasyDataTable from 'vue3-easy-data-table'
import { ref } from 'vue'

const showDropdown = ref(false)

function toggleDropdown() {
  showDropdown.value = !showDropdown.value
}

const tableItems = [ 
  { rank: 1, model: "Kimi k1.5 🥇", f1: 64.2, precision: 92.0, recall: 49.3, avgscore: 1.4 },
  { rank: 2, model: "GPT-4o 🥈", f1: 64.0, precision: 85.4, recall: 49.0, avgscore: 2.1 },
  { rank: 3, model: "QVQ-72B 🥉", f1: 62.0, precision: 85.4, recall: 49.0, avgscore: 2.1 },
  { rank: 4, model: "Virgo-72B", f1: 60.8, precision: 85.4, recall: 49.0, avgscore: 2.1 },
  { rank: 5, model: "Qwen2-VL-72B", f1: 56.2, precision: 85.4, recall: 49.0, avgscore: 2.1 },
  { rank: 6, model: "InternVL2.5-78B-MPO", f1: 56.2, precision: 85.4, recall: 49.0, avgscore: 2.1 },
  { rank: 7, model: "Qwen2-VL-7B", f1: 56.2, precision: 85.4, recall: 49.0, avgscore: 2.1 },
  { rank: 8, model: "InternVL2.5-8B-MPO", f1: 56.2, precision: 85.4, recall: 49.0, avgscore: 2.1 },
  { rank: 9, model: "InternVL2.5-8B", f1: 56.2, precision: 85.4, recall: 49.0, avgscore: 2.1 },
  { rank: 10, model: "Mulberry", f1: 56.2, precision: 85.4, recall: 49.0, avgscore: 2.1 },
  { rank: 11, model: "MiniCPM-V-2.6", f1: 56.2, precision: 85.4, recall: 49.0, avgscore: 2.1 },
  { rank: 12, model: "LLaVA-OV-72B	", f1: 56.2, precision: 85.4, recall: 49.0, avgscore: 2.1 },
  { rank: 13, model: "LLaVA-CoT", f1: 56.2, precision: 85.4, recall: 49.0, avgscore: 2.1 },
]

const menuItems = [
  { name: 'MME-Survey', link: 'https://example.com/mme-survey', hot: true },
  { name: 'MMSearch', link: 'https://example.com/mmsearch', hot: true },
  { name: 'MathVerse', link: 'https://example.com/mathverse', hot: true },
  { name: 'LLaMA-Adapter (V2)', link: 'https://example.com/llama-v2' },
  { name: 'ImageBind-LLM', link: 'https://example.com/imagebind-llm' },
  { name: 'Point-Bind & Point-LLM', link: 'https://example.com/point-bind' },
  { name: 'PerSAM', link: 'https://example.com/persam' },
  { name: 'CoMat', link: 'https://example.com/comat' },
]

const headers = [
  //{ text: "#", value: "rank" },
  { text: "Model", value: "model" },
  { text: "F1 Score", value: "f1" },
  { text: "Precision", value: "precision" },
  { text: "Recall", value: "recall" },
  { text: "Avg. Score", value: "avgscore" },
  // 继续添加其他表头
] 
  // 更多数据...
</script>

<style scoped>
body {
  margin: 0;
  background: #f9f9f9;
}

.dropdown-container {
  position: relative;
  display: inline-block;
  padding: 1rem;
}

.dropdown-trigger {
  cursor: pointer;
  font-weight: 600;
  color: #2563eb; /* 蓝色文字 */
  position: relative;
}

.dropdown-arrow {
  height: 0.7em;
  vertical-align: middle;
  margin-left: 0.25em;
}

.dropdown-container {
  display: inline-block;
  position: relative;
  padding: 1rem;
  cursor: pointer;
  font-weight: bold;
  color: #2563eb; /* 蓝色 */
}

.dropdown-trigger {
  display: flex;
  align-items: center;
}

.dropdown-arrow {
  height: 0.7em;
  margin-left: 0.25em;
  vertical-align: middle;
}

.dropdown-menu {
  position: absolute;
  left: 0;
  top: 100%;
  margin-top: 0.5rem;
  width: 14rem;
  background-color: #fff;
  border: 1px solid #e5e7eb;
  border-radius: 0.375rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  z-index: 50;
}

.dropdown-item {
  display: block;
  padding: 0.5rem 1rem;
  color: #1f2937;
  text-decoration: none;
}

.dropdown-item:hover {
  background-color: #f3f4f6;
}

.hot-icon {
  margin-right: 0.25em;
}


.hot-icon {
  margin-right: 0.5rem;
}


.container {
  font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
  color: #333;
  background-color: white;
  width: 100%;        
  max-width: 700px; 
  margin: 2rem auto;
  padding: 0 1rem;
}

h1 {
  font-size: 1.8rem;
  margin-bottom: 0.5rem;
}

.tag-button {
  display: inline-block;
  margin: 5px;
  padding: 6px 14px;
  border-radius: 20px;
  background-color: #2f2f2f;
  color: white;
  font-size: 14px;
  text-decoration: none;
  transition: background-color 0.2s;
}
.tag-button:hover {
  background-color: #4a4a4a;
}

sup {
  font-size: 0.6em;
  vertical-align: super;
}


.authors a {
  text-decoration: none;
  color: #007acc;
}

.venue {
  font-weight: bold;
  margin-top: 0.5rem;
}

.links a {
  text-decoration: none;
  color: #444;
  margin-right: 0.5rem;
}

.abstract {
  width: 100%;                  /* 占满父元素 */
  max-width: 1200px;            /* 设置最大宽度限制 */
  margin: 2rem auto;            /* 上下间距 + 居中 */
  padding: 0 1rem;              /* 左右留出空白 */
  line-height: 1.6;
  text-align: justify;         /* 两端对齐 */
  box-sizing: border-box;
}

.teaser {
  max-width: 100%;
  margin-top: 1rem;
  border: 1px solid #ccc;
}

.my-table {
  width: 100%;
  max-width: 700px;
  margin: 0 auto;
  border-collapse: collapse;
  text-align: center;
}

.my-table th,
.my-table td {
  text-align: center;
  padding: 10px;
}

.spacer {
  height: 55px; /* 控制空白高度 */
}
.spacer2 {
  height: 5px; /* 控制空白高度 */
}

.carousel-container img {
  width: 600px;
  height: auto;
  display: block;
  margin: 0 auto; /* 居中 */
}

.page-footer {
  background-color: #f0f0f0; 
  width: 1000px;               /* 占满整个视口宽度 */
  padding: 1rem 0;  
  font-size: 0.85rem;          
  margin-top: 4rem;           /* 与上面内容的间隔 */
}

.footer-content {
  max-width: 1000px;       
  margin: 0 auto;
  padding: 0 1rem;
  text-align: center;
  font-size: 14px;
}

html {
  scroll-behavior: smooth;
}

</style>
