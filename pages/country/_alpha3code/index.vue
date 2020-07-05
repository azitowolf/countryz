<template>
  <section class="section">
    <div>single country {{ $route.params.alpha3code }}</div>
    <pre>
      {{JSON.stringify(this.country, 2)}}
    </pre>
  </section>
</template>

<script>
import axios from "axios";
export default {
  name: 'country',
    data() {
    return {
      country: {}
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
        `https://restcountries.eu/rest/v2/alpha/${this.$route.params.alpha3code}`,
        config
      );
      this.country = res.data;
    } catch (e) {
      console.log(e);
    }
  }
};
</script>

<style>
</style>