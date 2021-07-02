<template>
  <div>
    <h1>asdasdsad</h1>
    <button @click="drawerActive = !drawerActive">show drawer</button>
    <drawer height="h-2/3" v-model:active="drawerActive">
      <div>
        <p class="h-[999px]">asdasd</p>
      </div>
    </drawer>
  </div>
</template>

<script>
import { defineComponent } from "vue";
import ButtonRepo from "@/components/ButtonRepo.vue";
import Drawer from '@/components/Drawer/index.vue';
export default defineComponent({
  components: { ButtonRepo, Drawer },
  data() {
    return {
      drawerActive: true
    }
  }
});
</script>
