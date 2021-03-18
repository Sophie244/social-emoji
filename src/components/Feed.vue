<template>
    <v-container>
        <v-toolbar class="v-toolbar"
                   dark
        >
            <v-toolbar-title class="v-toolbar-title">
                Username Feed
            </v-toolbar-title>
            <v-spacer></v-spacer>
            <v-badge
                    color="pink"
                    content="6">
                <v-icon>
                    {{mdiBellOutline}}
                </v-icon>
            </v-badge>
        </v-toolbar>

        <v-card class="feed" elevation="10">
            <v-card-title>
                Username
            </v-card-title>
            <v-card-subtitle class="v-card-subtitle">
                Date | #Post
            </v-card-subtitle>
            <v-card-text class="v-card-text">
                Small plates, salads & sandwiches -
                an intimate setting with 12 indoor seats plus patio seating.
            </v-card-text>
            <v-divider class="v-divider"></v-divider>
            <v-card class="v-card-reactions"
                    elevation="0"
                    v-if="reactions.length > 0 && reactions.length <= 10"
            >
                {{reactions}}
            </v-card>
            <v-card class="v-card-reactions"
                    elevation="0"
                    v-else-if="reactions.length > 0 && reactions.length > 10"
            >
                {{omitEmoji()}}
            </v-card>
            <v-divider class="v-divider"></v-divider>
            <v-card-actions class="v-card-actions">
                <v-spacer></v-spacer>
                <v-icon type="button"
                        @click="showEmojiDialog">{{mdiEmoticonHappyOutline}}
                </v-icon>
                <VEmojiPicker
                        v-show="emojiDialog"
                        :pack="emojisNative"
                        labelSearch="Search"
                        @select="selectEmoji"/>
                <span class="span"></span>
                <div class="comment-invoker">
                    <v-icon type="button">{{mdiCommentTextMultipleOutline}}</v-icon>
                </div>
            </v-card-actions>
        </v-card>
    </v-container>
</template>

<script>
    import {mdiEmoticonHappyOutline, mdiBellOutline} from '@mdi/js';
    import {mdiCommentTextMultipleOutline} from '@mdi/js';
    import {VEmojiPicker} from 'v-emoji-picker';
    import packEmoji from 'vue-emoji-picker/src/emojis';

    export default {
        name: "Feed",

        components: {
            VEmojiPicker
        },

        data: () => ({
            mdiEmoticonHappyOutline,
            mdiCommentTextMultipleOutline,
            mdiBellOutline,
            input: '',
            emojiDialog: false,
            reactions: [],
            omitReactions: [],

        }),
        mounted() {
        },
        methods: {
            showEmojiDialog() {
                this.emojiDialog = !this.emojiDialog;
            },

            selectEmoji(emoji) {
                this.input = emoji;
                this.reactions += emoji.data;
            },

            omitEmoji() {
                this.omitReactions = this.reactions.slice(0, 10)
                return this.omitReactions
            }
        },
        computed: {
            emojisNative() {
                return packEmoji;
            }
        }
    };
</script>

<style scoped lang="scss">

    .v-toolbar {
        margin-bottom: 35px;
        text-align: center;
    }

    .v-toolbar-title {
        text-align: center;
    }

    .v-card-subtitle {
        text-align: left;
    }

    .v-card-text {
        text-align: left;
    }

    .v-divider {
        width: 80%;
        margin-right: auto;
        margin-left: auto;
    }

    .v-card-reactions {
        max-width: 80%;
        overflow: hidden;
    }

    .span {
        width: 35px;
    }

    .v-card-actions {
        padding-right: 50px;
    }

</style>
