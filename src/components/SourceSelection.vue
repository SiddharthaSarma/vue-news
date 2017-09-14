<template>
  <div class="source-selection">
    <div class="jumbotron">
      <h4>Select News source</h4>
      <div class="form-group">
        <select class="form-control" id="sources" v-on:change="sourceChanged">
          <option value="-1">Select a new source</option>
          <option v-bind:value="source.id" v-bind:key="source.id" v-for="source in sources">{{source.name}}</option>
        </select>
        <div v-if="source">
          <p><small v-text="source.description"></small></p>
          <a :href="source.url" target="_blank" class="btn btn-primary">Go to {{source.name}}</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'sourceselection',
  data() {
    return {
      sources: [],
      source: ''
    }
  },
  methods: {
    sourceChanged: function(event) {
      this.source = null;
      for (var i = 0; i < this.sources.length; i++) {
        if (this.sources[i].id === event.target.value) {
          this.source = this.sources[i];
        }
      }
      this.$emit('sourceChanged', this.source);
    }
  },
  created() {
    axios.get('https://newsapi.org/v1/sources?language=en').then((response) => this.sources = response.data.sources);
  }
}
</script>
