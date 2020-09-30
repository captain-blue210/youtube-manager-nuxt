<template>
    <section class="section">
        <div class="container">
            <div class="block" v-for="item in items" :key="item.id">
                <div class="block">
                    <AppVideo
                        :item="item"
                        :video-id="item.id"
                    />
                </div>
            </div>
            <div class="field">
                <label class="label">Comment</label>
                <div class="control">
                    <input v-model="comment" class="input" type="text" placeholder="Text input">
                </div>
            </div>
            <div class="field is-grouped">
                <div class="control">
                    <button
                        class="button is-link"
                        @click="comment"
                    >コメント</button>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
import ROUTES from '~/routes/api'
import AppVideo from '~/components/AppVideo';

export default {
    data() {
        return {
            comment: "",
        }
    },
    components: {
        AppVideo
    },
    computed: {
        items() {
            return this.$store.getters.getFavoriteVideos
        }
    },
    methods: {
        comment() {
            this.$store.dispatch("comment", this.comment)
        }
    },
    async fetch({store}) {
        const payload = {
            uri: ROUTES.GET.FAVORITE,
        }
        await store.dispatch('fetchFavoriteVideos', payload)
    }
}
</script>
