<template>
    <div>
        <div class="parallax parallax-home">
            <div class="container">
                <div data-aos="fade-up" data-aos-duration="1000" class="top-landing-details">
                    <h2>Videos</h2>
                </div>
            </div>
        </div>
        <div class="container">
            <div class="videos">
                <div class="p-grid">
                    <div v-for="video in videos" class="p-col-12 p-md-6 p-lg-4">
                        <div class="frame-area embed-responsive embed-responsive-16by9">
                            <iframe width="560" height="315" :src="video.link"
                                    title="YouTube video player" frameborder="0"
                                    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                                    allowfullscreen></iframe>

                        </div>
                        <div style="color: black;">
                            <h4><strong>{{ video.title }}</strong></h4>
                            <p>{{ video.abt }}</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </div>
</template>

<script>
import {mapGetters} from 'vuex'

export default {
    name: "Videos Component",
    methods: {
        track () {
            this.$gtag.pageview(this.$route)
        },
    },
    computed: {
        ...mapGetters([
            'videos'
        ])
    },
    created() {
        if (this.videos.length < 1) {
            this.$store.dispatch('fetchVideos')
        }
    },
    mounted() {
        if (this.videos.length < 1) {
            this.$store.dispatch('fetchVideos')
        }
    }
}
</script>

<style scoped lang="sass">
.background-video
    width: 100vw
    height: 100%
    object-fit: cover
    left: 0
    right: 0
    top: 0
    z-index: -1
.parallax-home
    background-image: url('https://d1bqrv1jyf8x1f.cloudfront.net/images/shk_general/Greenpark_SHK_Drone_3.jpg')
    height: 90vh

.frame-area
    object-fit: cover !important
    position: relative

    iframe
        position: absolute
        overflow: auto
</style>
