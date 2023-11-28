<template>
    <div class="p-2 alert" :class="cardColor">
        <h3>{{ cardHeading }}</h3>
        <slot></slot>
    </div>
</template>

<script>

export default {

    props: {
        cardHeading: String,
        cardColor: String,
        myArray: Array,
    }
}

</script>

<style>
.sortable-drag-column {
    min-height: 300px;
}
</style>