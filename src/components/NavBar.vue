<template>
    <nav class="navbar">
        <div class="wrapper">
            <form class="searchbar">
                <label>
                    <span class="screen-reader-only">Search:</span>
                    <input v-model="tag" type="text" placeholder="Search for photos..." class="searchbar-input">
                </label>
                <button type="submit" class="btn btn-go" @click.prevent="search">Go</button>
            </form>
        </div>
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
