<template>
  <div>
    <div class="mb-5">
      <h1>Resources</h1>
      <p>Add keywords to your account.</p>
      <input v-model="keyword" class="m-3" placeholder="Enter Keyword:" />
      <button class="btn btn-primary m-3" @click="callApi('resources/')">Add</button>
    </div>

    <div class="result-block-container">
      <div :class="['result-block', executed ? 'show' : '']">
        <h6 class="muted">Result</h6>
        <pre v-highlightjs="JSON.stringify(apiMessage, null, 4)">
          <code class="js rounded"></code>
        </pre>
      </div>
    </div>
  </div>
</template>

<script>
import externalApiConfig from "../../external_api_config.json";

export default {
  name: "Api",
  data() {
    return {
      apiMessage: null,
      executed: false,
      keyword: ""
    };
  },
  methods: {
    async callApi(endpoint) {
      const accessToken = await this.$auth.getAccessToken();
      // console.log(accessToken);

      try {
        var url = externalApiConfig.url + endpoint;

        const { data } = await this.$http.post(url, this.keyword, {
          headers: {
            Authorization: `Bearer ${accessToken}`
          },
          params: {
            keyword: this.keyword,
          }
        });

        this.apiMessage = data;
        this.executed = true;
      } catch (e) {
        this.executed = false;
      }
    }
  }
};
</script>
