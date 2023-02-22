<template>
    <div class="flex justify-between">
        <div class="overflow-x-hidden overflow-y-clip w-full">
            <TheHeader />

            <div class="flex-grow custom-scroll">
                <nuxt ref="nuxt" />
            </div>

            <TheFooter />
        </div>
        <a href="tel:0588888548" class="fixed inline-block sm:hidden text-center bottom-[120px] z-50 w-14 h-14 rounded-full bg-prim-100 !text-white hover:bg-prim-100 transition-all duration-700 right-4 sm:right-8">
            <span class="leading-[56px]">
                <i class="fas fa-phone text-lg" />
            </span>
        </a>
        <div ref="zaloWidget">
            <div
                class="zalo-chat-widget !right-4 sm:!right-8"
                data-oaid="1823779553933075111"
                data-welcome-message="Chào mừng bạn đến với Wealth Managament, inbox ngay để được hỗ trợ"
                data-autopopup="0"
                data-width="350"
                data-height="420"
            />
        </div>
    </div>
</template>

<script>
    import TheHeader from '@/components/layout/TheHeader.vue';
    import TheFooter from '@/components/layout/TheFooter.vue';

    const SCRIPT_ID = 'zalo-widget';

    export default {
        components: {
            TheHeader,
            TheFooter,
        },

        data() {
            return {
                loading: false,
                isScroll: false,
            };
        },

        created() {
            window.addEventListener('scroll', this.handleScroll, true);
        },

        mounted() {
            setTimeout(() => {
                this.appendScript(this.initWidget);
            }, 300);
        },

        beforeDestroy() {
            window.removeEventListener('scroll', this.handleScroll, true);
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
                    if (typeof zaloWidget === 'undefined') {
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
                script.src = 'https://sp.zalo.me/plugins/sdk.js';
                script.onload = onload;
                this.$refs.zaloWidget.appendChild(script);
            },
        },
    };
</script>
