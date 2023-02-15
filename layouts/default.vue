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
        <div id="fb-root" />
        <div id="fb-customer-chat" class="fb-customerchat" />
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
