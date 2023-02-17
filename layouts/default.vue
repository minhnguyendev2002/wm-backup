<template>
    <div class="flex justify-between">
        <div class="overflow-x-hidden overflow-y-clip w-full">
            <TheHeader />

            <div class="flex-grow custom-scroll">
                <nuxt ref="nuxt" />
            </div>

            <TheFooter />
        </div>
        <ScrollToTop :scroll="isScroll" />
        <a href="tel:0588888548" class="fixed inline-block sm:hidden text-center top-[calc(100vh-10%)] z-50 w-14 h-14 rounded-full bg-prim-100 !text-white hover:bg-prim-100 transition-all duration-700 right-8">
            <span class="leading-[56px]">
                <i class="fas fa-phone text-lg" />
            </span>
        </a>
    </div>
</template>

<script>
    import TheHeader from '@/components/layout/TheHeader.vue';
    import TheFooter from '@/components/layout/TheFooter.vue';
    import ScrollToTop from '@/components/shared/ScrollToTop.vue';

    export default {
        components: {
            TheHeader,
            TheFooter,
            ScrollToTop,
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
