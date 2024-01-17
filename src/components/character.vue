<script>
export default {
  name: "Character",
  props: {
    position: Object,
    defaultHeight: Number,
    maxLeftPosition: Number,
    maxRightPosition: Number,
    jumpValue: Number,
  },
  data() {
    return {
      isJumping: false,
      moveDistance: 15,
      isMovingLeft: false,
      isMovingRight: false,
      isStandBy: false,
    };
  },
  methods: {
    jump() {
      if (!this.isJumping) {
        // Déclencher l'événement de saut
        this.isStandBy = false;
        this.isJumping = true;
        // Réinitialiser le saut après une courte période
        setTimeout(() => {
          this.isJumping = false;
        }, 500); // Ajustez la durée du saut selon vos besoins
      }
    },
    moveLeft() {
      if (this.position) {
        if (this.position.x > this.maxLeftPosition + this.moveDistance) {
          this.position.x -= this.moveDistance;
        } else {
          this.position.x = this.maxLeftPosition;
        }
      }
      this.isStandBy = false;
      this.isMovingLeft = true;
      this.isMovingRight = false;
    },
    moveRight() {
      if (this.position) {
        if (this.position.x < this.maxRightPosition - this.moveDistance) {
          this.position.x += this.moveDistance;
        } else {
          this.position.x = this.maxRightPosition;
        }
        this.isStandBy = false;
        this.isMovingRight = true;
        this.isMovingLeft = false;
      }
    },
    handleTransitionEnd() {
      // Réinitialiser la position verticale à la fin de l'animation de saut
      this.position.y = this.defaultHeight; // Ou toute valeur par défaut que vous souhaitez
    },
  },
  computed: {
    characterImageSource() {
      // Logique pour déterminer la source de l'image en fonction de l'état du personnage
      if (this.isJumping) {
        return "/Portfolio/img/character/Anim-6.png";
      } else if (this.isMovingLeft) {
        return "/Portfolio/img/character/Walk.gif";
      } else if (this.isMovingRight) {
        return "/Portfolio/img/character/Walk.gif";
      } else if (this.isStandBy) {
        return "/Portfolio/img/character/Anim-0.png";
      } else {
        return "/Portfolio/img/character/Anim-0.png"; // Image par défaut
      }
    },
    characterX() {
      return this.position.x; // Propriété calculée pour la position x
    },
    characterIsJumping() {
      return this.isJumping; // Propriété calculée pour l'état de saut
    },
  },
  watch: {
    characterX(newValue) {
      // Émettre un événement au parent avec la nouvelle valeur de la position x
      this.$emit("update-position-x", newValue);
    },
    characterIsJumping(newValue) {
      // Émettre un événement au parent avec la nouvelle valeur de l'état de saut
      this.$emit("update-is-jumping", newValue);
    },
  },
  created() {
    // Écouter les événements de saut et de déplacement
    window.addEventListener("keydown", (e) => {
      switch (e.key) {
        case " ":
          this.jump();
          break;
        case "ArrowLeft":
        case "a":
          this.moveLeft();
          break;
        case "ArrowRight":
        case "d":
          this.moveRight();
          break;
      }
    });
    window.addEventListener("keyup", (e) => {
      switch (e.key) {
        case "ArrowLeft":
        case "a":
          setTimeout(() => {
            this.isMovingLeft = false;
            this.isStandBy = true;
          }, 200);
          break;
        case "ArrowRight":
        case "d":
          setTimeout(() => {
            this.isMovingRight = false;
            this.isStandBy = true;
          }, 200);
          break;
      }
    });
  },
};
</script>

<template>
  <div
    ref="character"
    class="character"
    :style="{ left: position.x + 'px', top: position.y + 'px' }"
    :class="{
      jumping: isJumping,
    }"
    @transitionend="handleTransitionEnd"
  >
    <img
      :class="{ reversed: isMovingLeft }"
      :src="characterImageSource"
      alt="character"
    />
  </div>
</template>

<style scoped>
.character {
  width: 150px;
  position: relative;
  transition: transform 0.5s ease-in-out; /* Animation de transition pour le saut */
}

.jumping {
  transform: translateY(calc(-1px * v-bind(jumpValue))); /* Ajustez la hauteur du saut */
}

.reversed {
  transform: scaleX(-1);
}
</style>
