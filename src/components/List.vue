<template>
    <div class="list-group-item mb-2">
        <div>
            {{ name }}
        </div>
    </div>
</template>

<script>

export default {
    name: 'List',
    props: {
        name: String,
    }
}

</script>