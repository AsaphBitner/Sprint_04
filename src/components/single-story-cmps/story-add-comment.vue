<template>
  <section class="story-add-comment">
    <form @submit="addComment(story._id, $event)" method="POST">
      <button type="button" class="comment-imoji-icon">
        <div class="">
          <svg
            aria-label="Emoji"
            class="_8-yf5"
            fill="#262626"
            height="24"
            role="img"
            viewBox="0 0 48 48"
            width="24"
          >
            <path
              d="M24 48C10.8 48 0 37.2 0 24S10.8 0 24 0s24 10.8 24 24-10.8 24-24 24zm0-45C12.4 3 3 12.4 3 24s9.4 21 21 21 21-9.4 21-21S35.6 3 24 3z"
            ></path>
            <path
              d="M34.9 24c0-1.4-1.1-2.5-2.5-2.5s-2.5 1.1-2.5 2.5 1.1 2.5 2.5 2.5 2.5-1.1 2.5-2.5zm-21.8 0c0-1.4 1.1-2.5 2.5-2.5s2.5 1.1 2.5 2.5-1.1 2.5-2.5 2.5-2.5-1.1-2.5-2.5zM24 37.3c-5.2 0-8-3.5-8.2-3.7-.5-.6-.4-1.6.2-2.1.6-.5 1.6-.4 2.1.2.1.1 2.1 2.5 5.8 2.5 3.7 0 5.8-2.5 5.8-2.5.5-.6 1.5-.7 2.1-.2.6.5.7 1.5.2 2.1 0 .2-2.8 3.7-8 3.7z"
            ></path>
          </svg>
        </div>
      </button>
      <div class="" style=""></div>
      <textarea
        v-model="newCommentInput"
        @keydown.enter="addComment(story._id, $event)"
        aria-label="Add a comment…"
        placeholder="Add a comment…"
        class="Ypffh"
        autocomplete="off"
        autocorrect="off"
        style=""
      ></textarea>
      <button class="" type="submit" @click="addComment(story._id, $event)">
        Post
      </button>
    </form>
  </section>
</template>

<script>
export default {
  props: {
    story: Object,
  },

  data() {
    return {
      loggedInUser: {},
      newCommentInput: "",
    };
  },
  methods: {
    async getLoggedInUser() {
      this.loggedInUser = await this.$store.dispatch("getLoggedInUser");
    },
    async addComment(storyId, ev) {
      if (ev.shiftKey) return;
      ev.preventDefault();
      if (!this.newCommentInput) {
        console.log("No text");
        return;
      }
      const payload = {
        storyId: storyId,
        text: this.newCommentInput,
      };
      await this.$store.dispatch("addComment", payload);
      this.newCommentInput = "";
      let tempStory = this.$store.state.stories.find(item => item._id === this.story._id)
      this.story.comments = tempStory.comments
      //   await this.resetnewCommentsInput(storyIdx);
      //   this.loadLimitedStories();
    },
  },
  //   computed:{
  //   },

  async created() {
    await this.getLoggedInUser();
  },
};
</script>

<style>
</style>