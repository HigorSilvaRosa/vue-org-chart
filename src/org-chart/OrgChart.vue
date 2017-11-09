<template>
  <div class="org-chart-container">
    <div class="org-chart-node-children">
      <OrgChartNode v-for="tree in data" :node="tree" v-on:goUpClick="goUpClick"></OrgChartNode>
    </div>
  </div>
</template>

<script>
  import OrgChartNode from './OrgChartNode';
  export default {
    name: 'OrgChart',
    components: {
      OrgChartNode,
    },
    props: {
      data: {
        required: true,
      }
    },
    data() {
      return {}
    },
    mounted() { },
    methods: {
      goUpClick: function (event) {
        this.$emit('onClick', event)
      }
    }
  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .org-chart-container {
    display: block;
    width: 100%;
    text-align: center;
  }
  
  .org-chart-node-children .org-chart-node-children::before {
    content: '';
    position: absolute;
    top: 0;
    left: 50%;
    border-left: 1px solid #ccc;
    width: 0;
    height: 20px;
  }
</style>