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
                <div class="field">
                    <label class="label">Comment</label>
                    <div class="control">
                        <input :id="item.id" name="comment" class="input" type="text">
                    </div>
                </div>
                <div class="field is-grouped">
                    <div class="control">
                        <button
                            class="button is-link"
                            @click="commentVideo(item.id)"
                        >コメント</button>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
import ROUTES from '~/routes/api'
import AppVideo from '~/components/AppVideo';

export default {
    components: {
        AppVideo
    },
    computed: {
        items() {
            return this.$store.getters.getFavoriteVideos
        }
    },
    methods: {
        commentVideo(videoId) {
            const params = {
                comment: document.getElementById(videoId)
            }
            this.$store.dispatch("commentVideo", {
                uri: ROUTES.POST.COMMENT.replace(':id', videoId),
                payload: params
            })
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
