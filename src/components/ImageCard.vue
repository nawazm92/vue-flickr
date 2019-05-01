<template>
  <li class="image-card">
    <img class="image-card__image" :src="img.url_n" :alt="img.title">
    <div class="image-card__body">
      <p v-if="img.title" class="image-title">{{img.title}}</p>
      <p v-else class="image-title">Untitled</p>
      <p class="image-owner">By {{img.ownername}}</p>
      <section class="image-extra-info">
        <p class="image-date">{{img.datetaken | moment}}</p>
        <p class="image-views">Views: {{img.views}}</p>
      </section>
    </div>
  </li>
</template>

<script>
import moment from 'moment';

export default {
  name: 'ImageCard',
  props: ['img'],
  filters: {
    moment(date) {
      return moment(date).format('MMMM Do, YYYY');
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
</style>
