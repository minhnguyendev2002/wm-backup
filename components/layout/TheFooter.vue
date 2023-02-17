<template>
    <footer class="relative">
        <div class="absolute z-[-1] bg-[url('/images/backgrounds/shape-4.png')] bg-cover bg-no-repeat bg-center w-full h-full" />
        <div class="container mx-auto">
            <div class="footer-top text-white py-24">
                <div class="grid grid-cols-12 gap-y-8">
                    <div class="col-span-12 md:col-span-6 xl:col-span-4">
                        <div>
                            <img class="w-[280px] sm:w-[260px] xl:w-[380px] bg-[#fff] p-3 rounded-md mb-4" src="/images/logo.jpg" alt="/">
                            <div class="my-5">
                                <span class="text-xl text-white/70 block">
                                    Gọi cho chúng tôi
                                </span>
                                <a class="!text-prim-100 text-3xl hover:underline" href="tel:0588888548">
                                    058.8888.548
                                </a>
                                <div class="font-medium text-xl text-white mt-3">
                                    Chăm sóc khách hàng 24/7
                                </div>
                            </div>
                            <!-- <ul class="flex items-center gap-5">
                                <li>
                                    <nuxt-link
                                        aria-label="About us on Facebook"
                                        class="w-12 h-12 leading-[48px] block !text-white !bg-[#1b1e83] hover:!bg-prim-100 transition-all duration-500 text-center relative z-10 rounded-full"
                                        to="/"
                                    >
                                        <i class="fab fa-facebook-f" />
                                    </nuxt-link>
                                </li>
                                <li>
                                    <nuxt-link
                                        aria-label="About us on Twitter"
                                        class="w-12 h-12 leading-[48px] block !text-white !bg-[#1b1e83] hover:!bg-prim-100 transition-all duration-500 text-center relative z-10 rounded-full"
                                        to="/"
                                    >
                                        <i class="fab fa-twitter" />
                                    </nuxt-link>
                                </li>
                                <li>
                                    <nuxt-link
                                        aria-label="About us on Instagram"
                                        class="w-12 h-12 leading-[48px] block !text-white !bg-[#1b1e83] hover:!bg-prim-100 transition-all duration-500 text-center relative z-10 rounded-full"
                                        to="/"
                                    >
                                        <i class="fab fa-instagram" />
                                    </nuxt-link>
                                </li>
                                <li>
                                    <nuxt-link
                                        aria-label="About us on Dribbble"
                                        class="w-12 h-12 leading-[48px] block !text-white !bg-[#1b1e83] hover:!bg-prim-100 transition-all duration-500 text-center relative z-10 rounded-full"
                                        to="/"
                                    >
                                        <i class="fab fa-dribbble" />
                                    </nuxt-link>
                                </li>
                            </ul> -->
                        </div>
                    </div>
                    <div class="col-span-12 md:col-span-6 xl:col-span-2">
                        <div>
                            <span class="text-2xl leading-9 font-bold text-white mb-7 block">
                                Giới thiệu về WM
                            </span>
                            <div>
                                <ul class="flex flex-col gap-3">
                                    <li class="flex items-center gap-3">
                                        <nuxt-link to="/about-us" class="flex-1 font-medium !text-lg !text-white/70">
                                            Giới thiệu
                                        </nuxt-link>
                                    </li>
                                    <li class="flex items-center gap-3">
                                        <a
                                            class="flex-1 font-medium !text-lg !text-white/70 hover:!text-prim-100 transition-all duration-500"
                                            href="/gift"
                                        >
                                            Giải thưởng WM
                                        </a>
                                    </li>
                                </ul>
                            </div>
                        </div>
                    </div>
                    <div class="col-span-12 md:col-span-6 xl:col-span-3">
                        <div class="">
                            <span class="text-2xl leading-9 font-bold text-white mb-7 block">
                                Sản phẩm giao dịch
                            </span>
                            <div>
                                <ul class="flex flex-col gap-3">
                                    <li
                                        v-for="service in services"
                                        :key="service.id"
                                        class="flex items-center gap-3"
                                        @click="changeTypeTradeOverview(service.type)"
                                    >
                                        <a
                                            class="flex-1 block font-medium !text-lg !text-white/70 hover:!text-prim-100 transition-all duration-500"
                                            :href="path !== '/' ? `/#${service.type}` : `#${service.type}`"
                                        >
                                            {{ service.title }}
                                        </a>
                                    </li>
                                </ul>
                            </div>
                        </div>
                    </div>
                    <div class="col-span-12 md:col-span-6 xl:col-span-3">
                        <div>
                            <span class="text-2xl leading-9 font-bold text-white mb-7 block">
                                Liên hệ
                            </span>
                            <div>
                                <ul class="flex flex-col gap-3">
                                    <li class="flex items-center gap-3">
                                        <span class="w-12 h-12 leading-[48px] block !text-white !bg-[#1b1e83] text-center relative z-10 rounded-full"><i class="fas fa-phone" /></span>
                                        <a
                                            class="flex-1 font-medium !text-lg !text-white/70 hover:!text-prim-100 transition-all duration-500"
                                            href="tel:0588888548"
                                        >
                                            058.8888.548
                                        </a>
                                    </li>
                                    <li class="flex items-center gap-3">
                                        <span class="w-12 h-12 leading-[48px] block !text-white !bg-[#1b1e83] text-center relative z-10 rounded-full"><i class="fas fa-comment" /></span>
                                        <span class="flex-1 font-medium !text-lg !text-white/70">
                                            wealthmanagement.qltc@gmail.com
                                        </span>
                                    </li>
                                    <li class="flex items-center gap-3">
                                        <span class="w-12 h-12 leading-[48px] block !text-white !bg-[#1b1e83] text-center relative z-10 rounded-full"><i class="fas fa-map-pin" /></span>
                                        <span class="flex-1 font-medium !text-lg !text-white/70">
                                            Wealth Managament Address
                                        </span>
                                    </li>
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="text-center">
                <div class="bg-second-100 border-t-[1px] border-solid border-white/10">
                    <p class="mb-0 text-white py-7">
                        © Copyright 2023 by
                        <nuxt-link to="/" class="!text-white">
                            Wealth Managament
                        </nuxt-link>
                    </p>
                </div>
            </div>
        </div>
    </footer>
</template>

<script>
    import { mapState } from 'vuex';

    export default {
        props: {
            data: {
                type: Object,
                default: () => {},
            },
        },
        data() {
            return {
            };
        },

        computed: {
            ...mapState('widget', ['services']),
            path() {
                return this.$route.path;
            },
        },

        methods: {
            changeTypeTradeOverview(key) {
                console.log(this.$route.path);
                this.$store.dispatch('widget/changeTypeTradeOverview', key);
            },
        },
    };
</script>
