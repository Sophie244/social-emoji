<template>
    <v-container>
        <v-card class="login" elevation="10">
            <v-card-title class="v-card-title">
                Welcome to Emojimedia <div class="emoji">{{displayEmoji('heart_eyes')}}</div>
            </v-card-title>
            <v-form v-model="valid">
                <v-container>
                    <v-col
                            cols="12"
                            md="12"
                    >
                        <v-text-field
                                v-model="username"
                                label="Username"
                                required
                        >
                        </v-text-field>
                    </v-col>
                    <v-col
                            cols="12"
                            md="12"
                            v-if="visible"
                    >
                        <v-text-field
                                v-model="firstname"
                                label="Firstname"
                                required
                        >
                        </v-text-field>
                    </v-col>
                    <v-col
                            cols="12"
                            md="12"
                            v-if="visible"
                    >
                        <v-text-field
                                v-model="lastname"
                                label="Lastname"
                                required
                        >
                        </v-text-field>
                    </v-col>
                    <v-col
                            cols="12"
                            md="12"
                    >
                        <v-text-field
                                v-model="password"
                                label="Password"
                                required
                        >
                        </v-text-field>
                    </v-col>
                </v-container>
            </v-form>
            <v-card-actions class="v-card-actions">
                <v-btn elevation="0"
                       v-on:click="login"
                       v-bind="attrs"
                       v-on="on"
                >Login</v-btn>
                <v-btn elevation="0"
                       v-on:click="register"
                       v-bind="attrs"
                       v-on="on"
                >
                    Register
                </v-btn>
            </v-card-actions>
        </v-card>
    </v-container>
</template>

<script>
    export default {
        name: 'Login',

        data: () => ({
            visible: false,
        }),

        methods: {
            register() {
                this.visible = true;
            },

            login() {
                this.visible = false;


            },

            displayEmoji(unicode) {
                const emoji = require("emoji-dictionary");
                return emoji.getUnicode(unicode)
            }
        }
    }
</script>

<style scoped lang="scss">

    .login {
        width: max-content;
        margin-left: auto;
        margin-right: auto;
    }

    .v-card-title {
        letter-spacing: 2px;
    }

    .v-card-actions {
        padding-left: 170px;
        position: relative;
    }
</style>
