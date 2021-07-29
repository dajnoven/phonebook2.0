<template>
  <div class="info__contact">
    <div class="info__header">
      <span>About contact</span>
    </div>
    <div class="info__content">
      <slot></slot>
    </div>
    <div class="info__footer">
      <button
              class="btn-mini"
              @click="closeModal"
      >
        Close
      </button>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Info',
    props: {},
    data() {
      return {}
    },
    methods: {
      closeModal() {
        this.$emit('closeModal')
      }
    }
  }

</script>

<style lang="scss">
.info__contact {
  padding: 16px;

  position: fixed;
  top: 50px;
  width: 600px;
  min-height: auto;

  background: #4a4444;
  box-shadow: 0 0 17px 0 #a5a1a1;
  border-radius: 30px;


  &__heder,
  &__footer {
    display: flex;

  }
  &__content {
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
.info__content {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  font-size: 16px;
  text-align: center;
}
.info__header {
  padding: 24px;

  font-family: "Avenir", Helvetica, Arial, sans-serif;
  font-size: 24px;
  font-weight: bold;
  text-align: center;
}
  .info__footer {
    display: flex;
    flex-direction: row-reverse;
  }

</style>