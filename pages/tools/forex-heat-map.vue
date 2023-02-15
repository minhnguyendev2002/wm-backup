<template>
    <div class="w-screen lg:px-10 !h-[calc(100vh-100px)]">
        <ForexMap ref="ForexMap" />
    </div>
</template>

<script>
    import ForexMap from '@/components/shared/WidgetTrade/ForexMap.vue';

    export default {
        layout: 'tool',
        components: {
            ForexMap,
        },
        mounted() {
            this.$nextTick(() => {
                this.$forceUpdate();
            });
        },
    };
</script>
