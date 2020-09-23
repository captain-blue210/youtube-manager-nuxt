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
    async fetch({store}) {
        const payload = {
            uri: ROUTES.GET.FAVORITE,
        }
        await store.dispatch('fetchFavoriteVideos', payload)
    }
}
</script>
