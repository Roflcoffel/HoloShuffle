<template>
    <div class="pure-g">
        <div class="pure-u-1-1" v-for="(song, i) in songs" :key="i">
            <h5><a :src="base_url + song.youtube_id">{{ song.title }} - {{ song.by }}</a></h5>
            <hr/>
        </div>
    </div>
</template>

<script>
export default {
    name: "SongList_Component",
    data() {
        return {
            base_url: "https://www.youtube.com/watch?v="
        }
    },
    props: {
        songs: Array,
    }
}
</script>