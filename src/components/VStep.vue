<template>
  <transition :name="animationName" :class="{ 'slider': animationName === 'slide' }">
    <div :class="{ 'slot': animationName === 'slide' }" v-if="isActive">
      <slot />
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    stepKey: { required: true, type: Number },
    title: { required: true, type: String },
    icon: { required: false, type: String },
    description: { required: false, type: String }
  },
  data() {
    return {
      isActive: false,
    }
  },
  computed: {
    animationName() {
      if (!this.$parent.animation) {
        return ''
      } else {
        return this.$parent.animation === 'fade' ? 'fade' : 'slide'
      }
    }
  }
}
</script>

<style scoped lang="scss">
.slider{
  overflow: hidden;
  position: relative;
  height: 200px;
  width: 400px;
  
  .slot {
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right:0;
  }
}

/* Slide Animaton */
.slide-leave-active,
.slide-leave-to {
    display: none;
}

.slide-enter-active {
  transition: 1s;
}
.slide-enter {
  transform: translate(100%, 0);
}

/* Fade Animation */
.fade-leave-active,
.fade-leave-to {
  display: none;
}
.fade-enter-active {
  transition: opacity .7s;
}
.fade-enter {
  opacity: 0;
}
</style>