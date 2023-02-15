<template>
    <div :id="container" ref="tradingview" class="tradingview-widget-container">
        <div class="tradingview-widget-container__widget" />
    </div>
</template>

  <script>
    const SCRIPT_ID = 'tradingview-widget-script';
    const CONTAINER_ID = 'tradingview-widget-container';

    export default {
        name: 'MarketOverview',
        props: {
            options: {
                type: Object,
                default: () => ({
                    colorTheme: 'light',
                    dateRange: '12M',
                    showChart: true,
                    locale: 'en',
                    largeChartUrl: '',
                    isTransparent: false,
                    showSymbolLogo: true,
                    showFloatingTooltip: false,
                    width: '100%',
                    height: '660',
                    plotLineColorGrowing: 'rgba(228, 167, 54, 1)',
                    plotLineColorFalling: 'rgba(228, 167, 54, 1)',
                    gridLineColor: 'rgba(240, 243, 250, 1)',
                    scaleFontColor: 'rgba(120, 123, 134, 1)',
                    belowLineFillColorGrowing: 'rgba(228, 167, 54, 0.12)',
                    belowLineFillColorFalling: 'rgba(228, 167, 54,0.12)',
                    symbolActiveColor: 'rgba(228, 167, 54, 0.12)',
                    tabs: [
                        {
                            title: 'Indices',
                            symbols: [
                                {
                                    s: 'CME_MINI:ES1!',
                                    d: 'S&P 500',
                                },
                                {
                                    s: 'CME:6E1!',
                                    d: 'Euro',
                                },
                                {
                                    s: 'FX:USDJPY',
                                    d: 'USD/JPY',
                                },
                                {
                                    s: 'COMEX:GC1!',
                                    d: 'Gold',
                                },
                                {
                                    s: 'NYMEX:CL1!',
                                    d: 'Crude Oil',
                                },
                                {
                                    s: 'NYMEX:NG1!',
                                    d: 'Natural Gas',
                                },
                                {
                                    s: 'CBOT:ZC1!',
                                    d: 'Corn',
                                },
                            ],
                            originalTitle: 'Indices',
                        },
                    ],
                }),
            },
        },
        data() {
            return {
                container: CONTAINER_ID,
            };
        },
        mounted() {
            setTimeout(() => {
                this.appendScript(this.initWidget);
            }, 300);
        },
        methods: {
            canUseDOM() {
                return typeof window !== 'undefined' && window.document && window.document.createElement;
            },
            getScriptElement() {
                return document.getElementById(SCRIPT_ID);
            },
            updateOnloadListener(onload) {
                const script = this.getScriptElement();
                const oldOnload = script.onload;
                // eslint-disable-next-line no-return-assign
                return script.onload = () => {
                    oldOnload();
                    onload();
                };
            },
            scriptExists() {
                return this.getScriptElement() !== null;
            },
            appendScript(onload) {
                if (!this.canUseDOM()) {
                    onload();
                    return;
                }

                if (this.scriptExists()) {
                    if (typeof TradingView === 'undefined') {
                        this.updateOnloadListener(onload);
                        return;
                    }
                    onload();
                    return;
                }
                const script = document.createElement('script');
                script.id = SCRIPT_ID;
                script.type = 'text/javascript';
                script.async = true;
                script.src = 'https://s3.tradingview.com/external-embedding/embed-widget-market-overview.js';
                script.onload = onload;
                script.textContent = JSON.stringify(this.options);

                this.$refs.tradingview.appendChild(script);
            },
        },
    };
  </script>
