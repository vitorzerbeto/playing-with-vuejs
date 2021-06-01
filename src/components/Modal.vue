<template>
  <div :class="modalContainerClasses">
    <div class="background"></div>
    <div class="modal">
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    isActive: {
      type: Boolean,
      required: true,
    },
    onClose: {
      type: Function,
      required: true,
    },
  },
  computed: {
    modalContainerClasses() {
      return {
        'modal-container': true,
        'modal-container--active': this.isActive,
      };
    },
  },
};
</script>

<style>
.modal-container {
  display: none;
  position: fixed;
  width: 100vw;
  height: 100vh;
  top: 0;
  right: 0;
}

.modal-container .background {
  background: rgba(0, 0, 0, 0.3);
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 0;
}

.modal-container .modal {
  width: 50vw;
  height: 100%;
  position: absolute;
  top: 0;
  right: 0;
  z-index: 1;
}

/** MODAL ACTIVE **/
.modal-container.modal-container--active {
  display: block;
}
</style>
