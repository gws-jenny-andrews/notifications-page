<script setup>
import { toRefs } from 'vue'
//const {post} = defineProps(['post'])
const { post } = defineProps({
  post: Object
})
</script>

<template>

  <div class="notification" :class="{ 'unread': !post.read }">
    <div class="avatar">
      <img :src="`/images/${post.avatar}`" />
    </div>
    <div class="details">
      <div class="details_inner">
        <div class="details_main">
          <div>
            <p>
              <span class="username">{{ post.name }}</span> {{ post.post }}
              <a v-if="post.link !== null">{{ post.link }}</a>
              <span v-if="!post.read" class="dot space"></span>
            </p>

          </div>
          <div class="date">{{ post.time }}</div>
        </div>
        <div class="details_picture" v-if="post.picture != '' && post.picture != null">
          <img :src="`/images/${post.picture}`" />
        </div>
      </div>

      <div class="message" v-if="post.message">
        <p>{{ post.message }}</p>
      </div>
    </div>

  </div>
</template>

<style scoped lang="scss">
.notification {
  display: flex;
  flex-direction: row;
  padding: 12px 10px;
  background-color: var(--neutral-100);
  border-radius: 10px;
  gap: 15px;

  &.unread {
    background-color: var(--neutral-200);
  }

  .avatar {
    width: 50px;
    display: flex;
    justify-content: flex-start;
    align-items: flex-start;

    img {
      width: 40px;
      height: 40px;
      border-radius: 100%;
    }
  }

  .details {
    display: flex;
    flex-direction: column;
    flex-grow: 1;
    gap: 0px;
    font-size: 0.9rem;

    .details_inner {
      display: flex;
      flex-direction: row;
      gap: 10px;
      line-height: 1.2rem;

      .details_picture {
        display: flex;
        flex-grow: 1;
        justify-content: flex-end;

        img {
          width: 50px;
          height: 50px;
          object-fit: cover;
          border-radius: 6px;
        }
      }

      .details_main {
        display: flex;
        flex-direction: column;
        gap: 3px;



        span.username {
          font-weight: 800;
          color: var(--neutral-700);
          cursor:pointer;

          &:hover {
            color: var(--primary-blue);
          }
        }

        span.dot {
          display: inline-flex;
          width: 8px;
          height: 8px;
          background-color: var(--primary-red);
          border-radius: 100%;

          &.space {
            margin-left: 5px;
          }
        }

      }
    }



    a {
      text-decoration: none;
      color: #777;
      font-weight: 800;
      cursor: pointer;

      &:hover {
        color: var(--primary-blue);
      }
    }

    .date {
      color: var(--neutral-500);
    }
  }

  .message {
    border: 1px solid var(--neutral-400);
    padding: 15px 10px;
    margin-top: 10px;
    line-height: 120%;
    border-radius: 6px;
    margin-bottom: 10px;
    

    &:hover {
      background-color: var(--neutral-300);
    }
  }

}


@media (min-width: 730px) {
  .notification {
    .details {
      font-size: 1rem;
    }

    .message {
      /* I think using this looks wrong. So what 
      I dont care. I'm doing it my way ! */
      //max-width: 98%;
      
      padding: 15px 25px;
    }
  }
}
</style>
