<template>
    <div class="relative">
        <span v-if="alert" class="absolute left-0 top-6 w-1 h-2 transform -translate-y-1/2 bg-white rounded-full rounded-l-none"></span>
        <a @click="$emit('alert')" class="bg-white w-12 h-12 mx-auto mb-4 rounded-full flex items-center justify-center cursor-pointer">
            {{ title }}
        </a>
        <span v-if="notification" class="absolute border-gray-700 border-2 right-2 bottom-0 z-10 rounded-full bg-red-500 w-5 h-5 flex items-center justify-center text-white text-sm">{{notification}}</span>
    </div>
</template>

<script>
export default {
    props: ['title', 'alert', 'notification']
}
</script>

<style>

</style>