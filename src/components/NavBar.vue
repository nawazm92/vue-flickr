<template>
    <nav class="navbar">
        <form class="searchbar">
            <label>
                <span class="screen-reader-only">Search:</span>
                <input v-model="tag" type="text" placeholder="Search photos" class="searchbar-input">
            </label>
            <button type="submit" class="btn btn-go" @click.prevent="search">Go</button>
        </form>
      </nav>
</template>

<script>
export default {
    name: 'NavBar',
    data() {
        return {
            tag: ''
        }
    },
    methods: {
        search() {
            this.$router.push({name: 'searchResults', params: {tag: this.tag}})
            this.tag = '';
        }
    }
}
</script>
