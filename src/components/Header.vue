<template>
    <div :class="$style.index">
        <div :class="$style.container">
            <div :class="$style.linkSection">
                <div :class="[$style.box, $style.leftBox]">
                    <router-link :to="`/`">
                        <div :class="$style.link">
                            <i class="el-icon-s-home" />
                        </div>
                    </router-link>
                </div>

                <div :class="[$style.box, $style.rightBox]">
                    <span v-on:click="logout()" v-if="isLoggeIn()" :to="`/`">
                        <div :class="$style.link">Logout</div>
                    </span>
                    <div :class="$style.cover" v-else>
                        <router-link :to="`/member/login`">
                            <div :class="$style.link">Login</div>
                        </router-link>

                        <router-link :to="`/member/join`">
                            <div :class="$style.link">Join</div>
                        </router-link>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component({
    components: {},
})
export default class Header extends Vue {
    isLoggeIn() {
        return this.$store.state.token !== undefined;
    }
    logout() {
        this.$store.commit("setToken", undefined);
        this.$store.commit("setUser", undefined);
    }
}
</script>

<style lang="scss" module>
@import "@/assets/utils.scss";

.index {
    border-bottom: 1px solid #dbdbdb;

    .container {
        max-width: 1080px;
        height: 80px;

        padding: 12px;

        @include setCenter;

        .title {
            display: inline-block;
        }

        .linkSection {
            display: flex;

            a {
                text-decoration: none;

                color: black;
            }

            .box {
                width: 50%;

                display: flex;
            }

            .box.rightBox {
                justify-content: end;

                > span {
                    cursor: pointer;
                }
            }

            .cover {
                display: flex;
            }

            .link {
                padding: 16px 12px;

                font-size: 16px;

                > i {
                    width: 100%;
                    height: 100%;
                }
            }
        }
    }
}
</style>
