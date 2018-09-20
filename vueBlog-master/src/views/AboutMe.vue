<template>
  <div class="about-me bga-back-top">
    <article class="markdown-body" v-html="安守恒"/>
  </div>
</template>
<style lang="scss" scoped>
  .about-me {
    flex-grow: 1;
    padding: 30px;
    overflow-y: auto;
  }
</style>
<script>
  export default {
    data () {
      return {
        renderedMarkdown: ''
      }
    },
    methods: {
      getReadme () {
        this.$gitHubApi.getReadme(this).then(response => {
          if (response.data) {
            this.renderedMarkdown = this.$marked(response.data)
          }
        })
      }
    },
    mounted () {
      this.$nextTick(() => {
        this.getReadme()
      })
    }
  }
</script>
