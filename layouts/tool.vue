<template>
    <div class="flex justify-between">
        <div class="overflow-x-hidden overflow-y-clip w-full">
            <TheHeader />

            <div class="flex-grow custom-scroll">
                <nuxt />
            </div>
        </div>
    </div>
</template>

<script>
    import TheHeader from '@/components/layout/TheHeader.vue';

    export default {
        components: {
            TheHeader,
        },

        data() {
            return {
                loading: false,
                isScroll: false,
            };
        },

        created() {
            window.addEventListener('scroll', this.handleScroll, true);
        },

        beforeDestroy() {
            window.removeEventListener('scroll', this.handleScroll, true);
        },

        methods: {
            handleScroll() {
                if (window.scrollY > 200) {
                    this.isScroll = true;
                } else {
                    this.isScroll = false;
                }
            },
        },
    };
</script>
