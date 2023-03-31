<template>
    <div class="flex flex-col">
        <div class=" banner-carousel mt-1 flex-1 h-full">
            <a-empty v-if="dataCarousel.length === 0" class="!mt-20" />
            <VueSlickCarousel
                v-else
                key="banner"
                ref="SliderCarousel"
                v-bind="settings"
                @beforeChange="afterChangeSlide"
            >
                <div v-for="banner in dataCarousel" :key="banner._id" class="">
                    <div class="relative w-full h-full py-16 sm:pt-[120px] sm:pb-[100px]">
                        <div
                            :style="{ backgroundImage: `url(${banner.thumbnail || '/images/banners/default-banner.jpg'})` }"
                            class="animate-[zoom-up_3s_linear_1s_forwards]
                            absolute top-0 z-[0] w-full h-full after:absolute after:content-[''] after:top-0 after:left-0 after:w-full after:h-full after:opacity-40 after:bg-[#0c4ea4] bg-cover bg-no-repeat bg-center"
                        />
                        <div class="container mx-auto text-center lg:text-right min-h-[300px] md:min-h-[400px] xl:min-h-[550px] flex flex-col">
                            <div class="overflow-y-hidden flex flex-col justify-center items-center mb-auto flex-1">
                                <transition name="translate-y-transition">
                                    <div v-if="titleAnimate">
                                        <h1 class="text-5xl lg:text-[80px] font-bold lg:leading-[90px] text-white relative z-[1] animate-[fade-top_1s_linear_.5s_forwards] opacity-0 translate-y-[100%]">
                                            {{ banner.title || 'Wealth Management' }}
                                        </h1>
                                        <h2 class="xl:max-w-[70%] ml-auto relative z-[1] text-2xl sm:text-3xl font-medium mb-11 text-white animate-[fade-top_.7s_linear_1s_forwards] opacity-0 translate-y-[100%]">
                                            {{ banner.subtitle || 'Wealth Management cung cấp công nghệ tài liệu bằng sáng chế toàn cầu với triết lý: “Đầu tư vững vàng - Thảnh thơi vui sống"' }}
                                        </h2>

                                        <a
                                            href="https://www.vncrmrosy.com/pc/user/regist"
                                            aria-hidden="false"
                                            class="!bg-[#f4f4fa] ml-auto mr-auto lg:mr-0 lg:ml-auto mt-auto z-[1] w-64 justify-center !text-[#0c4ea4] font-bold py-5 px-8 flex items-center relative hover:!bg-[#0c4ea4] duration-300 hover:!text-white
                                                    animate-[fade-top_.7s_linear_1.5s_forwards] opacity-0 translate-y-[100%]"
                                        >
                                            <i class="fas fa-minus mr-3 text-lg" /> <span>Đăng ký ngay</span>
                                        </a>
                                    </div>
                                </transition>
                            </div>
                        </div>
                    </div>
                </div>

                <template #prevArrow>
                    <div slot="prev-arrow" class="absolute -top-3 !-left-[260px] !w-11 !h-11 !text-center rounded-full !border-solid !border-spacing-1 duration-300 hover:!border-gray-200">
                        <i class="isax isax-arrow-left text-black text-3xl" />
                    </div>
                </template>
                <template #nextArrow>
                    <div slot="next-arrow" class="absolute -top-3 !-right-36 !w-11 !h-11 !text-center rounded-full !border-solid !border-spacing-1 duration-300 hover:!border-gray-200">
                        <i class="isax isax-arrow-right text-black text-3xl" />
                    </div>
                </template>

                <template #customPaging>
                    <div slot="custom-paging">
                        <span class="block mx-auto w-20 h-1 rounded-full bg-white duration-300" />
                    </div>
                </template>
            </VueSlickCarousel>
        </div>
    </div>
</template>

<script>
    import VueSlickCarousel from 'vue-slick-carousel';
    import 'vue-slick-carousel/dist/vue-slick-carousel-theme.css';
    import 'vue-slick-carousel/dist/vue-slick-carousel.css';

    export default {
        components: {
            VueSlickCarousel,
        },

        props: {
            data: {
                type: Array,
            },
            loading: {
                type: Boolean,
                default: false,
            },
            path: {
                type: String,
                default: '/',
            },
            title: {
                type: String,
                default: 'Record',
            },
        },

        data() {
            return {
                titleAnimate: true,
                dataCarousel: this.banners || this.data?.length > 0 ? this.data.slice(0, 5) : Array(5).fill({}),
                settings: {
                    speed: 1000,
                    autoplaySpeed: 1000,
                    dots: false,
                    fade: true,
                    arrows: true,
                    slidesToShow: 1,
                    slidesToScroll: 1,
                    autoplay: false,
                    delay: 5000,
                    responsive: [
                        {
                            breakpoint: 1280,
                            settings: {
                                arrows: false,
                            },
                        },
                    ],
                },
            };
        },

        computed: {
        },

        watch: {
            data: {
                handler() {
                    this.dataCarousel = this.data.slice(0, 5) || [];
                    this.$refs.SliderCarousel.onPropsUpdated();
                },
                deep: true,
            },
        },

        methods: {
            afterChangeSlide() {
                this.titleAnimate = false;
                setTimeout(() => {
                    this.titleAnimate = true;
                }, 0);
            },
        },
    };
</script>

<style lang="scss">
    .banner-carousel {
        .slick-slider {
            @apply h-full;
        }
        .slick-prev:before, .slick-next:before {
            content: '' !important;
        }
        .slick-list {
            padding: 0px 0px !important;
            // @apply h-[79vh] lg:h-[calc(100vh-100px)] #{!important};
        }
        .slick-track {
            height: 100%;
        }
        .lick-slide {
            float: right !important;
        }
        .slick-dots {
            bottom: -6px;
            @apply xl:pr-28;
            .slick-active {
                span {
                    @apply w-20 bg-black relative;
                }
            }
            li {
                @apply w-20 mx-1;
            }
        }
        p {
            @apply mb-0
        }
    }
</style>
