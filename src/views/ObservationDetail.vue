<template>
  <ocs-data-loader
    :data-loaded="dataLoaded"
    :data-load-error="dataLoadError"
    :data-not-found="dataNotFound"
  >
    <template v-slot:not-found>
      <not-found />
    </template>
    <h1>Observation {{ id }}</h1>
    <ocs-observation-detail
      :observation="data"
      :request-link="{
        to: { name: 'requestDetail', params: { id: data.request } },
      }"
    />
  </ocs-data-loader>
</template>

<script>
import { OCSMixin } from "ocs-component-lib";
import NotFound from "@/components/NotFound.vue";

export default {
  name: "ObservationDetail",
  components: {
    NotFound,
  },
  mixins: [OCSMixin.getDataMixin],
  props: {
    id: {
      type: [String, Number],
      required: true,
    },
  },
  methods: {
    initializeDataEndpoint: function () {
      return (
        this.$store.state.urls.observationPortalApi +
        "/api/observations/" +
        this.id +
        "/"
      );
    },
  },
};
</script>
