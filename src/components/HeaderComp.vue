<script lang="ts">
import SearchComp from './SearchComp.vue';
export default {
    name: "HeaderComp",
    components: {
        SearchComp,
    },
}
</script>

<template>
    <div class="row m-1 p-4">
        <div class="col">
            <div class="h1 text-primary text-center mx-auto">
                    <i class="fa fa-check bg-primary text-white rounded p-2"></i>
                    <u>My Todo-s</u>
            </div>
        </div>
    </div>
    <div class="p-2 mx-4 border-black-25 border-bottom"></div>
</template>

<style scoped>
u {
    margin-left: 10px;
}
</style>