<template>
    <div class="flex justify-between">
        <div class="overflow-x-hidden overflow-y-clip w-full">
            <TheHeader />

            <div class="flex-grow custom-scroll">
                <nuxt ref="nuxt" />
            </div>

            <TheFooter />
        </div>
        <span class="fixed  cursor-pointer inline-block sm:hidden text-center bottom-[120px] z-50 w-14 h-14 rounded-full bg-prim-100 !text-white hover:bg-prim-100 transition-all duration-700 right-4 sm:right-8" @click="showPhone = !showPhone">
            <span class="leading-[56px]">
                <i class="fas text-lg" :class="[showPhone ? 'fa-times' : 'fa-phone']" />
            </span>
            <ul v-if="showPhone" class="absolute -left-[170px] -top-4 mb-0 flex flex-col gap-2">
                <li class="bg-prim-100 px-3 py-2 rounded">
                    <a class="!text-white font-semibold" href="tel:0904588802">Di Động: 0904588802</a>
                </li>
                <li class="bg-prim-100 px-3 py-2 rounded">
                    <a class="!text-white font-semibold" href="tel:0588888548">Cơ quan: 0588888548</a>
                </li>
            </ul>
        </span>
        <div class="fixed w-14 h-14 bottom-[50px] rounded-full right-4 sm:right-8 z-50">
            <a href="https://zalo.me/0588888548" class="text-center relative z-10">
                <img class="w-full h-full" src="/images/zalo-icon.png" alt="zalo">
            </a>
        </div>
    </div>
</template>

<script>
    import TheHeader from '@/components/layout/TheHeader.vue';
    import TheFooter from '@/components/layout/TheFooter.vue';

    export default {
        components: {
            TheHeader,
            TheFooter,
        },

        data() {
            return {
                loading: false,
                isScroll: false,
                showPhone: false,
            };
        },

        created() {
            window.addEventListener('scroll', this.handleScroll, true);
        },

        beforeDestroy() {
            window.removeEventListener('scroll', this.handleScroll, true);
        },

        methods: {
        },
    };
</script>
