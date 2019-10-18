<template>
  <div>
    <div class="mb-5">
      <h1>External API</h1>
      <p>
        Ping an external API by clicking the buttons below. This will call the external API using an access token, and the API will validate it using
        the API's audience value.
      </p>

      <button class="btn btn-primary m-3" @click="callApi('public')">Public</button>
      <button class="btn btn-primary m-3" @click="callApi('private')">Private</button>
      <button class="btn btn-primary m-3" @click="callApi('private-scoped')">Private-Scoped</button>
      <button class="btn btn-primary m-3" @click="callApi('resources')">Resources</button>
      <br />
      <input v-model="parameter" class="m-3" placeholder="Enter User ID:" />
      <button
        class="btn btn-primary m-3"
        @click="callApi('private/')"
      >Resources-With-Slash-Parameter</button>
      <button
        class="btn btn-primary m-3"
        @click="callApi('private-resources')"
      >Resources-With-Query-Parameter</button>
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
      parameter: ""
    };
  },
  methods: {
    async callApi(endpoint) {
      const accessToken = await this.$auth.getAccessToken();

      try {
        var url = externalApiConfig.url + endpoint;

        if (endpoint == "private-resources") {
          url += "?user_id=" + this.parameter;
        } else if (endpoint == "private/") {
          url += this.parameter;
        }

        const { data } = await this.$http.get(url, {
          headers: {
            Authorization: `Bearer ${accessToken}`
          }
        });

        this.apiMessage = data;
        this.executed = true;
      } catch (e) {
        this.apiMessage = `Error: the server responded with '${e.response.status}: ${e.response.statusText}'`;
      }
    }
  }
};
</script>
