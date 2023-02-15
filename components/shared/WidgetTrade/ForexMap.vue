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
                    width: '100%',
                    height: '100%',
                    currencies: [
                        'EUR',
                        'USD',
                        'JPY',
                        'GBP',
                        'CHF',
                        'AUD',
                        'CAD',
                        'NZD',
                    ],
                    isTransparent: false,
                    colorTheme: 'light',
                    locale: 'en',
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
                script.src = 'https://s3.tradingview.com/external-embedding/embed-widget-forex-cross-rates.js';
                script.onload = onload;
                script.textContent = JSON.stringify(this.options);

                this.$refs.tradingview.appendChild(script);
            },
        },
    };
  </script>
