<template>
  <OrgChart :data="testData" v-on:onClick="onClick"></OrgChart>
</template>

<script>
  import OrgChart from './org-chart/OrgChart';

  export default {
    name: 'app',
    components: {
      OrgChart
    },
    data() {
      return {
        testData: [
          {
            id: 1,
            label: "Seu Siriguejo",
            children: [
              {
                id: 2,
                label: "Bob Esponja",
                children: [
                  {
                    id: 4,
                    label: "Patrick Estrela",
                    children: []
                  },
                  {
                    id: 5,
                    label: "Sandy Bochechas",
                    children: []
                  }
                ]
              },
              {
                id: 3,
                label: "Lula Molusco",
                children: []
              }
            ]
          }
        ]
      }
    },
    methods: {
      onClick: function (node) {
        console.log(node.label+" was clicked!");
      }
    }
  }

</script>

<style>

</style>