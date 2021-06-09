<template>
  <div :class="modalContainerClasses">
    <div class="background" @click="onClose"></div>
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
  display: block;
  position: fixed;
  width: 100vw;
  height: 100vh;
  top: 0;
  right: 0;
  visibility: hidden;
  transition: visibility 0s 0.3s;
}

.modal-container .background {
  background: rgba(0, 0, 0, 0.3);
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 0;
  opacity: 0;
  transition: opacity ease 0.3s;
}

.modal-container .modal {
  width: 50vw;
  height: 100%;
  position: absolute;
  top: 0;
  right: 0;
  z-index: 1;
  transform: translateX(100%);
  transition: transform ease-out 0.3s;
}

/** MODAL ACTIVE **/
.modal-container.modal-container--active {
  visibility: visible;
  transition: visibility 0s 0s;
}

.modal-container.modal-container--active .background {
  opacity: 1;
}
.modal-container.modal-container--active .modal {
  transform: translateX(0);
}
</style>
