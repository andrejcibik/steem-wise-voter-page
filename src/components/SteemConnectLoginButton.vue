<!-- src/components/SteemConnectLoginButton.vue -->
<template>
        <div class="steemconnect-container">
            <span class="steemconnect-error-msg">{{ errorMessage }}</span>
            <span v-if="isLoggedIn">
                <b-button class="steemconnect-logout-button" size="sm" variant="link"
                     @click="logout" title="Logout from SteemConnect">
                    Logout from SteemConnect
                </b-button>
            </span>
            <span v-else>
                <a :href="loginUrl">
                    Login with SteemConnect
                </a>
            </span>
        </div>
</template>

<script lang="ts">
import Vue from "vue";
import { SteemConnectApiHelper } from "../api/SteemConnectApiHelper";

export default Vue.extend({
    props: [],
    data() {
        return {
        };
    },
    methods: {
        logout() {
            this.$store.dispatch("logoutFromSteemConnect");
        },
    },
    computed: {
        isLoggedIn(): boolean {
            return this.$store.state.steemConnectData.loggedIn;
        },
        loginUrl(): string {
            return SteemConnectApiHelper.getLoginUrl();
        },
        errorMessage(): string {
            return this.$store.state.steemConnectData.error;
        },
        username(): string {
            return this.$store.state.steemConnectData.account ?
                this.$store.state.steemConnectData.account.name : "(loading account...)";
        },
    },
});
</script>

<style>
.steemconnect-container {
    color: #999;
}

.steemconnect-error-msg {
    color: red;
}
</style>
