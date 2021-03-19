<template>
  <no-ssr>
    <div>
      <!-- <div class="arrow-paging-set">
        <ul class="paging">
          <li v-for="(item, index) in list" :key="index">
            <button
              type="button"
              :class="{ on: index == pagingNumber }"
              @click="slideGo"
            >
              index
            </button>
          </li>
        </ul>
      </div> -->
      <input ref="input" type="text" />
      <Splide
        ref="primary"
        :options="options"
        :class="`slider-${slliderName}`"
        @splide:moved="moved"
      >
        <template v-if="content">
          <slot name="content"></slot>
        </template>
        <!-- list -->
        <template v-else>
          <SplideSlide v-for="(item, index) in list" :key="index">
            <slot :item="item"></slot>
          </SplideSlide>
        </template>
      </Splide>
    </div>
  </no-ssr>
</template>

<script>
// import { createSlides } from '@splidejs/splide/src/js/utils/slides'
export default {
  name: 'VCarousel',
  props: {
    slliderName: {
      type: String,
      default: '',
    },
    data: {
      type: Array,
      default: () => [],
    },
    options: {
      type: Object,
      default: () => {},
    },
    content: {
      type: Boolean,
      default: false,
    },
  },

  data() {
    return {
      pagingNumber: 1,
      // slides: createSlides(),
      // pagingSize: '',
    }
  },
  computed: {
    list() {
      return this.data.map((item) => ({ ...item }))
    },
    // pagingSize() {
    //   return 14 * list.length
    // },
  },
  mounted() {
    console.log(this.$refs.primary)
  },
  methods: {
    slideGo() {
      console.log(this.slides)
    },
    moved(splide, newIndex) {
      console.log('moved', newIndex)
      this.pagingNumber = newIndex
    },
  },
}
</script>
