<template>
    <div class="bg-transparent w-full">
        <div class="relative partner-carousel px-2 pb-3 mt-1 z-10 sm:px-5">
            <VueSlickCarousel key="partner-list" ref="SliderCarousel" v-bind="settings">
                <div v-for="(partner, index) in partners" :key="index" class="pointer-events-none ">
                    <img :src="partner.logo" class="w-full object-cover" alt="/">
                </div>
                <template #prevArrow>
                    <div slot="prev-arrow" class="absolute !top-[115%] !left-[44%] lg:!left-[47%] sm:pl-0 z-[100]">
                        <a-icon type="left" class="text-4xl !text-black-100/20 hover:!text-black-100 duration-200 cursor-pointer mr-3" />
                    </div>
                </template>
                <template #nextArrow>
                    <div slot="next-arrow" class="absolute !top-[115%] !right-[44%] lg:!right-[48%] sm:pl-0 z-[100]">
                        <a-icon type="right" class="text-4xl !text-black-100/20 hover:!text-black-100 duration-200 cursor-pointer" />
                    </div>
                </template>

                <template #customPaging>
                    <div slot="custom-paging" class="mt-4">
                        <span class="block mx-auto w-2 h-2 rounded-full bg-gray-80 duration-300" />
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
        components: { VueSlickCarousel },

        data() {
            return {
                settings: {
                    speed: 600,
                    dots: false,
                    infinity: true,
                    autoplay: true,
                    autoplaySpeed: 3000,
                    arrows: true,
                    slidesToShow: 6,
                    slidesToScroll: 6,
                    responsive: [
                        {
                            breakpoint: 1080,
                            settings: {
                                slidesToShow: 4,
                                slidesToScroll: 4,
                            },
                        },
                        {
                            breakpoint: 800,
                            settings: {
                                slidesToScroll: 3,
                                slidesToShow: 3,
                                arrows: false,
                            },
                        },
                        {
                            breakpoint: 640,
                            settings: {
                                slidesToShow: 3,
                                slidesToScroll: 1,
                                arrows: false,
                            },
                        },
                    ],
                },
                partners: [
                    { logo: '/images/partners/ACB.png' },
                    { logo: '/images/partners/ANZ.png' },
                    { logo: '/images/partners/ATGlobal.png' },
                    { logo: '/images/partners/BIDV.jpg' },
                    { logo: '/images/partners/Citibank.jpg' },
                    { logo: '/images/partners/eToro.webp' },
                    { logo: '/images/partners/FXCM.jpg' },
                    { logo: '/images/partners/IC.jpg' },
                    { logo: '/images/partners/MB.jpg' },
                    { logo: '/images/partners/StandardChartered.jpg' },
                    { logo: '/images/partners/Techcombank.png' },
                    { logo: '/images/partners/Vietcombank.jpg' },
                    { logo: '/images/partners/XM.jpg' },
                ],
            };
        },
    };
</script>
<style lang="scss">
    .partner-carousel {
        .slick-prev:before, .slick-next:before {
            content: '' !important;
        }
        .slick-list {
            padding: 10px 0px !important;
            overflow: initial !important;
        }
        .slick-slide {
            float: right !important;
            padding: 0px 15px !important;
            height: 100% !important;
        }
        .slick-slider {
            margin: 0px -15px !important;
        }
    }
</style>
