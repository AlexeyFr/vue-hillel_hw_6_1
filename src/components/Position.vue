<template>
  <div>
    <div v-if="loading">Loading...</div>
    <div v-else>
      <router-link class="all_positions" :to="{name: 'positions'}">See all positions</router-link>
      <div class="position">
        <div class="type_location">{{position.type}} / {{position.location}}</div>
        <div class="title">{{position.title}}</div>
        <div class="description" v-html="position.description"></div>
      </div>
    </div>
  </div>
</template>

<script>

  import axios from 'axios';

  export default {
    data () {
      return {
        position: [],
        loading: true,
      }
    },
    created () {
      axios.get(`http://localhost:3000/positions/${this.$route.params.id}.json`)
        .then(res => {
          this.position = res.data;
          this.loading = false;
        })
        .catch(console.log)
    }

  }

</script>

<style scoped>
  .all_positions {
    display: inline-block;
    font-weight: bold;
    color: #1d80be;
    font-size: 14px;
    margin: 20px 0;
  }
  .position {
    width: 560px;
    padding: 15px 24px;
    box-shadow: 0 0 1px 2px #ebebeb;
    margin-bottom: 10px;
  }
  .type_location {
    margin: 15px 0;
    color: #888;
  }
  .title {
    margin: 15px 0 10px 0;
    font-weight: bold;
    padding-bottom: 15px;
    font-size: 22px;
    color: #294455;
    border-bottom: 1px solid #ddd;
  }
</style>