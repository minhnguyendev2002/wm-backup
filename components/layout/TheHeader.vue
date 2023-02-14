<template>
    <div class="2xl:max-w-[1500px] mx-auto px-3 bg-white py-4 px-4 md:px-6 flex justify-between items-center">
        <div class="flex items-center w-full">
            <div class="max-w-[300px]">
                <img class="w-full h-full object-cover" src="/images/logo.jpg" alt="logo">
            </div>
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
                    <a-button type="primary" class="!bg-prim-100">
                        Đăng nhập
                    </a-button>
                    <a-button type="primary" class="!bg-prim-100">
                        Đăng ký
                    </a-button>
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
                <a-button type="primary" class="!bg-prim-100 !w-full">
                    Đăng nhập
                </a-button>
                <a-button type="primary" class="!bg-prim-100 !w-full">
                    Đăng ký
                </a-button>
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
                    key: '/cong-cu-thi-truong',
                    classIcon: 'isax isax-user',
                    childrens: [],
                }, {
                    label: 'Giới thiệu về nền tảng',
                    key: '/gioi-thieu',
                    classIcon: 'isax isax-shopping-cart',
                    childrens: [
                        {
                            label: 'Về chúng tôi',
                            key: '/gioi-thieu/ve-chung-toi',
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
