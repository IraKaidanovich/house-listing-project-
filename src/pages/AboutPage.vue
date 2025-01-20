<template>
  <div class="page-content" :class="{ 'page-content-dark': isDarkMode }">
    <h1 class="title" :class="{ 'title-dark': isDarkMode }">
      About Real Estate
    </h1>
    <p>
      From a student room in 2010 to a full-service digital agency in the heart
      of Amsterdam. Our story is one of those. A story we are very proud of.
      <br /><br />
      We - the over 50 enthusiastic strategists, designers, developers and
      testers - who work together daily on the most beautiful projects. And we
      have been doing this for small and large clients - from independent
      entrepreneurs, startups, the public sector and SMEs, to multinationals
      like Randstad and nonprofits like Greenpeace. <br /><br />
      Clients with diverse objectives, target groups and resources, challenging
      us time and again to develop a suitable digital solution. As a team, this
      makes us rich in experience, flexible and enormously versatile. And that
      is precisely where our strength lies.
    </p>
  </div>
</template>

<script setup>
import { ref, inject } from "vue";

const isDarkMode = inject("isDarkMode");

const info = ref(null);
</script>

<style>
.page-content {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  text-align: left;
  padding: 0% 15% 60%;
  font-family: Open Sans;
  font-size: 15px;
  color: #4a4b4c;
  font-weight: 300;
}

.page-content-dark {
  color: white;
  background-color: #2c2e30;
}

.title {
  font-family: Montserrat;
  font-size: 32px;
  color: black;
  font-weight: 700;
}

.title-dark {
  color: white;
}
</style>
