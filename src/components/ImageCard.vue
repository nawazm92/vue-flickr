<template>
  <li class="image-card">
    <img
      class="image-card__image"
      :class="{skeleton: loading}"
      :src="img_url"
      :alt="title">
    <div class="image-card__body">
      <p class="image-title" :class="{skeleton: loading}">{{ title }}</p>
      <p class="image-owner" :class="{skeleton: loading}">By {{ owner_name }}</p>
      <section class="image-extra-info">
        <p class="image-date" :class="{skeleton: loading}">{{ date_taken }}</p>
        <p class="image-views" :class="{skeleton: loading}">Views: {{ views }}</p>
      </section>
    </div>
  </li>
</template>

<script>
import moment from 'moment';

const TRANSPARENT_GIF = 'data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7';

export default {
  name: 'ImageCard',
  props: {
    img: {
      type: Object,
      default() {
        return {}
      }
    },
    loading: {
      type: Boolean,
      default: false,
    }
  },
  computed: {
    img_url() {
      if (this.loading) return TRANSPARENT_GIF

      return this.img.url_n
    },
    title() {
      return this.img.title || 'Untitled'
    },
    owner_name() {
      return `By ${this.img.ownername}`
    },
    date_taken() {
      return moment(this.img.datetaken).format('MMMM Do, YYYYY')
    },
    views() {
      const v = (this.img.views === 1) ? 'view' : 'views'
      return `${this.img.views} ${v}`
    }
  }
};
</script>

<style lang="scss">
.image-card {
  width: calc(33% - 1rem);
  margin: 0.5rem;
  border-radius: 5px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, .15);
  background: white;
  @media only screen and (max-width: 799px) {
    width: calc(50% - 1rem);
  }
  @media only screen and (max-width: 549px) {
    width: 100%;
    margin: 0.5rem 0;
  }
}
.image-card__image {
  border-radius: 5px 5px 0 0;
  width: 100%;
  height: 200px;
  object-fit: cover;
}
.image-card__body {
  padding: 0.5rem 1rem 1rem;
}
.image-title {
  font-weight: bold;
  margin: 0;
}
.image-owner {
  margin-top: 0;
  font-size: 0.8rem;
}
.image-title,
.image-owner {
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow: hidden;
  text-align: left;
}
.image-extra-info {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.image-date,
.image-views {
  margin-bottom: 0;
  font-size: 0.8rem;
}

@keyframes skeleton-glow {
  from {
    border-color: rgba(206, 217, 224, 0.2);
    background: rgba(206, 217, 224, 0.2)
  }
  to {
    border-color: rgba(92, 112, 128, 0.2);
    background: rgba(92, 112, 128, 0.2);
  }
}

.skeleton {
  animation: skeleton-glow 1s liner infinite alternate;
  background-clip: border-box;
  background-clip: padding-box !important;
  background: rgba(206, 217, 224, 0.2) !important;
  background-color: rgba(206, 217, 224, 0.2) !important;
  border-radius: 2px;
  box-shadow: none !important;
  color: transparent !important;
  cursor: default;
  pointer-events: none;
  user-select: none;
}
</style>
