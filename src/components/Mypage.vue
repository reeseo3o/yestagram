<template>
  <div style="padding: 10px">
    <h4>팔로워</h4>
    <input placeholder="🔍" />
    <div class="post-header" v-for="(a, i) in follower" :key="i">
      <div class="profile" :style="`background-image:url(${a.image})`"></div>
      <span class="profile-name">{{ a.name }}</span>
    </div>
  </div>
</template>

<script>
import { computed, onMounted, ref, toRefs, watch } from "vue";
import axios from "axios";
import { useStore } from "vuex";
export default {
  name: "mypage",
  props: {
    one: Number,
  },

  setup(props) {
    let follower = ref([]);

    let { one } = toRefs(props);
    console.log(one.value);

    let re = computed(() => {
      return follower.value.length;
    });
    console.log(re.value);

    let store = useStore();
    console.log(store.state.name);
    console.log(store.commit());

    onMounted(() => {
      axios.get("/follower.json").then((a) => {
        follower.value = a.data;
      });
    });

    return { follower };
  },
  data() {},
};
</script>

<style></style>
