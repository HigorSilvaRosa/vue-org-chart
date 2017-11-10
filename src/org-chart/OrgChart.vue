<template>
  <div class="org-chart-container">
    <div class="org-chart-node-children">
      <OrgChartNode v-for="node in treeData" :node="node" v-on:goUpClick="goUpClick" v-on:goUpDrop="goUpDrop"></OrgChartNode>
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
      let treeNodes = this.getChildren(this.data, null);
      
      return {
        treeData: this.data
      }
    },
    mounted() {

    },
    methods: {
      goUpClick: function (event) {
        this.$emit('onClick', event)
      },
      goUpDrop: function (event) {
        this.$emit('onDrop', event)
      },

      getChildren: function (nodes, parentId) {
        let result = [];
        for (let i in nodes) {
          let node = nodes[i];
          result.push({
            id: node.id,
            parentId: parentId,
            label: node.label
          })
          result = result.concat(this.getChildren(node.children, node.id))
        }
        return result
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