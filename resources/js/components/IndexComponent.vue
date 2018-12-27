<template>
  <div class="">
    <h1>Posts</h1>
    <div class="row">
      <div class="col-md-10"></div>
      <div class="col-md-2">
        <router-link :to="{ name: 'create' }" class="btn btn-primary">Create Post</router-link>
      </div>
    </div><br />

    <table class="table table-hover">
      <thead>
        <tr>
          <th>ID</th>
          <th>Item Name</th>
          <th>Item Price</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="post in posts" :key="post.id">
          <td>{{ post.id }}</td>
          <td>{{ post.title }}</td>
          <td>{{ post.body }}</td>
          <td>
            <router-link :to="{name: 'edit', params: {id: post.id}}" class="btn btn-primary">Edit</router-link>
          </td>
          <td>
            <button class="btn btn-danger" @click.prevent="deletePost(post.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        posts: []
      }
    },
    created() {
      let uri = 'http://localhost:82/api/posts';
      this.axios.get(uri).then(response => {
        this.posts = response.data.data;
      });
    },
    methods: {
      deletePost(id) {
        let uri = `http://localhost:82/api/post/delete/${id}`;
        this.axios.delete(uri).then(response => {
          this.posts.splice(this.getIndex(id), 1);
        });
      },
      getIndex(id) {
        var index = -1;
        this.posts.forEach((post,i) => {
          if(post.id == id)
            index = i;
        });
        return index;
      }
    },
  }
</script>

<style scoped>

</style>