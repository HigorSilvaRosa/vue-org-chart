<template>
  <div class="org-chart-node">
    <div class="org-chart-node-label" v-on:click="clickNode" v-draggable.nodes="node"  v-droppable.nodes="dropNode">
      {{ node.label }}
    </div>
    <div class="org-chart-node-children" v-if="node.children.length > 0">
      <OrgChartNode v-for="childNode in node.children" :node="childNode"  v-on:goUpClick="goUpClick" v-on:goUpDrop="goUpDrop" ></OrgChartNode>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'OrgChartNode',
    components: {
    },
    props: {
      node: {
        required: true,
      }
    },
    data() {
      return {}
    },
    mounted() {
    },
    methods: {
      clickNode: function (event) {
        this.$emit('goUpClick', this.node)
      },
      goUpClick: function(event){
        this.$emit('goUpClick', event)
      },
      dropNode: function(node){
        this.$emit('goUpDrop', {
          node: JSON.parse(node),
          to: this.node
        })
      },
      goUpDrop: function(event){
        this.$emit('goUpDrop', event)
      },
    }
  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  /*Now the CSS*/
  
  * {
    margin: 0;
    padding: 0;
  }
  
  .org-chart-node-children {
    padding-top: 20px;
    position: relative;
    transition: all 0.5s;
    -webkit-transition: all 0.5s;
    -moz-transition: all 0.5s;
  }
  
  .org-chart-node {
    float: left;
    text-align: center;
    list-style-type: none;
    position: relative;
    padding: 20px 5px 0 5px;
    transition: all 0.5s;
    -webkit-transition: all 0.5s;
    -moz-transition: all 0.5s;
  }
  /*We will use ::before and ::after to draw the connectors*/
  
  .org-chart-node::before,
  .org-chart-node::after {
    content: '';
    position: absolute;
    top: 0;
    right: 50%;
    border-top: 1px solid #ccc;
    width: 50%;
    height: 20px;
  }
  
  .org-chart-node::after {
    right: auto;
    left: 50%;
    border-left: 1px solid #ccc;
  }
  /*We need to remove left-right connectors from elements without 
any siblings*/
  
  .org-chart-node:only-child::after,
  .org-chart-node:only-child::before {
    display: none;
  }
  /*Remove space from the top of single children*/
  
  .org-chart-node:only-child {
    padding-top: 0;
  }
  /*Remove left connector from first child and 
right connector from last child*/
  
  .org-chart-node:first-child::before,
  .org-chart-node:last-child::after {
    border: 0 none;
  }
  /*Adding back the vertical connector to the last nodes*/
  
  .org-chart-node:last-child::before {
    border-right: 1px solid #ccc;
    border-radius: 0 5px 0 0;
    -webkit-border-radius: 0 5px 0 0;
    -moz-border-radius: 0 5px 0 0;
  }
  
  .org-chart-node:first-child::after {
    border-radius: 5px 0 0 0;
    -webkit-border-radius: 5px 0 0 0;
    -moz-border-radius: 5px 0 0 0;
  }
  /*Time to add downward connectors from parents*/
  
  .org-chart-node-children .org-chart-node-children::before {
    content: '';
    position: absolute;
    top: 0;
    left: 50%;
    border-left: 1px solid #ccc;
    width: 0;
    height: 20px;
  }
  
  .org-chart-node-label {
    box-shadow: 0 2px 5px 0 rgba(0,0,0,0.16), 0 2px 10px 0 rgba(0,0,0,0.12);
    display: inline-block;
    padding: 10px;
    margin: 0px;
    border: 1px solid #cccccc;
    font-size: 16px;
  }

  .org-chart-node-label:hover{
    background: #eeeeee;
  }
</style>