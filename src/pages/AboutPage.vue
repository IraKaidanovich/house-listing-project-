<template>
  <div class="page-content">
    <h1 class="title">About DTT Rael Estate</h1>
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
    <h2>Design and Developement</h2>
    <div class="content-web-link">
      <img class="logo" src="@/assets/images/logo.png" alt="logo of DTT company" />
      <div class="web-link">
        <h5 class="web-link-item text">By DTT</h5>
        <a href="www.d-tt.nl" class="web-link-item link">www.d-tt.nl</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AboutPage",
  data() {
    return {
      info: null,
    };
  },
};
</script>

<style>
.page-content {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  text-align: left;
  padding: 0% 15%;
  font-family: Open Sans;
  font-size: 15px;
  color: #4a4b4c;
  font-weight: 300;
}

.title {
  font-family: Montserrat;
  font-size: 32px;
  color: black;
  font-weight: 700;
}

.logo {
  height: 70px;
}

.content-web-link {
  display: flex;
}

.web-link {
  display: flex;
  flex-direction: column;
  padding: 15px 20px;
}

.text {
  margin: 0px;
  font-size: 18px;
  color: black;
  font-weight: 300;
}

.link {
  text-decoration: none;
  color: inherit;
  font-size: 15px;
  font-family: "Montserrat";
  color: #067bc2;
  font-weight: 300;
}
</style>
