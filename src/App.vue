<template>
  <div
    id="app"
    class="container-fluid">
    <div class="row">
      <div class="col-12 col-md-10 mx-auto">
        <QuizFront />
      </div>
    </div>
  </div>
</template>

<script>
import QuizFront from './components/QuizFront.vue';
import ResizeObserver from 'resize-observer-polyfill';

export default {
  name: 'App',
  components: {
    QuizFront
  },
  data() {
    return {}
  },
  created() {
    const quizName = this.$route.query.quizName;
    this.$store.dispatch('fetchData', quizName);
  },
  mounted() {
    const elementRoot = this.$root.$el;
    const resizeObserver = new ResizeObserver(entries => {
      for (const entry of entries) {
        const {
          height
        } = entry.contentRect;
        const elementHeight = 'elementHeight:' + height;
        // console.log(elementHeight);
        parent.postMessage(elementHeight, '*');
      }
    });
    resizeObserver.observe(elementRoot);
  },
  methods: {

  },
}
</script>

<style lang="scss">
@import "./styles/custom";
</style>
