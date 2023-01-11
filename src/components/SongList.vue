<template>
    <div class="pure-g">
        <div class="pure-u-1-1" v-for="(song, i) in songs" :key="i">
            <hr/>
            <ol>
                <li>
                <h5><a :href="base_url + song.youtube_id">{{ song.title }}</a> - {{ song.by }}</h5>
                </li>
            </ol>
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

<style scoped>
    hr {
        margin-top: 50px;
    }
    a {
        color: #49c8f0;
    }
</style>
