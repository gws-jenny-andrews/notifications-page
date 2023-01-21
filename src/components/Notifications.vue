<script setup>
import { ref, reactive, onMounted } from 'vue'
import axios from 'axios'
import Notification from './Notification.vue';
import Header from './Header.vue'

const totalNotifications = ref(0)
const posts = ref([])

onMounted(async () => {
  try {
    const response = await axios.get("data.json")
    const data = response.data
    posts.value = data;
    console.log(data)
    const unreadPosts = data.filter(x => x.read === false)
    totalNotifications.value = unreadPosts ? unreadPosts.length : 0
  }
  catch (ex) {
    console.log("Error fetching data", ex)
  }
})


function handleClick() {
  if (totalNotifications.value > 0) {
    posts.value.map(x=>x.read = true)
  }
  totalNotifications.value = 0
}

</script>

<template>
  <article class="notifications-container">
    <Header :totalNotifications="totalNotifications" @clearUnread="handleClick" />
    <div v-if="posts.length > 0" class="notifications_list" >
      <Notification v-for="post in posts" :post="post" />
    </div>
</article>
</template>

<style scoped lang="scss">

.notifications-container {
  background-color: var(--neutral-100);
  width:100%;
  max-width:730px;
  margin: 0 auto;
}

.notifications_list {
  display: flex;
  flex-direction: column;
  gap: 12px;
}


@media (min-width: 730px) {
  .notifications-container {
    padding:35px;
  }
}
</style>
