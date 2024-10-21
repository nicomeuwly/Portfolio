<script>
export default {
  name: "SkillElement",
  props: {
    title: String,
    icon: String,
    level: Number,
  },
  data() {
    return {
      numberOfCircles: 5,
      dominantColor: "var(--white)",
      spacingBetweenCircles: 16,
      radius: 7,
      border: 2,
      showSkillLevel: false,
    };
  },
  methods: {
    processImage() {
      // Récupérer l'élément image
      const img = this.$refs.image;

      // Créer un canvas
      const canvas = document.createElement("canvas");
      const ctx = canvas.getContext("2d");

      // Définir la taille du canvas pour correspondre à celle de l'image
      canvas.width = img.width;
      canvas.height = img.height;

      // Dessiner l'image sur le canvas
      ctx.drawImage(img, 0, 0, img.width, img.height);

      // Obtenir les données d'image (tableau de pixels)
      const imageData = ctx.getImageData(0, 0, img.width, img.height);
      const pixels = imageData.data;

      // Compter l'occurrence de chaque couleur, en ignorant les pixels blancs et transparents
      const colorCounts = {};
      for (let i = 0; i < pixels.length; i += 4) {
        // Ignorer les pixels blancs (R, G, B sont égaux à 255)
        if (
          pixels[i] === 255 &&
          pixels[i + 1] === 255 &&
          pixels[i + 2] === 255
        ) {
          continue;
        }

        // Ignorer les pixels transparents (alpha = 0)
        if (pixels[i + 3] === 0) {
          continue;
        }

        // Les valeurs R, G, B sont stockées à chaque position i, i+1, i+2
        const color = `${pixels[i]},${pixels[i + 1]},${pixels[i + 2]}`;

        // Incrémenter le compteur pour cette couleur
        colorCounts[color] = (colorCounts[color] || 0) + 1;
      }

      // Trouver la couleur la plus présente
      let maxCount = 0;
      for (const color in colorCounts) {
        if (colorCounts[color] > maxCount) {
          maxCount = colorCounts[color];
          this.dominantColor = `rgb(${color})`; // Met à jour la couleur dominante
        }
      }
    },
    handleMouseOver() {
      this.showSkillLevel = true;
      this.$refs.image.style.filter = "grayscale(0%)";
    },
    handleMouseLeave() {
      this.showSkillLevel = false;
      this.$refs.image.style.filter = "grayscale(100%)";
    },
  },
  computed: {
    svgWidth() {
      return (
        this.numberOfCircles * this.spacingBetweenCircles +
        this.border * this.radius +
        3
      );
    },
    svgHeight() {
      return 2 * this.radius + 2 * this.border;
    },
    cy() {
      return this.radius + this.border;
    },
  },
};
</script>

<template>
  <div
    class="skill-container"
    @mouseover="handleMouseOver"
    @mouseleave="handleMouseLeave"
  >
    <transition name="fade">
      <div
        class="skill-level"
        :style="{ backgroundColor: dominantColor }"
        v-if="showSkillLevel"
      >
        <svg :width="svgWidth" :height="svgHeight" style="align-self: flex-end">
          <circle
            v-for="circle in numberOfCircles"
            :key="circle"
            :cx="
              (circle - 1) * (spacingBetweenCircles + 2 * border) +
              radius +
              border
            "
            :cy="cy"
            :r="radius"
            stroke="var(--white)"
            :stroke-width="border"
            :fill="circle <= level ? 'var(--white)' : 'none'"
          />
        </svg>
      </div>
    </transition>
    <div class="skill-element">
      <img
        ref="image"
        :src="'/Portfolio/img/logos/' + icon + '.png'"
        :alt="icon + ' logo'"
        @load="processImage"
      />
      <h3 v-if="showSkillLevel">{{ title }}</h3>
    </div>
  </div>
</template>

<style scoped>
.skill-container {
  position: relative;
  width: 100px;
  height: 188px;
}
.skill-element {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 150px;
  background-color: var(--white);
  border-radius: 10px;
  padding: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
}
.skill-level {
  width: 100%;
  height: 100%;
  padding: 10px;
  border-radius: 10px;
  display: flex;
  justify-content: center;
}
img {
  width: 90%;
  object-fit: contain;
  filter: grayscale(100%);
  transition: filter 0.3s ease-in-out;
}
h3 {
  margin: 0;
  font-size: 0.9rem;
  font-weight: normal;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
