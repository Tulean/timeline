<template>
  <v-timeline class="timeline">
    <v-timeline-item
      v-for="candidate in sortedData"
      :key="candidate._id"
      :color="generator()"
      small
    >
      <template v-slot:opposite>
        <span
          :class="`headline font-weight-bold black--text`"
          v-text="candidate.registered"
        ></span>
      </template>
      <div class="py-4">
        <h2
          :class="`headline font-weight-bold mb-4 black--text`"
          v-text="candidate.name.first + ` ` + candidate.name.last"
        />
        <div v-text="candidate.about" />
        <div v-for="(tag, i) in candidate.tags" :key="i">
          <div v-text="`#` + tag" />
        </div>
      </div>
    </v-timeline-item>
  </v-timeline>
</template>
<script>
import axios from "axios";
import moment from "moment";
export default {
  name: "timeline",
  data() {
    return {
      baseUrl: process.env.VUE_APP_BASE_URL,
      sortedData: null
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    //fetching data from JSON file
    fetchData() {
      axios.get(this.baseUrl + "timeline.json").then(res => {
        this.sortData(res.data);
      });
    },

    //sorting data by date, date format modified to "YYYYMMDD"
    sortData(data) {
      this.sortedData = data.sort(
        (a, b) =>
          moment(a.registered).format("YYYYMMDD") -
          moment(b.registered).format("YYYYMMDD")
      );
    },

    //randomizing colors
    generator() {
      return "#" + ((Math.random() * 0xffffff) << 0).toString(16);
    }
  }
};
</script>
<style scoped>
.timeline {
  padding: 5%;
}
</style>
