<template>
  <section class="section">
    <div class="columns is-multiline">
      <!-- Country CARDS HERE -->
      <div
        v-for="country in countries.slice(0,25)"
        :key="country.alpha3Code"
        :title="country.name"
        class="column is-one-fifth"
      >
        <div class="card">
          <div class="card-header">{{country.name}}</div>
          <div class="card-content">
            info about countries
            <!-- add info -->
          </div>
          <div class="card-image">
            <figure class="image is-4by3">
              <img :src="country.flag" alt="Placeholder image" />
            </figure>
          </div>
        </div>
        <nuxt-link :to="`/country/${country.alpha3Code}`">Go to Country</nuxt-link>
      </div>
    </div>
  </section>
</template>

<script>
import Card from "~/components/Card";
import axios from "axios";

export default {
  name: "HomePage",
  components: {
    Card
  },
  head() {
    return {
      title: "rest countries - test app"
    };
  },
  data() {
    return {
      countries: []
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      const res = await axios.get(
        "https://restcountries.eu/rest/v2/all",
        config
      );
      this.countries = res.data;
    } catch (e) {
      console.log(e);
    }
  }
};
</script>
