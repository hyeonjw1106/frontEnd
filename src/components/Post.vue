<template>
  <div class="post">
    <div class="post-header">
      <img :src="post.userImage" class="profile" />
      <span class="profile-name">{{ post.name }}</span>
    </div>

    <div class="post-body">
      <img :src="post.postImage" class="post-img" />
    </div>

    <div class="post-content">
      <p>{{ post.likes }} Likes</p>
      <p>
        <strong>{{ post.name }}</strong> {{ post.content }}
      </p>
      <p class="date">{{ post.date }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Post',
  props: {
    post: Object
  }
}
</script>
