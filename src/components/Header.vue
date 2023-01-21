<script setup>

const {totalNotifications} = defineProps({
  totalNotifications: Number
})

const emits = defineEmits(["clearUnread"])

</script>

<template>
  <div class="header">
    <div class="notifications">
      <h1>Notifications</h1>
      <div class="notifications_badge">{{ totalNotifications }}</div>
    </div>
    <div>
      <button @click="emits('clearUnread')">Mark all as read</button>
    </div>
  </div>
</template>

<style scoped lang="scss">
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-grow: 1;
  margin-bottom: 20px;
  

  .notifications {
    display: flex;
    flex-direction: row;
    align-items: center;
    font-size: 1.0rem;
    gap: 10px;

    h1 {
      font-size: 1.2rem;
      font-weight:800;
      color:var(--neutral-700)
    }

    .notifications_badge {
      display:flex;
      justify-content:center;
      align-items:center;
      background-color: var(--primary-blue);
      color: var(--neutral-100);
      border-radius: 6px;
      padding: 2px 12px;
      font-weight:800;
    }
  }

  button {
      background-color: transparent;
      font-family: "Plus Jakarta Sans", sans-serif;
      font-weight:500;
      font-size:0.94rem;
      color: #555;
      border: none;
      outline: none;
      cursor:pointer;

      &:hover {
        color: var(--primary-blue);
        font-weight:800;
      }
    }
}


@media (min-width: 730px) {
  .header .notifications h1 {
    font-size: 1.3rem
  }
}

</style>
