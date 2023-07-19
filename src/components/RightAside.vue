<template>
  <div class="right_wrapper border_wrapper q-pa-sm">
    <div
        v-for="(item, parentIndex) in data"
        :key="parentIndex"
        class="link_item q-pa-sm border_wrapper"
    >
      <div class="title d-flex justify-between">
        <span>{{ item.name }}</span>
        <button
            class="btn_randomize"
            @click="makeRandomizeArr(parentIndex)"
        >
          Перемешать
        </button>
      </div>

      <div class="colors">
        <template v-if="!item.randomize">
          <template
              v-for="(children, childrenIndex) in item.children"
          >
            <div
                v-if="children.value"
                :key="childrenIndex"
                class="parent_color d-flex"
            >
              <div
                  v-for="(indexColor) in children.count"
                  :key="indexColor"
                  :style="{ 'background-color': children.color, 'cursor': 'pointer' }"
                  @click="deleteSquare(parentIndex, childrenIndex)"
                  class="color"
              >
              </div>
            </div>
          </template>
        </template>
        <template v-else>
            <div
                class="random_wrapper"
            >
              <div
                  v-for="(randomColor, randomColorIndex) in item.randomizeArr"
                  :key="randomColorIndex"
                  :style="{ 'background-color': randomColor }"
                  class="randomColor"
              />
            </div>
        </template>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "RightAside",
  props: {
    data: {
      type: Array,
      default() {
        return []
      }
    }
  },
  methods: {
    makeRandomizeArr(parentIndex) {
      const arr = [];
      this.data[parentIndex].children.forEach(item => {
        if (item.value) {
          let count = JSON.parse(JSON.stringify(item.count));
          while (count > 0) {
            arr.push(item.color)
            --count
          }
        }
      })
      this.data[parentIndex].randomizeArr = this.shuffleArray(arr);
      this.data[parentIndex].randomize = true;
    },
    shuffleArray(array) {
      for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
      }
      return array;
    },
    deleteSquare(parentIndex, childrenIndex){
      this.data[parentIndex].children[childrenIndex].count -= 1
    }
  }
}
</script>

<style lang="scss" scoped>
.right_wrapper {
  max-width: 500px;
  width: 100%;
  @media (max-width: 1070px) {
    max-width: 100%;
  }

  .link_item {
    &:not(:last-child) {
      margin-bottom: 10px;
    }

    .parent_color {
      justify-content: flex-start;
      align-items: center;
      flex-wrap: wrap;

      &:not(:last-child) {
        margin-bottom: 10px;
      }

      .color {
        width: 10px;
        height: 10px;
        margin-top: 2px;

        &:not(:last-child) {
          margin-right: 2px;
        }
      }
    }
  }

  .random_wrapper {
    display: flex;
    justify-content: flex-start;
    align-items: flex-start;
    flex-wrap: wrap;
    margin-top: 5px;

    .randomColor {
      width: 10px;
      height: 10px;
      margin-top: 2px;

      &:not(:last-child) {
        margin-right: 2px;
      }
    }
  }


  .btn_randomize {
    padding: 5px 10px;
    background-color: #08a8a8;
    border: none;
    border-radius: 10px;
    color: white;
    outline: none;
    cursor: pointer;
  }
}
</style>