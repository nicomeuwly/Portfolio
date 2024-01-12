<script>
import Window from "@/components/Window.vue";
import Character from "@/components/character.vue";
import Block from "@/components/block.vue";

export default {
  name: "JobsWindowGame",
  components: {
    Window,
    Character,
    Block,
  },
  props: {
    activeWindow: Number,
  },
  data() {
    return {
      blocks: [{ id: 1 }, { id: 2 }, { id: 3 }, { id: 4 }, { id: 5 }],
      characterPosition: {
        x: 0,
        y: 80,
      },
      gameWidth: 0,
      ready: false,
      characterWidth: 0,
      characterIsJumping: false,
      characterCurrentPosition: 0,
    };
  },
  methods: {
    receiveDataFromChild(data) {
      this.$emit("parent-to-grandparent", data);
    },
    handleCharacterLeftPosition(newValue) {
      this.characterCurrentPosition = newValue;
      console.log(this.characterCurrentPosition);
    },
    handleCharacterJumping(newValue) {
      this.characterIsJumping = newValue;
      console.log(this.characterIsJumping);
    },
    getBlockPositions() {
      this.$nextTick(() => {
        const blockContainer = this.$refs.blockContainer;
        const blockElements = blockContainer.getElementsByClassName("block");
        const marginInAndOut = window.innerWidth * 0.22;
        for (let i = 0; i < blockElements.length; i++) {
          const blockElement = blockElements[i];
          const rect = blockElement.getBoundingClientRect();
          this.blocks[i].left = rect.left - marginInAndOut;
        }
      });
    },
    setGameWidth() {
      this.$nextTick(() => {
        const image = new Image();
        image.src = "/Portfolio/img/character/Anim-0.png";
        image.onload = () => {
          this.characterWidth = image.width;
          this.gameWidth = window.innerWidth * 0.56 - image.width;
          this.ready = true;
        };
      });
    },
  },
  mounted() {
    this.getBlockPositions();
    this.setGameWidth();
  },
};
</script>

<template>
  <Window @child-to-parent="receiveDataFromChild">
    <div class="game-container" ref="gameContainer">
      <div class="block-container" ref="blockContainer">
        <Block v-for="block in blocks" :key="block.id" />
      </div>
      <Character
        @update-position-x="handleCharacterLeftPosition"
        @update-is-jumping="handleCharacterJumping"
        v-if="ready"
        :position="characterPosition"
        :maxLeftPosition="0"
        :maxRightPosition="gameWidth"
      />
      <div class="floor"></div>
    </div>
  </Window>
</template>

<style scoped>
.game-container {
  width: 100%;
  height: 100%;
  display: flex;
  flex-wrap: wrap;
  align-content: space-between;
}
.block-container {
  width: 100%;
  display: flex;
  justify-content: space-between;
  position: relative;
  top: 20px;
}
.floor {
  width: 100%;
  height: 20px;
  background-color: var(--white);
  border-radius: 20px;
}
</style>
