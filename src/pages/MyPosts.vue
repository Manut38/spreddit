<template>
  <q-page class="constrain q-pa-md">
    <tag-creator-bar
      allow-subscribe
      :tags="tags"
      placeholder="Filter Tags"
      icon="eva-funnel-outline"
      class="q-pb-md">
    </tag-creator-bar>
    <PostList
      ref="postList"
      :tags="tags"
      :user-filter="currentUserRef"
      @tag-clicked="tags = [$event]"/>
  </q-page>
</template>

<script>
import TagCreatorBar from "components/forum/TagCreatorBar";
import PostList from "components/forum/posts/PostList";
import {mapGetters} from "vuex";

export default {
  name: 'MyPosts',
  components: {PostList, TagCreatorBar},

  data() {
    return {
      tags: [],
    }
  },
  computed: {
    ...mapGetters('user', ['currentUserRef']),
  },
  beforeRouteLeave(to, from, next) {
    this.$refs.postList.clearQuery()
    next();
  },
  created() {
    this.$changeBackgroundColor('my-posts')
  }
}
</script>
