<script>
export default {
  props: {
    position: Object,
  },
  data() {
    return {
      isJumping: false,
      isMovingLeft: false,
      isMovingRight: false,
    };
  },
  methods: {
    jump() {
      if (!this.isJumping) {
        // Déclencher l'événement de saut
        this.isJumping = true;
        // Réinitialiser le saut après une courte période
        setTimeout(() => {
          this.isJumping = false;
        }, 500); // Ajustez la durée du saut selon vos besoins
      }
    },
    handleTransitionEnd() {
      // Réinitialiser la position verticale à la fin de l'animation de saut
      this.position.y = 300; // Ou toute valeur par défaut que vous souhaitez
    },
  },
  mounted() {
    // Écoutez l'événement de saut
    window.addEventListener("keydown", (e) => {
      switch (e.key) {
        case " ":
          this.jump();
          break;
      }
    });
  },
};
</script>

<template>
  <div
    class="character"
    :style="{ left: position.x + 'px', top: position.y + 'px' }"
    :class="{
      jumping: isJumping
    }"
    @transitionend="handleTransitionEnd"
  >
    🚶
  </div>
</template>

<style scoped>
.character {
  position: absolute;
  font-size: 6rem;
  transition: transform 0.5s ease-in-out; /* Animation de transition pour le saut */
}

.jumping {
  transform: translateY(-80px); /* Ajustez la hauteur du saut */
}
</style>
