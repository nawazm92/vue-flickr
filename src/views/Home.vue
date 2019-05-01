<template>
    <div class="home">
      <nav class="navbar">
        <form>
            <label>
                <span class="screen-reader-only">Search:</span>
                <input v-model="tag" type="text" placeholder="Search photos" class="searchbar-input">
            </label>
            <button type="submit" class="btn btn-go" @click.prevent="search">Go</button>
        </form>
      </nav>
      <div class="wrapper">
        <p v-if="loading" class="text-centered loading">Loading<span>.</span><span>.</span><span>.</span></p>
        <ul v-else class="image-card-grid">
          <image-card v-for="img in cleanImgs" :key="img.id" :img="img" />
        </ul>
      </div>
    </div>
</template>
<script>
import config from '../../public/config';
import axios from 'axios';
import ImageCard from '@/components/ImageCard';

export default {
    name: 'home',
    components: {
      ImageCard
    },
    computed: {
      cleanImgs() {
        return this.images.filter(img => img.url_n)
      }
    },
    data() {
        return {
            loading: false,
            tag: '',
            images: []
        }
    },
    methods: {
        search() {
            this.loading = true;

            this.fetchImages()
                .then((response) => {
                    this.images = response.data.photos.photo;
                    this.loading = false;
                })
            // console.log('Searching for: ', this.tag)
        },

        fetchImages() {
            return axios({
                method: 'get',
                url: 'https://api.flickr.com/services/rest',
                params: {
                    method: 'flickr.photos.search',
                    api_key: config.api_key,
                    tags: this.tag,
                    extras: 'url_n, owner_name, date_taken, views',
                    page: 1,
                    format: 'json',
                    nojsoncallback: 1,
                    per_page: 30,
                }
            })
        },
    }
};
</script>

<style lang="scss">
  .screen-reader-only {
    height: 1px;
    width: 1px;
    position: absolute;
    left: -9999px;
  }
  .text-centered {
    text-align: center;
  }
  .wrapper {
    margin: 0 auto;
    max-width: 800px;
    @media only screen and (max-width: 799px) {
      max-width: 100%;
      margin: 0 1.15rem;
    }
  }
  .image-card-grid {
    list-style: none;
    margin: 0.5rem 0;
    padding: 0;
    display: flex;
    align-items: flex-start;
    flex-wrap: wrap;
  }
  .navbar {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 1rem;
    background: #EFEFEF;
  }
  .searchbar {
    width: 300px;
    display: flex;
    align-items: center;
    justify-content: center;
    @media only screen and (max-width: 549px) {
      width: 100%;
      label {
        width: 80%
      }
    }
  }
  .searchbar-input {
    padding: .5rem 1rem;
    border-radius: 20px;
    font-size: 1rem;
    border: 1px solid gray;
    min-width: 300px;
    @media only screen and (max-width: 549px) {
      min-width: 0;
      widows: 100%;
    }
  }
  .btn {
    padding: 0.5rem 1rem;
    font-size: 1rem;
    border-radius: 20px;
    background: transparent;
    border: none;
  }
  .btn-go {
    padding: 0.5rem 2rem;
    margin-left: 1rem;
    border: 1px solid #999;
    background: #666;
    color: #EFEFEF
  }
  .loading {
    font-size: 2rem;
  }
  .loading span {
    font-size: 50px;
    animation-name: blink;
    animation-duration: 1.4s;
    animation-iteration-count: infinite;
    animation-fill-mode: both;
  }

  .loading span:nth-child(2) {
    animation-delay: .2s;
  }

  .loading span:nth-child(3) {
    animation-delay: .4s;
  }

  @keyframes blink {
    0% {
      opacity: .2;
    }
    20% {
      opacity: 1;
    }
    100% {
      opacity: .2;
    }
  }
</style>
