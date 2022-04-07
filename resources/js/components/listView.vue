<template>
    <div class="mt-4">
        <h4>View Your Tasks</h4>
        <hr class="w-50 m-auto mb-3" />
        <ul class="list-group m-auto">
            <list-item
                :item="item"
                v-on:itemchanged="$emit('reloadlist')"
                v-for="item in items"
                :key="item.id"
                class="m-auto my-1 text-justify text-wrap item"
            />
        </ul>
    </div>
</template>

<script>
import listItem from "./listItem";

export default {
    components: {
        listItem
    },
    props: ["items"]
};
</script>

<style scoped>
.item{
    background: #e6e6e6;
    padding:8px;
    margin-top: 3px;
}
</style>
