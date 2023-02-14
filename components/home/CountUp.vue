<template>
    <ICountUp
        ref="Countup"
        :delay="delay"
        :options="options"
        :end-val="value"
    />
</template>

<script>
    import ICountUp from 'vue-countup-v2';

    export default {
        components: {
            ICountUp,
        },
        props: {
            value: {
                type: Number,
                default: 50,
            },
            delay: {
                type: Number,
                default: 0,
            },
        },
        data() {
            return {
                pageYOffset: 0,
                countUpOffset: 0,
                options: {
                    useEasing: true,
                    useGrouping: true,
                    separator: ',',
                    decimal: '.',
                },
            };
        },

        watch: {
            pageYOffset() {
                if (+this.pageYOffset > 2700) {
                    this.$refs.Countup.create();
                } else {
                    this.$refs.Countup.destroy();
                }
            },
        },

        destroyed() {
            window.removeEventListener('scroll', this.handleScroll);
        },

        mounted() {
            window.addEventListener('scroll', this.handleScroll);
            this.$refs.Countup.destroy();
            this.countUpOffset = this.$refs.Countup.$el.offsetTop;
            // console.log(this.$refs.Countup.$el.offsetTop);
        },

        methods: {
            handleScroll() {
                const { pageYOffset } = window;
                this.pageYOffset = pageYOffset;
            },
        },
    };
</script>
