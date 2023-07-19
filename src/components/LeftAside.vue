<template>
  <div class="left_wrapper border_wrapper q-pa-sm">
    <ul>
      <li
          v-for="(list, parentIndex) in data"
          :key="parentIndex"
      >
        <svg
            class="chevron"
            :class="`parent_chevron_${parentIndex}`"
            xmlns="http://www.w3.org/2000/svg"
            height="1em"
            viewBox="0 0 448 512"
            @click="growUl(parentIndex)"
        >
          <path
              d="M207.029 381.476L12.686 187.132c-9.373-9.373-9.373-24.569 0-33.941l22.667-22.667c9.357-9.357 24.522-9.375 33.901-.04L224 284.505l154.745-154.021c9.379-9.335 24.544-9.317 33.901.04l22.667 22.667c9.373 9.373 9.373 24.569 0 33.941L240.971 381.476c-9.373 9.372-24.569 9.372-33.942 0z"/>
        </svg>
        <span
            class="checkbox_wrapper"
            @click="changeParentValue(parentIndex)"
        >
        <input
            v-model="list.value"
            type="checkbox"
            :name="list.field + '_' + parentIndex"
            :id="list.field + parentIndex"
        >
        <span
            v-if="visibleCheckmark(parentIndex)"
            class="checkmark"
            :class="`checkmark_${parentIndex}`"
        />
      </span>
        <label
            :for="list.field + parentIndex"
        >
          {{ list.name }}
        </label>
        <ul
            class="child_ul"
            :class="`child_ul_${parentIndex}`"
        >
          <li
              v-for="(item, childIndex) in list.children"
              :key="childIndex"
              class="d-flex justify-between"
          >
            <span>
                <input
                    v-model="item.value"
                    type="checkbox"
                    :name="item.field + '_' + childIndex"
                    :id="item.field + childIndex"
                    @input="changeChildValue(item.value, parentIndex, childIndex)"
                >
                <label
                    :for="item.field + childIndex"
                >
                  {{ item.name }}
                </label>
            </span>
            <span>
              <span class="counter">{{item.count}}</span>
              <input
                  v-model="item.color"
                  type="color"
                  class="color_picker"
              />
            </span>
          </li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<script>

export default {
  name: "LeftAside",
  props: {
    data: {
      type: Array,
      default() {
        return []
      }
    }
  },
  methods: {
    changeChildValue(value, parentIndex, childIndex) {
      this.$emit(`update:${this.data[parentIndex].children[childIndex].value}`, value);

      setTimeout(_ => {
        if (this.data[parentIndex].children.every(item => !!item.value)) {
          this.data[parentIndex].value = true
        } else if (this.data[parentIndex].children.some(item => !!item.value)) {
          this.data[parentIndex].value = false
        }
      }, 0)

    },
    visibleCheckmark(parentIndex) {
      const data = this.data[parentIndex];
      if (data.children.every(item => !!item.value)) {
        return false
      } else {
        return !!data.children.some(item => !!item.value);
      }
    },
    changeParentValue(parentIndex) {
      const result = this.data[parentIndex].value;
      this.data[parentIndex].value = !result;
      for (const item of this.data[parentIndex].children) {
        item.value = !result;
      }
    },
    growUl(parentIndex) {
      const element = document.querySelector(`.child_ul_${parentIndex}`);
      const chevron = document.querySelector(`.parent_chevron_${parentIndex}`);
      if (element.clientHeight) {
        element.style.height = 0;
        chevron.style.transform = 'rotate(0deg)';
      } else {
        element.style.height = 20 * this.data[parentIndex].children.length + "px";
        chevron.style.transform = 'rotate(-90deg)';
      }
    }
  },
  mounted() {
    this.growUl(0)
  }
}
</script>

<style lang="scss" scoped>
.left_wrapper {
  max-width: 500px;
  width: 100%;

  .child_ul {
    padding-left: 40px;
    -moz-transition: height .5s;
    -ms-transition: height .5s;
    -o-transition: height .5s;
    -webkit-transition: height .5s;
    transition: height .5s;
    height: 0;
    overflow: hidden;
    li{
      max-width: 200px;
      width: 100%;
    }
  }

  .chevron {
    height: 13px;
    margin-right: 5px;
    cursor: pointer;
    transition: all .5s;
  }

  .checkbox_wrapper {
    position: relative;

    .checkmark {
      position: absolute;
      top: calc(50% - 3.5px);
      left: calc(50% - 2.5px);
      height: 5px;
      width: 5px;
      background: black;
      pointer-events: none;
    }
  }

  .counter{
    margin-right: 5px;
  }

  .color_picker{
    padding: 0;
    outline: none;
    background-color: transparent;
    border: none;
    inline-size: 17px;
    block-size: 20px;
    cursor: pointer;
    &::-webkit-color-swatch{
      border: none;
    }
  }
}
</style>