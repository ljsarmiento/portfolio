<template>
    <nav>
        <v-navigation-drawer
            app
            v-model="$store.state.navigation.sidebar.opened"
            :permanent="$vuetify.breakpoint.mdAndUp"
            floating
            overlay-opacity="0.1"
        >
            <v-app-bar color="primary" class="white--text" flat :dense="$vuetify.breakpoint.smAndDown">
                <v-app-bar-title>
                    {{ $store.getters.appName }}
                </v-app-bar-title>
            </v-app-bar>
            <profile/>
            <template v-slot:append v-if="$vuetify.breakpoint.smAndUp && windowHeight >= 640">
                <side-nav-menu class="mb-5"/>
            </template>
        </v-navigation-drawer>
    </nav>
</template>

<script>
    export default {
        name: 'Sidebar',
        components: {
            'profile'      : () => import('../cards/Profile.vue'),
            'side-nav-menu': () => import('./SideNavMenu.vue')
        },
        data() {
            return {
                // https://stackoverflow.com/questions/54166847/how-to-access-the-window-object-in-vue-js
                windowHeight: window.innerHeight
            }
        },
        computed: {},
        methods : {
            onResize() {
                this.windowHeight = window.innerHeight
            }
        },
        mounted() {
            this.$nextTick(() => {
                window.addEventListener('resize', this.onResize);
            });
        },
        beforeDestroy() {
            window.removeEventListener('resize', this.onResize);
        }
    }
</script>

<style scoped>

</style>
