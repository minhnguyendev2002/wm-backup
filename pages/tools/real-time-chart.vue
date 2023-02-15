<template>
    <div class="w-screen lg:px-10 !h-[calc(100vh-100px)]">
        <TradingView
            :options="{
                autosize: true,
                symbol: 'NASDAQ:AAPL',
                interval: 'D',
                timezone: 'Etc/UTC',
                theme: 'light',
                style: '1',
                locale: 'en',
                toolbar_bg: '#f1f3f6',
                enable_publishing: false,
                hide_side_toolbar: false,
                allow_symbol_change: true,
                width: '100%',
                height: '100%'
            }"
        />
    </div>
</template>

<script>
    import TradingView from 'vue-trading-view';

    export default {
        layout: 'tool',
        components: {
            TradingView,
        },
        data() {
            return {

            };
        },
    };
</script>
