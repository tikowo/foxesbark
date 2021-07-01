<template>
    <div class="fox-nav-small pt-3 bg-gray-900 overflow-auto">
        <Item title="A" :alert="true" :notification="1"/>
        <Item v-for="item in items" :key="item.id" :title="item.title" :alert="item.alert" @alert="item.alert = !item.alert"/>
    </div>
</template>

<script>
import Item from "./Item/index.vue";
export default {
    components: { Item },
    data() {
        return {
            items: [
                {
                    id: 1,
                    title: "C",
                    alert: false
                },
                {
                    id: 2,
                    title: "B",
                    alert: false
                }
            ]
        }
    }
}
</script>

<style lang="scss" scoped>
.fox-nav-small {
    width: 72px;
}
</style>