<template>
    <div>
        <HomeBanner :data="banners" :loading="loading" />
        <div class="container mx-auto">
            <div class="grid grid-cols-1 lg:grid-cols-2 lg:px-10 py-20 gap-y-10 sm:py-32">
                <div data-aos="fade-right" :data-aos-duration="600" class="lg:mr-24 relative z-[1]">
                    <h2 class="text-3xl sm:text-[40px] sm:leading-[55px] mb-3 font-bold text-second-100 uppercase">
                        Wealth Management
                    </h2>
                    <span class="uppercase text-lg font-semibold py-2 text-gray-80 relative">
                        Quản lý tài sản
                    </span>
                    <div class="grid grid-cols-1 lg:grid-cols-1 gap-3 mt-5">
                        <div>
                            <div class="mb-3">
                                <i class="fas fa-caret-right text-xl text-prim-100 mr-3" />
                                <span class="text-xl font-semibold text-second-100">Đội ngũ chuyên gia tư vấn chuyên nghiệp</span>
                            </div>
                            <p class="text-lg">
                                Wealth Management là công ty tư vấn, đầu tư và quản lý tài chính cá nhân chuyên nghiệp hoạt động
                                hàng đầu tại Châu Á và được thành lập vào năm 2008, có trụ sở chính tại Singapore. Nó chủ yếu hoạt
                                động các dịch vụ tài chính cá nhân, dịch vụ ngân hàng tư nhân, dịch vụ ngân hàng thương mại và doanh
                                nghiệp, dịch vụ ngân hàng đầu tư, tài chính doanh nghiệp và thị trường vốn. Kinh doanh, dịch vụ vốn
                                ngoại hối, dịch vụ môi giới tương lai, quản lý tài sản, quản lý vốn đầu tư mạo hiểm, bảo hiểm và dịch
                                vụ môi giới chứng khoán.
                            </p>
                        </div>
                    </div>
                    <nuxt-link
                        to="/about-us"
                        class="!bg-[#f4f4fa] w-64 justify-center mt-10 !text-[#0c4ea4] font-bold py-5 px-8 flex items-center relative hover:!bg-[#0c4ea4] duration-300 hover:!text-white"
                    >
                        <i class="fas fa-minus mr-3 text-lg" /> <span>Xem thêm</span>
                    </nuxt-link>
                </div>
                <div
                    data-aos="fade-left"
                    :data-aos-duration="600"
                    :data-aos-delay="100"
                    class="flex flex-col lg:flex-row items-center w-full"
                >
                    <div class="w-full">
                        <video
                            class="w-full"
                            controls
                            src="/medias/QLTC.mp4"
                        />
                    </div>
                </div>
            </div>
        </div>
        <div class="py-20 relative bg-[url('/images/backgrounds/about.png')] bg-cover bg-no-repeat bg-top">
            <div class="container mx-auto px-10">
                <div class="text-center mb-14">
                    <span
                        class="uppercase text-lg font-semibold pt-5 text-gray-80 relative
                                   after:content-[''] after:absolute after:h-0.5 after:w-6 after:bg-prim-100 after:top-0 after:left-1/2 after:-translate-x-1/2"
                    >Công việc của chúng tôi</span>
                    <h2 class="text-3xl sm:text-[40px] sm:leading-[55px] font-bold text-second-100 mt-3 uppercase">
                        Công việc kinh doanh chính
                    </h2>
                </div>
                <div class="grid grid-cols-12 gap-8">
                    <a
                        v-for="(service, index) in services"
                        :key="service.id"
                        :href="`#${service.type}`"
                        class="group cursor-pointer relative rounded-sm overflow-hidden hover:after:h-full hover:after:top-0 col-span-12 sm:col-span-6 xl:col-span-4 text-center bg-white flex flex-col justify-center items-center
                    after:absolute after:w-full after:bg-prim-100 after:z-[0] after:h-[0%] after:bottom-0 after:transition-all after:duration-1000"
                        :class="[widgetActive === service.type ? '!bg-prim-100' : '']"
                        data-aos="fade-up"
                        :data-aos-duration="600"
                        :data-aos-delay="(index+1) * 100"
                        @click="changeTypeTradeOverview(service.type)"
                    >
                        <div class="block w-full h-full py-14 px-10">
                            <span class="bg-white delay-300 w-[120px] h-[120px] p-5 mx-auto flex justify-center flex-col rounded-full relative z-10">
                                <div class="fill-prim-100 delay-300" v-html="service.source" />
                            </span>
                            <nuxt-link
                                to="/"
                                :class="[widgetActive === service.type ? '!text-white' : '!text-second-100']"
                                class="group-hover:!text-white delay-300 mt-3 text-2xl font-bold relative z-10"
                            >
                                {{ service.title }}
                            </nuxt-link>
                        </div>
                    </a>
                </div>
            </div>
        </div>
        <div class="py-20 relative bg-[url('/images/backgrounds/trade.png')] bg-cover bg-no-repeat bg-center">
            <div v-show="widgetActive === 'forex'" id="forex" class="container">
                <h2 class="text-center text-3xl sm:text-[40px] sm:leading-[55px] font-bold text-second-100 mb-5 uppercase">
                    Giao dịch Forex
                </h2>
                <ForexTrade />
            </div>
            <div v-show="widgetActive === 'indices'" id="indices" class="container">
                <h2 class="text-center text-3xl sm:text-[40px] sm:leading-[55px] font-bold text-second-100 mb-5 uppercase">
                    Chỉ số quốc tế
                </h2>
                <IndicesTrade />
            </div>
            <div v-show="widgetActive === 'stocks'" id="stocks" class="container">
                <h2 class="text-center text-3xl sm:text-[40px] sm:leading-[55px] font-bold text-second-100 mb-5 uppercase">
                    Cổ phiếu
                </h2>
                <StocksTrade />
            </div>
            <div v-show="widgetActive === 'bitcoin'" id="bitcoin" class="container">
                <h2 class="text-center text-3xl sm:text-[40px] sm:leading-[55px] font-bold text-second-100 mb-5 uppercase">
                    Tiền tệ kỹ thuật số
                </h2>
                <BitcoinTrade />
            </div>
            <div v-show="widgetActive === 'futures'" id="futures" class="container">
                <h2 class="text-center text-3xl sm:text-[40px] sm:leading-[55px] font-bold text-second-100 mb-5 uppercase">
                    Hợp đồng tương lai quốc tế
                </h2>
                <FuturesTrade />
            </div>
            <div v-show="widgetActive === 'precius'" id="precius" class="container">
                <h2 class="text-center text-3xl sm:text-[40px] sm:leading-[55px] font-bold text-second-100 mb-5 uppercase">
                    Kim loại quý
                </h2>
                <PreciusTrade />
            </div>
        </div>
        <div class="bg-[#f6f6f6]">
            <div class="container mx-auto py-20">
                <div class="w-full">
                    <h2 class="text-2xl sm:text-[40px] sm:leading-[55px] font-bold text-second-100 uppercase">
                        Đội ngũ chuyên gia
                    </h2>
                    <p class="my-5 text-lg">
                        Wealth Management có đội ngũ quản lý giàu kinh nghiệm đã và đang đầu tư ở Châu Á.
                        Đội ngũ này có văn hóa hợp tác mạnh mẽ giúp chúng tôi nổi bật so với các công ty cùng ngành trên toàn cầu.
                        Các quỹ của chúng tôi được quản lý bởi một nhóm các PM chuyên nghiệp khác nhau, bao gồm các chiến lược từ quản
                        lý tích cực không bị hạn chế đến các phương pháp định lượng có hệ thống.
                    </p>
                    <div class="border-2 border-solid border-gray-20 mt-10">
                        <div
                            v-for="work in workSpaces"
                            :key="work.id"
                            class="flex flex-wrap w-full justify-between px-5 sm:px-16 gap-5 py-5 items-center bg-white border-b-2 border-solid border-gray-20 last:border-b-0"
                        >
                            <div class="flex items-center gap-4 xl:w-auto xl:min-w-[220px]">
                                <img
                                    class="w-[60px] h-[60px] object-cover rounded-full border-2 border-solid border-prim-100"
                                    :src="work.avatar"
                                    alt="members"
                                >
                                <h2 class="text-2xl">
                                    {{ work.name }}
                                </h2>
                            </div>
                            <div class="text-center xl:min-w-[180px]">
                                <span class="text-xl">Trưởng nhóm</span>
                                <h2 class="text-2xl">
                                    {{ work.leader }}
                                </h2>
                            </div>
                            <div class="text-center">
                                <span class="text-xl">Kinh nghiệm</span>
                                <h2 class="text-2xl">
                                    {{ work.workingTime }} năm
                                </h2>
                            </div>
                            <div class="text-left xl:text-center w-full xl:max-w-[30%] order-1 xl:order-none">
                                <span class="text-xl">Phong cách giao dịch</span>
                                <h2 class="text-2xl">
                                    {{ work.tradingStyle }}
                                </h2>
                            </div>
                            <div class="text-center w-full xl:w-auto">
                                <span class="text-xl">Tỷ lệ lợi nhuận <br class="hidden xl:block"> trung bình hàng tháng</span>
                                <h2 class="text-2xl">
                                    {{ work.profitRate }}%
                                </h2>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="container mx-auto">
            <div data-aos="fade-top" data-aos-anchor-placement="top">
                <h2 class="text-2xl text-center sm:text-[40px] sm:leading-[55px] font-bold text-second-100 mt-20 uppercase">
                    Những con số về Wealth Management
                </h2>
                <p class="my-5 text-lg text-center max-w-[1024px] mx-auto">
                    Khách hàng của chúng tôi đến từ 190 quốc gia và đội ngũ của chúng tôi sử dụng 30 ngôn ngữ. Lãnh đạo của chúng tôi đã tới thăm 120 thành phố trên toàn cầu để nắm bắt nhu cầu của khách hàng và đối tác.
                </p>
            </div>
            <div class="relative pb-24 lg:pb-32 pt-12 lg:pt-24 grid grid-cols-12 items-center gap-y-16 gap-5 mt-10">
                <div class="col-span-12 xl:col-span-4">
                    <div class="text-center flex items-center justify-center">
                        <CountUp :value="1000000" class="text-[50px] lg:text-[65px] font-bold" />
                        <span><i class="fas fa-plus text-3xl ml-2" /></span>
                    </div>
                    <span class="mt-10 mx-auto block text-center text-2xl text-prim-100 font-semibold">
                        Khách hàng
                    </span>
                </div>
                <div class="col-span-12 xl:col-span-4">
                    <div class="hidden text-center sm:flex items-center justify-center gap-3">
                        <CountUp :value="2000000000" class="text-[50px] lg:text-[65px] xl:text-[50px] font-bold" />
                        <span><i class="fas fa-plus text-3xl ml-2" /></span>
                    </div>
                    <div class="text-center flex sm:hidden items-center justify-center gap-3">
                        <CountUp :value="2" class="text-[50px] lg:text-[65px] xl:text-[50px] font-bold" />
                        <span class="text-[50px] lg:text-[65px] xl:text-[50px] font-bold">B USD</span>
                        <span><i class="fas fa-plus text-3xl ml-2" /></span>
                    </div>
                    <span class="mt-10 mx-auto block text-center text-2xl text-prim-100 font-semibold">
                        Tổng số vốn quản lý
                    </span>
                </div>
                <div class="col-span-12 xl:col-span-4">
                    <div class="text-center flex items-center justify-center">
                        <CountUp :value="100" class="text-[50px] lg:text-[65px] font-bold" />
                        <span><i class="fas fa-plus text-3xl ml-2" /></span>
                    </div>
                    <span class="mt-10 mx-auto block text-center text-2xl text-prim-100 font-semibold">
                        Đội ngũ chuyên gia QLTC
                    </span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import { mapState } from 'vuex';
    import HomeBanner from '@/components/home/Banner.vue';
    import CountUp from '@/components/home/CountUp.vue';
    import ForexTrade from '@/components/shared/WidgetTrade/Forex.vue';
    import IndicesTrade from '@/components/shared/WidgetTrade/Indices.vue';
    import BitcoinTrade from '@/components/shared/WidgetTrade/Bitcoin.vue';
    import StocksTrade from '@/components/shared/WidgetTrade/Stocks.vue';
    import FuturesTrade from '@/components/shared/WidgetTrade/Futures.vue';
    import PreciusTrade from '@/components/shared/WidgetTrade/Precious.vue';

    export default {
        scrollToTop: true,
        components: {
            CountUp,
            HomeBanner,
            ForexTrade,
            IndicesTrade,
            BitcoinTrade,
            StocksTrade,
            FuturesTrade,
            PreciusTrade,
        },

        data() {
            return {
                loading: false,
                workSpaces: [
                    {
                        id: '0',
                        avatar: 'https://www.isefpzak.xyz/img/team4.5ea82be8.png',
                        name: 'Winners Team',
                        leader: 'Mr. Rambo',
                        workingTime: '20',
                        tradingStyle: 'Giỏi trong việc nắm bắt thị trường xung động ngắn hạn',
                        profitRate: '22,8',
                    },
                    {
                        id: '1',
                        avatar: 'https://www.isefpzak.xyz/img/team3.92a084e8.png',
                        name: 'Golden Team',
                        leader: 'Mr. Philip Wah',
                        workingTime: '19',
                        tradingStyle: 'Giao dịch theo mô hình định lượng toán học',
                        profitRate: '26,3',
                    },
                    {
                        id: '2',
                        avatar: 'https://www.isefpzak.xyz/img/team2.5b26df53.png',
                        name: 'Beast Team',
                        leader: 'Mr. Andrew',
                        workingTime: '22',
                        tradingStyle: 'Giao dịch trung và dài hạn hiệu quả',
                        profitRate: '35,7',
                    },
                    {
                        id: '3',
                        avatar: 'https://www.isefpzak.xyz/img/team1.591d93bd.png',
                        name: 'Long Team',
                        leader: 'Mr. Tony Cheung',
                        workingTime: '25',
                        tradingStyle: 'Xu hướng là vua, giao dịch dài hạn',
                        profitRate: '52,5',
                    },
                ],
                banners: [
                    {
                        thumbnail: '/images/banners/default-banner.jpg',
                        title: 'Wealth Management',
                        subtitle: 'Wealth Management cung cấp công nghệ tài liệu bằng sáng chế toàn cầu với triết lý: “Đầu tư vững vàng - Thảnh thơi vui sống"',
                    },
                    {
                        thumbnail: '/images/banners/banner-3.jpg',
                        title: 'Wealth Management',
                        subtitle: 'Wealth Management cung cấp công nghệ tài liệu bằng sáng chế toàn cầu với triết lý: “Đầu tư vững vàng - Thảnh thơi vui sống"',
                    },
                    {
                        thumbnail: 'https://www.isefpzak.xyz/img/BANNER1.a6b9f634.png',
                        title: 'Wealth Management',
                        subtitle: 'Wealth Management cung cấp công nghệ tài liệu bằng sáng chế toàn cầu với triết lý: “Đầu tư vững vàng - Thảnh thơi vui sống"',
                    },
                ],
            };
        },

        computed: {
            ...mapState('widget', ['widgetActive', 'services']),
        },

        methods: {
            changeTypeTradeOverview(key) {
                this.$store.dispatch('widget/changeTypeTradeOverview', key);
            },
        },

        head() {
            return {
                title: 'Trang chủ',
            };
        },
    };
</script>

<style lang="scss">
    .glass-effect:after {
        background: linear-gradient(90deg,transparent,rgba(255,255,255,.4),transparent);
    }
</style>
