<template>
  <div ref="holder">
    <div class="error hidden"><br>Data is missing or unavailable for metric: <p style="color: black !important">{{ title }}</p></div>
    <div class="bargraphchart hidefirst invis">
      <vega-lite :spec="spec" :data="values"></vega-lite>
      <p> {{ chart }} </p>
    </div>
  </div>
</template>


<script>
import { mapState } from 'vuex'
import AugurStats from 'AugurStats'

export default {
  props: ['source', 'citeUrl', 'citeText', 'title'],
  data() {
    return {
      values: []
    }
  },
  computed: {
    repo() {
      return this.$store.state.baseRepo
    },
    gitRepo () {
      return this.$store.state.gitRepo
    },
    spec() {
      let config = {
        "$schema": "https://vega.github.io/schema/vega-lite/v3.json",
        "data": { "values": []},
        "title": this.title,
        "width": (this.$el) ? this.$el.offestWidth : 800,
        "height": 400,
        "autosize": "fit",
        "mark": "bar",
        "encoding": {
          "y": {"field": "count",
                "type": "quantitative"},
          "x": {"field": "gender",
                "type": "nominal"},
          "color": {"field": "gender",
                    "type": "nominal"}
        }
      }
      $(this.$el).find('.showme').addClass('invis')
      $(this.$el).find('.textchart').addClass('loader')
      if (this.repo) {
        window.AugurRepos[this.repo][this.source]().then((data) => {
          $(this.$el).find('.showme, .hidefirst').removeClass('invis')
          $(this.$el).find('.bargraphchart').removeClass('loader')
          this.values = data
          console.log('Data:')
          console.log(data)
        })
      }
      return config
    }

}
}

</script>