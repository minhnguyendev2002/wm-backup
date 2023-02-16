<template>
    <div class="2xl:max-w-[1500px] mx-auto bg-white lg:py-1 px-3 md:px-6 flex justify-between items-center">
        <div class="flex items-center w-full">
            <nuxt-link to="/" class="max-w-[300px] block">
                <img class="w-full h-full object-cover" src="/images/logo.jpg" alt="logo">
            </nuxt-link>
            <div>
                <a-menu
                    v-if="!isTablet"
                    key="sideBar"
                    :open-keys="openKeys"
                    :default-selected-keys="activeKeys"
                    class="!hidden xl:!block"
                    mode="horizontal"
                    @click="handleClick"
                    @openChange="handleOpenChange"
                >
                    <template v-for="menuItem in menuItems">
                        <a-menu-item v-if="!menuItem.childrens.length" :key="menuItem.key">
                            <i :class="`${menuItem.classIcon}`" />
                            <span class="ml-3 text-lg py-10 font-medium"> {{ menuItem.label }} </span>
                        </a-menu-item>
                        <a-sub-menu v-if="menuItem.childrens.length > 0" :key="menuItem.key">
                            <template #title>
                                <i :class="`${menuItem.classIcon}`" />
                                <span class="ml-3 text-lg py-10 font-medium"> {{ menuItem.label }} </span>
                            </template>
                            <a-menu-item v-for="child in menuItem.childrens" :key="child.key">
                                <i :class="`${child.classIcon}`" />
                                <span class="ml-3 text-lg py-10 font-medium"> {{ child.label }} </span>
                            </a-menu-item>
                        </a-sub-menu>
                    </template>
                </a-menu>
            </div>
            <div class="ml-auto flex gap-3">
                <div class="gap-3 hidden sm:flex">
                    <a href="https://www.rosyvncrm.com/pc/user/login">
                        <a-button type="primary" class="!bg-prim-100">
                            Đăng nhập
                        </a-button>
                    </a>
                    <a href="https://www.rosyvncrm.com/pc/user/regist">
                        <a-button type="primary" class="!bg-prim-100">
                            Đăng ký ngay
                        </a-button>
                    </a>
                </div>
                <a-button
                    class="!block xl:!hidden !bg-prim-100"
                    type="primary"
                    @click="openSideBar"
                >
                    <i class="fas fa-bars" />
                </a-button>
            </div>
        </div>
        <a-drawer
            :visible="sidebarVisible"
            placement="left"
            width="280"
            @close="closeSideBar"
        >
            <div class="max-w-[250px] mx-auto my-7">
                <img class="w-full h-full object-cover" src="/images/logo.jpg" alt="logo">
            </div>
            <a-menu
                key="draw"
                :open-keys="openKeys"
                :default-selected-keys="activeKeys"
                class=""
                mode="inline"
                @click="handleClick"
                @openChange="handleOpenChange"
            >
                <template v-for="menuItem in menuItems">
                    <a-menu-item v-if="!menuItem.childrens.length" :key="menuItem.key">
                        <i :class="`${menuItem.classIcon}`" />
                        <span class="text-lg py-10 font-medium"> {{ menuItem.label }} </span>
                    </a-menu-item>
                    <a-sub-menu v-if="menuItem.childrens.length > 0" :key="menuItem.key">
                        <template #title>
                            <i :class="`${menuItem.classIcon}`" />
                            <span class="text-lg py-10 font-medium"> {{ menuItem.label }} </span>
                        </template>
                        <a-menu-item v-for="child in menuItem.childrens" :key="child.key">
                            <i :class="`${child.classIcon}`" />
                            <span class="text-lg py-10 font-medium"> {{ child.label }} </span>
                        </a-menu-item>
                    </a-sub-menu>
                </template>
            </a-menu>
            <div class="gap-3 sm:hidden flex justify-between mt-10">
                <a class="block w-full text-center" href="https://www.rosyvncrm.com/pc/user/login">
                    <a-button type="primary" class="!bg-prim-100">
                        Đăng nhập
                    </a-button>
                </a>
                <a class="block w-full text-center" href="https://www.rosyvncrm.com/pc/user/regist">
                    <a-button type="primary" class="!bg-prim-100">
                        Đăng ký ngay
                    </a-button>
                </a>
            </div>
        </a-drawer>
    </div>
</template>

<script>
    export default {
        components: {
        },

        data() {
            return {
                sidebarVisible: false,
                activeKeys: [],
                openKeys: [],
                isTablet: false,
            };
        },

        computed: {
            menuItems() {
                return [{
                    label: 'Trang chủ',
                    key: '/',
                    classIcon: 'isax isax-graph',
                    childrens: [
                    ],
                }, {
                    label: 'Công cụ thị trường',
                    key: '/tools/real-time-chart',
                    classIcon: 'isax isax-user',
                    childrens: [
                        {
                            label: 'Biểu đồ thị trường thời gian thực',
                            key: '/tools/real-time-chart',
                        },
                        {
                            label: 'Forex Map',
                            key: '/tools/forex-heat-map',
                        },
                    ],
                }, {
                    label: 'Giới thiệu về nền tảng',
                    key: '/about-us',
                    classIcon: 'isax isax-shopping-cart',
                    childrens: [
                        {
                            label: 'Về chúng tôi',
                            key: '/about-us',
                        },
                    ],
                }];
            },
        },

        watch: {
            '$route.path': {
                async handler() {
                    this.activeKeys = [];
                    this.sidebarVisible = false;
                },
                deep: true,
            },
        },

        async mounted() {
            this.isTablet = window.innerWidth < 1280;
        },

        methods: {
            handleClick({ key }) {
                this.$router.push(key);
            },

            openSideBar() {
                this.sidebarVisible = true;
            },

            closeSideBar() {
                this.sidebarVisible = false;
            },

            handleOpenChange(keys) {
                this.openKeys = keys?.length ? [keys?.pop()] : [];
            },
        },
    };
</script>

<style lang="scss">
    .header-sidebar-drawer {
        .ant-drawer-body {
            @apply p-0 h-full #{!important};
        }
    }
    .ant-menu-horizontal {
        @apply border-b-0 #{!important};

    }
    .ant-menu-inline {
        @apply border-r-0 #{!important};
    }
    .ant-menu-horizontal > .ant-menu-item,
    .ant-menu-horizontal > .ant-menu-submenu {
        @apply hover:border-prim-100 #{!important};
    }
</style>
