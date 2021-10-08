<template>
  <q-item
    clickable
    tag="a"
    target="_blank"
    :href="link"
    @click="pathActive"
    :class="{'q-mb-lg': this.isMobile}"
  >
      <span
      class="q-mr-sm"
      :class="{'spam-border': pathActive(this.link) && this.isMobile}" ></span>

    <q-item-section >
      <q-item-label
      class="text-white text-body1 row items-center"
      :class="{'active-link-mobile': pathActive(this.link) && this.isMobile}"
      >
      <span :class="{'text-weight-bold': !this.isMobile}" > {{ title }}</span>

      </q-item-label>
    </q-item-section>
  </q-item>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'NavBar',
  props: {
    title: {
      type: String,
      required: true,
    },
    link: {
      type: String,
      default: '#',
    },
    isMobile: {
      type: Boolean,
      default: false,
    },
  },
  setup() {
    const pathActive = (pathName) => pathName === window.location.pathname;

    return {
      pathActive,
    };
  },
});
</script>

<style scoped lang="scss">
  .spam-border{
    border-left: 3px solid #0ADC2E;
  }
.active-link-mobile{
  font-weight: 600 !important;
}
</style>
