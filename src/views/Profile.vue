<template>
  <div class="container">
    <div class="row align-items-center profile-header">
      <div class="col-md-2 mb-3">
        <img
          :src="profile.picture"
          alt="User's profile picture"
          class="rounded-circle img-fluid profile-picture"
        />
      </div>
      <div class="col-md text-center text-md-left">
        <h2>{{ profile.name }}</h2>
        <p class="lead text-muted">{{ profile.email }}</p>
        <button class="btn btn-secondary" @click="deleteUser()">Remove Account</button>
      </div>
    </div>

    <div class="row">
      <pre v-highlightjs="JSON.stringify(profile, null, 2)" class="rounded w-100">
        <code class="json"></code>
      </pre>
    </div>
  </div>
</template>

<script>
// import authConfig from "../../auth_config.json";

export default {
  data() {
    return {
      profile: this.$auth.profile
    };
  },
  methods: {
    handleLoginEvent(data) {
      this.profile = data.profile;
    },
    async deleteUser() {
      try {
        if (confirm("Do you really want to delete?")) {
          await this.$http.delete("http://localhost:5000/api/users", {
            headers: {
              Authorization: `Bearer ${await this.$auth.getAccessToken()}`
            }
          });

          const accessToken =
            "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6IlFqQTNRelF3T0RBeVEwSTVRemN4TkVNNE1EVTFNVGcyT1VNelJFTTVSa1ExTnpOR056RkZNQSJ9.eyJpc3MiOiJodHRwczovL3JhbmthaS5ldS5hdXRoMC5jb20vIiwic3ViIjoibGxESjZrQVUweXlUcEFiZWRSallEbUw4VWdpSmZoQ2NAY2xpZW50cyIsImF1ZCI6Imh0dHBzOi8vcmFua2FpLmV1LmF1dGgwLmNvbS9hcGkvdjIvIiwiaWF0IjoxNTcxNzQ3MDI4LCJleHAiOjE1NzE4MzM0MjgsImF6cCI6ImxsREo2a0FVMHl5VHBBYmVkUmpZRG1MOFVnaUpmaENjIiwic2NvcGUiOiJyZWFkOmNsaWVudF9ncmFudHMgY3JlYXRlOmNsaWVudF9ncmFudHMgZGVsZXRlOmNsaWVudF9ncmFudHMgdXBkYXRlOmNsaWVudF9ncmFudHMgcmVhZDp1c2VycyB1cGRhdGU6dXNlcnMgZGVsZXRlOnVzZXJzIGNyZWF0ZTp1c2VycyByZWFkOnVzZXJzX2FwcF9tZXRhZGF0YSB1cGRhdGU6dXNlcnNfYXBwX21ldGFkYXRhIGRlbGV0ZTp1c2Vyc19hcHBfbWV0YWRhdGEgY3JlYXRlOnVzZXJzX2FwcF9tZXRhZGF0YSBjcmVhdGU6dXNlcl90aWNrZXRzIHJlYWQ6Y2xpZW50cyB1cGRhdGU6Y2xpZW50cyBkZWxldGU6Y2xpZW50cyBjcmVhdGU6Y2xpZW50cyByZWFkOmNsaWVudF9rZXlzIHVwZGF0ZTpjbGllbnRfa2V5cyBkZWxldGU6Y2xpZW50X2tleXMgY3JlYXRlOmNsaWVudF9rZXlzIHJlYWQ6Y29ubmVjdGlvbnMgdXBkYXRlOmNvbm5lY3Rpb25zIGRlbGV0ZTpjb25uZWN0aW9ucyBjcmVhdGU6Y29ubmVjdGlvbnMgcmVhZDpyZXNvdXJjZV9zZXJ2ZXJzIHVwZGF0ZTpyZXNvdXJjZV9zZXJ2ZXJzIGRlbGV0ZTpyZXNvdXJjZV9zZXJ2ZXJzIGNyZWF0ZTpyZXNvdXJjZV9zZXJ2ZXJzIHJlYWQ6ZGV2aWNlX2NyZWRlbnRpYWxzIHVwZGF0ZTpkZXZpY2VfY3JlZGVudGlhbHMgZGVsZXRlOmRldmljZV9jcmVkZW50aWFscyBjcmVhdGU6ZGV2aWNlX2NyZWRlbnRpYWxzIHJlYWQ6cnVsZXMgdXBkYXRlOnJ1bGVzIGRlbGV0ZTpydWxlcyBjcmVhdGU6cnVsZXMgcmVhZDpydWxlc19jb25maWdzIHVwZGF0ZTpydWxlc19jb25maWdzIGRlbGV0ZTpydWxlc19jb25maWdzIHJlYWQ6ZW1haWxfcHJvdmlkZXIgdXBkYXRlOmVtYWlsX3Byb3ZpZGVyIGRlbGV0ZTplbWFpbF9wcm92aWRlciBjcmVhdGU6ZW1haWxfcHJvdmlkZXIgYmxhY2tsaXN0OnRva2VucyByZWFkOnN0YXRzIHJlYWQ6dGVuYW50X3NldHRpbmdzIHVwZGF0ZTp0ZW5hbnRfc2V0dGluZ3MgcmVhZDpsb2dzIHJlYWQ6c2hpZWxkcyBjcmVhdGU6c2hpZWxkcyBkZWxldGU6c2hpZWxkcyByZWFkOmFub21hbHlfYmxvY2tzIGRlbGV0ZTphbm9tYWx5X2Jsb2NrcyB1cGRhdGU6dHJpZ2dlcnMgcmVhZDp0cmlnZ2VycyByZWFkOmdyYW50cyBkZWxldGU6Z3JhbnRzIHJlYWQ6Z3VhcmRpYW5fZmFjdG9ycyB1cGRhdGU6Z3VhcmRpYW5fZmFjdG9ycyByZWFkOmd1YXJkaWFuX2Vucm9sbG1lbnRzIGRlbGV0ZTpndWFyZGlhbl9lbnJvbGxtZW50cyBjcmVhdGU6Z3VhcmRpYW5fZW5yb2xsbWVudF90aWNrZXRzIHJlYWQ6dXNlcl9pZHBfdG9rZW5zIGNyZWF0ZTpwYXNzd29yZHNfY2hlY2tpbmdfam9iIGRlbGV0ZTpwYXNzd29yZHNfY2hlY2tpbmdfam9iIHJlYWQ6Y3VzdG9tX2RvbWFpbnMgZGVsZXRlOmN1c3RvbV9kb21haW5zIGNyZWF0ZTpjdXN0b21fZG9tYWlucyByZWFkOmVtYWlsX3RlbXBsYXRlcyBjcmVhdGU6ZW1haWxfdGVtcGxhdGVzIHVwZGF0ZTplbWFpbF90ZW1wbGF0ZXMgcmVhZDptZmFfcG9saWNpZXMgdXBkYXRlOm1mYV9wb2xpY2llcyByZWFkOnJvbGVzIGNyZWF0ZTpyb2xlcyBkZWxldGU6cm9sZXMgdXBkYXRlOnJvbGVzIHJlYWQ6cHJvbXB0cyB1cGRhdGU6cHJvbXB0cyByZWFkOmJyYW5kaW5nIHVwZGF0ZTpicmFuZGluZyIsImd0eSI6ImNsaWVudC1jcmVkZW50aWFscyJ9.pqQQLl_tQz9rX1-bL2fhn5NJ8f0S9Q6-kN8T77C1l_b69gAe1P6ixFlaa_rt4OXhu6zvgLI7D9a6g-6bmkHdtH7N4A3PkmCU2yopb-zuGnMB505PaoYZjZXb-v87LXSb3sJfd7XK8ydFY1MdsWQ2VQbWbcig8pGG6eBeglrwD8TOlc3pp-BQb6fAxjYZYgh-XBZpjBtQdAa64zWOCIiSZ20x_wC3ZJP3dbCMphI8VU9TeiZR856OPVGrm-7T9c-9vvTUUsyUl3FKt8JMA_B3rYVpxp0O_Fzbgdjcj972UX7Lgk1iZBDoQUcikXo3nwhqKtMmO90spmcL8yUOCs-2ag";

          await this.$http.delete(
            "https://rankai.eu.auth0.com/api/v2/users/" + this.profile.sub,
            {
              headers: {
                Authorization: `Bearer ${accessToken}`
              }
            }
          );

          window.location.reload();
        }
      } catch (e) {
        // eslint-disable-next-line
        console.log(e);
      }
    }
  }
};
</script>
