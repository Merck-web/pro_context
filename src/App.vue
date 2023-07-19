<template>
  <div id="app">
    <div class="container">
      <div class="border_wrapper">
        <div class="d-flex justify-between q-pa-sm">
          <LeftAside
              :data.sync="checkBoxes"
              @allChecked="obj => checkBoxes[obj.index].value = obj.value"
          />
          <RightAside
              :data.sync="checkBoxes"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import LeftAside from "@/components/LeftAside.vue";
import RightAside from "@/components/RightAside.vue";

export default {
  name: 'App',
  components: {
    RightAside,
    LeftAside
  },
  data() {
    return {
      checkBoxes: [
        {
          name: "list 1",
          field: "list",
          value: false,
          randomize: false,
          randomizeArr: [],
          children: [
            {
              name: "item 1",
              field: "itemForOne",
              value: false,
              count: 10,
              color: '#FF0000'
            },
            {
              name: "item 2",
              field: "itemForOne",
              value: false,
              count: 16,
              color: '#FFFF00'
            },
            {
              name: "item 3",
              field: "itemForOne",
              value: false,
              count: 40,
              color: '#32CD32'
            },
            {
              name: "item 4",
              field: "itemForOne",
              value: false,
              count: 0,
              color: '#0000FF'
            },
          ]
        },
        {
          name: "list 2",
          field: "list",
          value: false,
          randomize: false,
          randomizeArr: [],
          children: [
            {
              name: "item 1",
              field: "itemForTwo",
              value: false,
              count: 10,
              color: '#FF0000'
            },
            {
              name: "item 2",
              field: "itemForTwo",
              value: false,
              count: 16,
              color: '#FFFF00'
            },
            {
              name: "item 3",
              field: "itemForTwo",
              value: false,
              count: 40,
              color: '#32CD32'
            },
            {
              name: "item 4",
              field: "itemForTwo",
              value: false,
              count: 0,
              color: '#0000FF'
            },
          ]
        },
        {
          name: "list 3",
          field: "list",
          value: false,
          randomize: false,
          randomizeArr: [],
          children: [
            {
              name: "item 1",
              field: "itemForThree",
              value: false,
              count: 10,
              color: '#FF0000'
            },
            {
              name: "item 2",
              field: "itemForThree",
              value: false,
              count: 16,
              color: '#FFFF00'
            },
            {
              name: "item 3",
              field: "itemForThree",
              value: false,
              count: 40,
              color: '#32CD32'
            },
            {
              name: "item 4",
              field: "itemForThree",
              value: false,
              count: 0,
              color: '#0000FF'
            },
          ]
        },
        {
          name: "list 4",
          field: "list",
          value: false,
          randomize: false,
          randomizeArr: [],
          children: [
            {
              name: "item 1",
              field: "itemForFour",
              value: false,
              count: 10,
              color: '#FF0000'
            },
            {
              name: "item 2",
              field: "itemForFour",
              value: false,
              count: 16,
              color: '#FFFF00'
            },
            {
              name: "item 3",
              field: "itemForFour",
              value: false,
              count: 40,
              color: '#32CD32'
            },
            {
              name: "item 4",
              field: "itemForFour",
              value: false,
              count: 0,
              color: '#0000FF'
            },
          ]
        },
      ]
    }
  },
}
</script>

