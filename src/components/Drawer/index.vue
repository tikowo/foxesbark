<template>
  <div
    @touchmove="touchstart"
    @touchend="touchend"
    :style="`--tw-translate-y:${hidden ? '100%' : positionY + 'px'}`"
    :class="{ transition, [height]: true }"
    class="fixed inset-x-0 bottom-0 bg-gray-300 rounded-t-lg transform-gpu"
  >
    <div
      v-if="active || mode != 'remove'"
      id="drawer-content"
      class="h-full overflow-y-auto"
    >
      <slot></slot>
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    active: {
      type: Boolean,
      required: true,
    },
    height: {
      type: String,
      default: "h-1/2",
    },
    mode: {
      type: String,
      default: "remove",
    },
  },
  watch: {
    active() {
      if (this.active) {
        this.show();
      } else {
        this.hide();
      }
    },
  },
  data() {
    return {
      positionY: 0,
      lastPosition: 0,
      transition: false,
      hidden: true,
      heights: ["h-1/2", "h-2/3", "h-full"],
    };
  },
  computed: {
    drawerStyles() {
      return {
        transform: this.transform,
      };
    },
  },
  mounted() {
    if (this.active) {
      this.show();
    }
  },
  methods: {
    show() {
      this.hidden = false;
      document.body.classList.add("overflow-hidden");
      this.animateTo(0);
      this.$emit("update:active", true);
    },
    hide() {
      this.addAndRemoveTransition();
      this.hidden = true;
      document.body.classList.remove("overflow-hidden");
      this.$emit("update:active", false);
    },
    touchstart(e) {
      const drawerContent = document.getElementById("drawer-content");

      if (drawerContent.scrollTop > 0) {
        return;
      }

      this.positionY -= this.lastPosition
        ? this.lastPosition - e.touches[0].clientY
        : 0;

      this.lastPosition = e.touches[0].clientY;

      if (this.positionY < 0) {
        this.positionY = 0;
      }
    },
    touchend() {
      if (this.positionY > 50) {
        this.hide();
      } else {
        this.animateTo(0);
      }
      this.lastPosition = 0;
    },

    animateTo(y) {
      this.addAndRemoveTransition();
      this.positionY = y;
    },
    addAndRemoveTransition() {
      this.transition = true;
      setTimeout(() => {
        this.transition = false;
      }, 300);
    },
  },
});
</script>
