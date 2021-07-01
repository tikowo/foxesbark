<template>
  <div>
    <h1>
      asdasdsad
    </h1>

    <div @touchmove="touchstart" @touchend="touchend" :style="`--tw-translate-y:${positionY}px`" :class="{transition: !(positionY-50)}" class="fixed inset-x-0 bottom-0 h-1/2 bg-gray-300 rounded-t-lg  transform-gpu">
        <p>ajlksdjaslkd</p>
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue'
import ButtonRepo from '@/components/ButtonRepo.vue'

export default defineComponent({
  components: { ButtonRepo },
  data() {
    return {
      positionY: 50,
      lastPosition:0,
      heights: ['h-1/2', 'h-2/3']
    }
  },
  computed: {
    drawerStyles() {
      return {
        transform: this.transform
      }
    }
  },
  methods: {
    touchstart(e) {
      this.positionY -= this.lastPosition ? this.lastPosition - e.touches[0].clientY: 0;
      this.lastPosition = e.touches[0].clientY;
      if(this.positionY < 0) {
        this.positionY = 0;
      }
    },
    touchend() {
      this.lastPosition = 0;
      this.positionY = 50;
    },
  }
})
</script>
