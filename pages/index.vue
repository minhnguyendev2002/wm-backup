<template>
    <div>
        <HomeBanner :data="banners" :loading="loading" />
        <div class="container mx-auto">
            <div class="grid grid-cols-1 lg:grid-cols-2 lg:px-10 py-20 gap-y-10 sm:py-32">
                <div data-aos="fade-right" :data-aos-duration="600" class="lg:mr-24 relative z-[1]">
                    <h2 class="text-3xl sm:text-[40px] sm:leading-[55px] mb-3 font-bold text-second-100 uppercase">
                        Wealth Managament
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
                                hàng đầu tại Châu Á và được thành lập vào năm 2008.  có trụ sở chính tại Singapore. Nó chủ yếu hoạt
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
                    class="flex flex-col lg:flex-row items-center"
                >
                    <div>
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
                        Các quỹ của chúng tôi được quản lý bởi một nhóm các PM chuyên nghiệp khác nhau, Bao gồm các chiến lược từ quản
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
                        leader: 'Rambo',
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
                        leader: 'Ông Tony Cheung',
                        workingTime: '25',
                        tradingStyle: 'Xu hướng là vua, giao dịch dài hạn',
                        profitRate: '52,5',
                    },
                ],
                services: [
                    {
                        id: '0',
                        type: 'forex',
                        source: '<svg x="0px" y="0px" viewBox="0 0 1000 1000" enable-background="new 0 0 1000 1000" xml:space="preserve"><g><path d="M981.2,503.7c-14.8-19.3-48.3-35.4-116,4.6c6.3-28.1-16.1-45.5-42.5-45.5c-23.4,0-50.7,6-72.4,28.1c-31.2-41.1-63.3-36.2-125.7,2.6c-23.8,14.8-44.8,27.4-60.4,36.2c-4.2,2.3-7.5,4.1-10.8,5.9c6.1,1.3,12.3,2.4,19.2,2.4c87.6,0,156.8,0,156.8,76c0,58.4-67.8,75.2-103.7,75.9H463.2c-66.9,0-132.4-69.7-132.4-69.7s77.3,31.7,132.4,31.7h161.9c0.3,0,66.1-2.6,66.1-37.9c0-32.3-17.8-38-118.8-38c-65.9,0-132.6-38.9-132.6-38.9s-66.7-48.7-87.2-61.5c-48.5-30.3-87.2-59-171.9-25.7C127.2,470.9,10,525.5,10,525.5l108,239.7l55.1-35.8c30.5-19.4,47.4-22.7,86.7-2.4c38.1,19.6,155.3,80.5,184.6,94.8c90,43.6,128.7,4.6,172.2-20.5c37.1-21.4,299.9-195.5,327.6-215C987.4,555.8,1000.8,529.2,981.2,503.7z"/><path d="M517.1,322.2v46.9c13.5-2.9,20.2-10.2,20.2-21.7C537.4,337.8,530.6,329.4,517.1,322.2z"/><path d="M486.2,270.1c0,5.8,1.4,10.6,4.1,14.4c2.7,3.8,7.8,7.7,15.1,11.8v-48.4C492.6,250.6,486.2,258,486.2,270.1z"/><path d="M510.1,158.6c-86.4,0-156.6,70.1-156.6,156.6c0,86.4,70.1,156.6,156.6,156.6c86.5,0,156.6-70.1,156.6-156.6C666.7,228.7,596.6,158.6,510.1,158.6z M545.9,372.3c-7.1,6.9-16.7,11.3-28.8,13.1v23.5h-11.7v-22.6c-15.2,0-27.8-3.1-37.8-9.4v-20.1c10,8.2,22.6,12.6,37.8,13.2v-53.4c-16.1-7.5-26.5-14.5-31.3-21.1c-4.7-6.5-7.1-14.2-7.1-23.1c0-10.4,3.6-19.4,10.7-27.1c7.2-7.7,16.4-12.3,27.8-13.8v-19.5h11.7v19.1c14.5,0.6,24.5,2.6,29.7,6.2v19.6c-7.6-5.9-17.5-9-29.7-9.5v55.1c15,6.9,25.4,13.7,31,20.5c5.7,6.8,8.5,14.5,8.5,23C556.6,356.6,553.1,365.4,545.9,372.3z"/></g></svg>',
                        title: 'Giao dịch Forex',
                    },
                    {
                        id: '1',
                        type: 'indices',
                        source: '<svg viewBox="0 0 1024 1024"><path d="M512 870.4c-98.679467 0-183.995733-35.259733-253.559467-104.840533C190.071467 697.1904 154.794667 613.358933 153.6 516.471467v-48.605867l-56.200533 56.200533a17.0496 17.0496 0 1 1-24.132267-24.132266l85.333333-85.333334a17.066667 17.066667 0 0 1 10.922667-4.9664h0.017067a14.8992 14.8992 0 0 1 3.259733 0.1024h0.017067a16.9984 16.9984 0 0 1 9.984 4.949334l85.248 85.248a17.0496 17.0496 0 1 1-24.132267 24.132266L187.733333 467.8656v48.401067c1.0752 87.466667 32.989867 163.293867 94.839467 225.160533C345.514667 804.369067 422.7072 836.266667 512 836.266667s166.485333-31.8976 229.4272-94.839467a347.818667 347.818667 0 0 0 52.053333-65.877333 17.066667 17.066667 0 0 1 29.2352 17.629866 380.757333 380.757333 0 0 1-57.156266 72.379734C695.978667 835.140267 610.679467 870.4 512 870.4z m341.333333-256c-0.7168 0-1.4336-0.0512-2.1504-0.136533h-0.034133a16.9472 16.9472 0 0 1-9.966933-4.949334l-85.248-85.248a17.0496 17.0496 0 1 1 24.132266-24.132266L836.266667 556.1344V512c0-89.2928-31.8976-166.485333-94.839467-229.4272C678.485333 219.648 601.2928 187.733333 512 187.733333s-166.485333 31.914667-229.4272 94.839467a330.222933 330.222933 0 0 0-52.753067 68.1472 17.066667 17.066667 0 1 1-29.5424-17.083733 364.834133 364.834133 0 0 1 58.180267-75.195734C328.004267 188.8768 413.320533 153.6 512 153.6s183.995733 35.2768 253.559467 104.840533S870.4 413.320533 870.4 512v44.1344l56.200533-56.200533a17.0496 17.0496 0 1 1 24.132267 24.132266l-85.333333 85.333334a16.964267 16.964267 0 0 1-10.922667 4.9664h-0.034133A24.064 24.064 0 0 1 853.333333 614.4z"  /><path d="M512 760.32a34.133333 34.133333 0 0 1-34.133333-34.133333v-14.1824c-18.688-5.5296-35.618133-15.837867-50.5856-30.805334C404.224 658.158933 392.533333 630.237867 392.533333 598.186667a34.133333 34.133333 0 0 1 68.266667 0c0 13.653333 4.676267 24.6784 14.7456 34.730666 10.6496 10.666667 22.237867 15.616 36.4544 15.616 13.9776 0 25.173333-4.829867 35.191467-15.2064 11.178667-10.820267 16.008533-22.016 16.008533-35.9936 0-14.216533-4.949333-25.8048-15.598933-36.4544-10.069333-10.069333-20.8384-14.7456-33.8944-14.7456h-2.56c-32.034133 0-60.245333-11.9808-83.8656-35.601066C404.224 487.492267 392.533333 459.281067 392.533333 426.666667c0-32.375467 11.554133-60.757333 34.3552-84.309334 15.394133-14.916267 32.392533-25.002667 50.978134-30.429866v-14.114134a34.133333 34.133333 0 0 1 68.266666 0v14.114134c18.517333 5.410133 35.1744 15.445333 49.749334 30.020266C619.485867 365.568 631.466667 394.069333 631.466667 426.666667a34.133333 34.133333 0 0 1-68.266667 0c0-14.216533-4.949333-25.8048-15.598933-36.4544-10.069333-10.069333-21.367467-14.7456-35.601067-14.7456-14.455467 0-26.1632 4.8128-36.846933 15.1552C465.6128 400.503467 460.8 412.2112 460.8 426.666667c0 14.216533 4.676267 25.531733 14.7456 35.584 10.6496 10.6496 21.9648 15.616 35.601067 15.616h2.56c31.470933 0 59.118933 11.690667 82.176 34.747733C619.485867 536.234667 631.466667 564.736 631.466667 597.333333c0 32.3584-12.4416 61.508267-35.9936 84.2752A113.578667 113.578667 0 0 1 546.133333 711.867733v14.318934a34.133333 34.133333 0 0 1-34.133333 34.133333z"  /></svg>',
                        title: 'Chỉ số quốc tế',
                    },
                    {
                        id: '4',
                        type: 'bitcoin',
                        source: '<svg version="1.2" baseProfile="tiny" viewBox="0 0 256 238" xml:space="preserve"><path d="M122.7,109.9l0.1-30.1c8.5,0,35.2-2.6,35.2,15.2C157.9,112,131.2,109.9,122.7,109.9z M164.8,141.8L164.8,141.8c0.1-19.5-32-16.7-42.2-16.7l-0.1,33.2C132.7,158.3,164.8,160.5,164.8,141.8z M10.6,119.9C10.6,54.9,62.8,2,127.8,2c65,0,117.5,52.5,117.5,117.5c0,65-52.9,117.5-117.5,117.5S10.6,184.6,10.6,119.9z M98.1,113.5c-0.5,0-1,0-1.6,0L96.3,153c-0.3,1.9-1.4,5-5.7,5c0.2,0.2-11,0-11,0l-3.1,18l19.6,0.1c3.7,0,7.2,0.1,10.8,0.1l-0.1,25l15.1,0.1l0.1-24.8c4.1,0.1,8.1,0.1,12,0.2l-0.1,24.7l15.1,0.1l0.1-25c25.3-1.4,43.1-7.7,45.4-31.5c1.8-19.2-7.1-27.7-21.5-31.2c8.8-4.4,14.2-12.2,13-25.3h0c-1.7-17.9-17-23.9-36.5-25.7l0.1-24.8l-15.1-0.1L134.5,62c-4,0-8,0.1-12,0.1l0.1-24.3l-15.1-0.1l-0.1,24.8c-3.3,0.1-6.5,0.1-9.6,0.1l0-0.1l-20.8-0.1L77,78.5c0,0,11.1-0.2,10.9,0c6.1,0,8.1,3.6,8.6,6.6l-0.1,28.2C96.9,113.4,97.5,113.4,98.1,113.5z"/></svg>',
                        title: 'Tiền tệ kỹ thuật số',
                    },
                    {
                        id: '3',
                        type: 'stocks',
                        source: '<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 1000 1000" enable-background="new 0 0 1000 1000" xml:space="preserve"><g><g transform="translate(0.000000,512.000000) scale(0.100000,-0.100000)"><path d="M1422.3,4986c-477.3-126.5-830-504.1-1015.9-1092.6c-95.8-304.8-139.9-609.5-151.4-1077.2l-11.5-417.9H830h586.5l7.7-3214.4c5.8-2574.2,11.5-3235.5,30.7-3312.2c74.8-279.8,226.2-483,440.9-590.4l126.5-61.3h3258.5h3258.5l143.8,44.1c222.3,69,375.7,162.9,546.3,337.4c185.9,187.9,295.2,375.7,394.9,670.9c88.2,256.8,132.3,542.5,132.3,843.4v222.3h-603.8h-603.8V726.9c0,3697.5,5.7,3473.2-107.3,3722.4c-109.3,237.7-314.4,433.2-548.2,519.4l-120.8,46l-3105.2,3.8C1661.9,5022.4,1558.4,5020.5,1422.3,4986z M7711.3,4403.3c84.3-36.4,178.3-138,218.5-241.5c32.6-82.4,34.5-268.4,40.2-3452.1l3.8-3365.9l-1652.3-11.5c-910.5-7.7-2114.2-13.4-2673.9-13.4H2626.1v-195.5c0-695.8-136.1-1173.1-368-1291.9c-88.2-46-145.7-21.1-193.6,84.3l-42.2,90.1L2012.7-7.2l-9.6,3986.9l-42.2,147.6c-23,80.5-59.4,182.1-82.4,224.3l-38.3,78.6h2903.9C7172.7,4430.1,7659.5,4426.3,7711.3,4403.3z M1374.4,4046.8c26.8-70.9,32.6-174.4,40.2-569.3l7.7-484.9H1131H841.5l11.5,120.8c46,465.8,162.9,826.1,341.2,1056.1l59.4,74.8l44.1-55.6C1320.7,4158,1355.2,4094.7,1374.4,4046.8z M9131.6-3307.9c-78.6-366.1-222.4-628.7-414-759c-203.2-136.1-11.5-128.4-3017-128.4H2992.2l59.4,159.1c57.5,159.1,116.9,423.6,139.9,640.2l13.4,118.8l184,5.7c103.5,3.8,1439.5,9.6,2971,11.5l2783.2,3.8L9131.6-3307.9z"/><path d="M5052.7,3690.3c-5.8-17.3-11.5-88.2-11.5-157.2v-128.4l-168.7-5.7c-392.9-11.5-747.5-161-969.9-408.3c-120.8-134.2-208.9-299-272.2-506c-49.8-159.1-53.7-197.4-53.7-517.5c-1.9-304.8,3.8-362.3,42.2-496.5c120.8-419.8,373.8-703.5,776.3-870.2c143.8-61.3,387.2-118.8,496.5-118.8c34.5,0,82.4-5.7,107.3-11.5l42.2-11.5l-3.8-661.3l-5.8-661.3l-607.6,1.9l-609.5,3.8v-404.4v-402.5h613.4h613.4v-141.8c0-212.8-13.4-203.2,251.1-203.2h228.1v170.6v168.7l130.3,13.4c435.1,44.1,849.1,253,1073.4,538.6c101.6,130.3,189.8,310.5,237.7,486.9c53.7,199.3,57.5,586.5,7.7,778.2c-78.6,302.9-254.9,600-479.2,810.8c-243.4,228.1-450.5,310.5-770.6,310.5h-199.3v670.9v670.9h498.4h498.4v392.9v392.9h-195.5c-109.3,0-333.5,5.8-498.4,13.4l-302.9,11.5v151.4v149.5h-228.1C5102.5,3720.9,5062.3,3715.2,5052.7,3690.3z M5041.2,1938.3v-670.9H4978c-34.5,0-113.1,13.4-172.5,28.8c-341.2,88.2-498.4,295.2-498.4,651.7c-1.9,145.7,7.7,189.8,47.9,279.9c55.6,122.7,155.2,230,264.5,285.6c97.8,49.8,256.8,92,350.8,93.9l70.9,1.9V1938.3z M5848.2,445.2c139.9-53.7,237.7-126.5,304.8-228.1c78.6-118.8,103.5-214.7,101.6-396.8c-1.9-274.1-120.8-475.4-339.3-577c-99.7-46-260.7-84.3-348.9-84.3h-46v672.8v674.7l113.1-11.5C5696.7,487.3,5792.6,466.3,5848.2,445.2z"/></g></g></svg>',
                        title: 'Cổ phiếu',
                    },
                    {
                        id: '5',
                        type: 'futures',
                        source: '<svg  viewBox="0 0 52.68 52.68"><g><g><path d="M52.353,30.31c-1.029-2.223-4.032-2.727-5.534-2.836l-0.439,2.968c1.741,0.146,2.987,0.56,3.251,1.129c0.182,0.394-0.167,1.052-0.39,1.41c-0.938,1.503-8.958-0.295-16.832-3.774l-1.213,2.743c3.673,1.625,10.913,4.517,15.896,4.517c2.125,0,3.84-0.525,4.695-1.898C52.989,32.636,52.758,31.188,52.353,30.31z"/><path d="M15.355,26.171c0.385,0.121,0.764,0.236,1.135,0.349c0.038,0.012,0.075,0.022,0.113,0.034c0.361,0.107,0.716,0.213,1.059,0.313l-0.688,0.979l-0.823,1.172l9.252-0.545l-4.438-6.307l-1.474,2.097C9.818,21.544,3.59,18.548,3,16.529c-0.161-0.638,0.236-1.141,0.628-1.318c0.522-0.239,1.903,0.26,2.523,0.649l1.44-2.469c-0.289-0.185-2.957-1.922-5.19-0.918c-0.881,0.395-2.006,1.338-2.365,3.582c-0.677,4.236,8.316,7.914,15.312,10.112C15.352,26.169,15.354,26.169,15.355,26.171z"/><path d="M8.375,18.099c0.437-0.885,0.936-1.734,1.5-2.535c1.271,0.85,2.739,1.59,4.364,2.201c-0.223,0.814-0.403,1.666-0.563,2.533c0.511,0.186,1.042,0.373,1.595,0.561c0.15-0.877,0.323-1.738,0.539-2.559c1.473,0.451,3.06,0.787,4.714,1.016l0.441-0.627l0.526,0.748c0.94,0.102,1.894,0.18,2.874,0.203v3.881l1.677,2.383V19.64c3.04-0.072,5.908-0.538,8.465-1.313c0.626,2.385,0.991,5.035,1.005,7.842h-9.284l0.811,1.152l0.369,0.523h3.415l0.564-1.278l1.829,0.81c0.372,0.164,0.738,0.314,1.105,0.469h1.156c-0.008,0.158-0.023,0.31-0.032,0.465c0.552,0.222,1.096,0.433,1.632,0.631c0.027-0.364,0.061-0.725,0.077-1.096h6.742c-0.083,1.043-0.264,2.06-0.512,3.047c0.593,0.142,1.145,0.258,1.653,0.351c0.389-1.569,0.6-3.211,0.6-4.899c0-4.387-1.394-8.452-3.755-11.785c-0.311-0.439-0.636-0.868-0.98-1.28c-3.752-4.502-9.396-7.373-15.701-7.373c-0.011,0-0.02,0.002-0.03,0.002c-0.007,0-0.012-0.002-0.018-0.002c-0.024,0-0.046,0.004-0.07,0.004c-5.906,0.033-11.37,2.703-14.936,6.637c-1.466,1.598-2.748,3.564-3.185,4.879C7.567,17.731,7.944,17.893,8.375,18.099z M43.958,26.169H37.19c-0.015-2.987-0.413-5.818-1.108-8.37c1.66-0.617,3.158-1.37,4.451-2.234C42.653,18.573,43.922,22.223,43.958,26.169z M39.547,14.283c-1.141,0.747-2.467,1.405-3.941,1.949c-1.085-3.222-2.669-5.902-4.577-7.722C34.385,9.611,37.321,11.639,39.547,14.283z M26.042,7.653c3.404,0.526,6.333,4.052,8,9.098c-2.403,0.712-5.117,1.143-8,1.213V7.653z M24.365,7.641v10.323c-2.917-0.07-5.665-0.511-8.09-1.238C17.959,11.646,20.926,8.112,24.365,7.641z M19.23,8.562c-1.879,1.812-3.439,4.461-4.515,7.64c-1.441-0.538-2.738-1.187-3.857-1.919C13.051,11.678,15.936,9.672,19.23,8.562z"/><path d="M29.288,33.292c-1.059-0.129-2.136-0.225-3.247-0.25v-2.604l-0.521,0.03l-1.156,0.067v2.505c-3.078,0.073-5.98,0.551-8.564,1.344c-0.276-1.051-0.498-2.158-0.664-3.306l-1.667,0.099c0.188,1.297,0.442,2.551,0.767,3.738c-1.625,0.611-3.094,1.354-4.363,2.202c-1.88-2.667-3.09-5.838-3.364-9.272h6.643c0.026,0.602,0.069,1.193,0.126,1.779l1.156-1.646c-1.886-0.595-3.588-1.199-5.146-1.812h-2.84c0.004-0.397,0.029-0.79,0.057-1.182c-0.567-0.262-1.102-0.525-1.612-0.791c-0.074,0.707-0.126,1.419-0.126,2.145c0,4.387,1.395,8.451,3.756,11.783c0.311,0.439,0.637,0.867,0.981,1.28c3.729,4.472,9.324,7.334,15.58,7.37c0.024,0,0.046,0.002,0.07,0.002c0.006,0,0.011,0,0.018,0c0.01,0,0.02,0,0.03,0c6.304,0,11.949-2.87,15.701-7.371c0.344-0.412,0.67-0.842,0.98-1.281c0.07-0.098,0.13-0.203,0.198-0.303c-4.316-0.961-8.884-2.801-11.696-4.045L29.288,33.292z M10.863,38.396c1.118-0.729,2.413-1.377,3.85-1.915c1.076,3.18,2.638,5.826,4.517,7.638C15.936,43.009,13.056,41.001,10.863,38.396z M24.365,45.04c-3.439-0.473-6.41-4.002-8.094-9.082c2.426-0.729,5.175-1.17,8.094-1.24V45.04z M39.544,38.397c-2.226,2.645-5.159,4.674-8.517,5.773c1.908-1.82,3.495-4.498,4.58-7.721C37.08,36.993,38.405,37.651,39.544,38.397zM26.042,45.027v-10.31c2.883,0.07,5.599,0.502,8.004,1.213C32.38,40.979,29.446,44.501,26.042,45.027z"/></g></g></svg>',
                        title: 'Hợp đồng tương lai quốc tế',
                    },
                    {
                        id: '6',
                        type: 'precius',
                        source: '<svg x="0px" y="0px" viewBox="0 0 122.88 107.33" ><g><path class="st0" d="M12.49,28.62l-0.26,0.21c1.72,2.11,2.43,4.6,2.14,7.46c-0.29,2.86-1.5,5.15-3.61,6.87l0.21,0.26 c2.11-1.72,4.6-2.43,7.46-2.13c12.88,1.34,3.67,8.8,4.99-4.07c0.29-2.86,1.5-5.15,3.61-6.87l-0.21-0.26 c-2.11,1.72-4.6,2.43-7.46,2.14C16.5,31.93,14.21,30.73,12.49,28.62L12.49,28.62L12.49,28.62z M31.26,64.84l8.86-31.19 c0.32-1.14,1.36-1.89,2.49-1.89v0H80.4c1.26,0,2.3,0.9,2.54,2.08l9.1,31.15c0.4,1.37-0.39,2.8-1.76,3.2 c-0.24,0.07-0.48,0.1-0.72,0.1v0.01H33.7c-1.43,0-2.59-1.16-2.59-2.59C31.11,65.4,31.16,65.11,31.26,64.84L31.26,64.84z M62,103.86 l8.86-31.19c0.32-1.14,1.36-1.89,2.49-1.89v0h37.79c1.26,0,2.3,0.9,2.54,2.08l9.1,31.15c0.4,1.37-0.39,2.8-1.76,3.2 c-0.24,0.07-0.48,0.1-0.72,0.1v0.01H64.44c-1.43,0-2.59-1.16-2.59-2.59C61.85,104.43,61.9,104.14,62,103.86L62,103.86z M75.3,75.96 l-7.43,26.18h48.99l-7.65-26.18H75.3L75.3,75.96z M0.15,103.86l8.86-31.19c0.32-1.14,1.36-1.89,2.49-1.89v0h37.79 c1.26,0,2.3,0.9,2.54,2.08l9.1,31.15c0.4,1.37-0.39,2.8-1.76,3.2c-0.24,0.07-0.48,0.1-0.72,0.1v0.01H2.59 c-1.43,0-2.59-1.16-2.59-2.59C0,104.43,0.05,104.14,0.15,103.86L0.15,103.86z M13.45,75.96l-7.43,26.18H55l-7.65-26.18H13.45 L13.45,75.96z M44.56,36.94l-7.43,26.18h48.99l-7.65-26.18H44.56L44.56,36.94z M44.31,0l-0.26,0.21c1.72,2.11,2.43,4.6,2.14,7.46 c-0.29,2.86-1.5,5.15-3.61,6.87l0.21,0.26c2.11-1.72,4.6-2.43,7.47-2.13c2.87,0.3,5.16,1.5,6.87,3.6l0.26-0.21 c-1.72-2.11-2.43-4.6-2.14-7.46c0.29-2.86,1.5-5.15,3.61-6.87l-0.21-0.26c-2.11,1.72-4.6,2.43-7.46,2.14 C48.32,3.31,46.03,2.11,44.31,0L44.31,0L44.31,0z M86.63,2.31l-0.47,0.39c3.14,3.86,4.45,8.41,3.91,13.65 c-0.54,5.24-2.74,9.43-6.6,12.57l0.39,0.47c3.86-3.14,8.41-4.45,13.66-3.9c5.24,0.54,9.43,2.75,12.57,6.6l0.47-0.39 c-3.14-3.86-4.45-8.41-3.91-13.65c0.54-5.24,2.74-9.43,6.6-12.57L112.85,5c-3.86,3.14-8.41,4.45-13.65,3.91 C93.96,8.37,89.77,6.17,86.63,2.31L86.63,2.31L86.63,2.31z"/></g></svg>',
                        title: 'Kim loại quý',
                    },
                ],
                banners: [
                    {
                        thumbnail: '/images/banners/default-banner.jpg',
                        title: 'Wealth Managament',
                        subtitle: 'Wealth Managament cung cấp công nghệ tài liệu bằng sáng chế toàn cầu với triết lý: “Đầu tư vững vàng - Thảnh thơi vui sống"',
                    },
                    {
                        thumbnail: '/images/banners/banner-3.jpg',
                        title: 'Wealth Managament',
                        subtitle: 'Wealth Managament cung cấp công nghệ tài liệu bằng sáng chế toàn cầu với triết lý: “Đầu tư vững vàng - Thảnh thơi vui sống"',
                    },
                    {
                        thumbnail: 'https://www.isefpzak.xyz/img/BANNER1.a6b9f634.png',
                        title: 'Wealth Managament',
                        subtitle: 'Wealth Managament cung cấp công nghệ tài liệu bằng sáng chế toàn cầu với triết lý: “Đầu tư vững vàng - Thảnh thơi vui sống"',
                    },
                ],
                typeTrade: [
                    'forex',
                    'indices',
                    'bitcoin',
                    'stocks',
                    'futures',
                    'precius',
                ],
                widgetActive: 'forex',
            };
        },

        methods: {
            changeTypeTradeOverview(key) {
                this.widgetActive = this.typeTrade.includes(key) ? key : 'forex';
                console.log(this.widgetActive);
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
