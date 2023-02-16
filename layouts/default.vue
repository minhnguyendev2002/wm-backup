<template>
    <div class="flex justify-between">
        <div class="overflow-x-hidden overflow-y-clip w-full">
            <TheHeader />

            <div class="flex-grow custom-scroll">
                <nuxt />
            </div>

            <TheFooter />
        </div>
        <ScrollToTop :scroll="isScroll" />
        <a href="tel:0333867228" class="fixed inline-block sm:hidden text-center top-[calc(100vh-10%)] z-50 w-14 h-14 rounded-full bg-prim-100 !text-white hover:bg-prim-100 transition-all duration-700 right-8">
            <span class="leading-[56px]">
                <i class="fas fa-phone text-lg" />
            </span>
        </a>
    </div>
</template>

<script>
    // import { mapState } from 'vuex';
    import TheHeader from '@/components/layout/TheHeader.vue';
    import TheFooter from '@/components/layout/TheFooter.vue';
    import ScrollToTop from '@/components/shared/ScrollToTop.vue';

    export default {
        components: {
            TheHeader,
            TheFooter,
            ScrollToTop,
        },

        // async fetch() {
        //     await this.fetchData();
        // },

        data() {
            return {
                loading: false,
                isScroll: false,
            };
        },

        // computed: {
        //     ...mapState('settings', ['setting']),
        // },

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

            // async fetchData() {
            //     try {
            //         this.loading = true;
            //         await this.$store.dispatch('settings/fetchAll');
            //     } catch (err) {
            //         this.$handleError(err);
            //     } finally {
            //         this.loading = false;
            //     }
            // },
        },
    };
</script>
