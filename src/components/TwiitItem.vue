<template>
  <div class="twiit-item">
    <div class="user-profile__twiit">
      <div class="twiit-item__user">
        @{{ username }}
      </div>
      <div class="twiit-item__content">
        {{ twiit.content }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TwiitItem",
  props: {
    username: {
      type: String,
      required: true
    },
    twiit: {
      type: Object,
      required: true
    }
  }
};
</script>

<style lang="scss" scoped>
.twiit-item {
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #DFE3E8;
  box-sizing: border-box;
  cursor: pointer;
  transition: all 0.25s ease;

  &:hover {
    transform: scale(1.1, 1.1);
  }

  .twiit-item__user {
    font-weight: bold;
  }
}
</style>