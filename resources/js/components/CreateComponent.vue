<template>
  <div>
    <h1>Create A Post</h1>
    <form @submit.prevent="addPost">
      <div class="row">
        <div class="col-md-6">
          <div class="form-group">
            <label for="">Post Title:</label>
            <input type="text" class="form-control" v-model="post.title">
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-md-6">
          <div class="form-group">
            <label for="">Post Body:</label>
            <textarea class="form-control" v-model="post.body" rows="5"></textarea>
          </div>
        </div>
      </div><br />
      <div class="form-group">
        <button class="btn btn-primary">Create</button>
      </div>
    </form>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        post: {}
      }
    },
    methods: {
      addPost() {
        let uri = 'http://localhost:82/api/post/create';
        this.axios.post(uri, this.post).then(response => {
          this.$router.push({name: 'posts'});
        });
      }
    },
  }
</script>

<style scoped>

</style>