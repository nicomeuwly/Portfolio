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
  data() {
    return {
      blocks: [{ id: 1 }, { id: 2 }, { id: 3 }, { id: 4 }, { id: 5 }, { id: 6 }, { id: 8 }],
      characterPosition: {
        x: 0,
        y: 80,
      },
      defaultCharacterHeight: 0,
      gameWidth: 0,
      ready: false,
      characterWidth: 0,
      characterIsJumping: false,
      characterCurrentPosition: 0,
      jumpLevel: 0,
    };
  },
  methods: {
    receiveDataFromChild(data) {
      this.$emit("parent-to-grandparent", data);
    },
    openJob(id, blockId) {
      this.$emit("open-job", id, blockId);
    },
    handleCharacterLeftPosition(newValue) {
      this.characterCurrentPosition = newValue;
    },
    handleCharacterJumping(newValue) {
      this.characterIsJumping = newValue;
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
    setGameDimensions() {
      this.$nextTick(() => {
        const floorPosition = this.$refs.floor.getBoundingClientRect();
        const blockContainerHeight = this.$refs.blockContainer.offsetHeight;
        const floorHeight = this.$refs.floor.offsetHeight;
        const gameContainerHeight = this.$refs.gameContainer.offsetHeight;
        const marginUpAndDown = window.innerHeight * 0.63;
        this.$refs.characterContainer.style.height = gameContainerHeight - floorHeight - blockContainerHeight - 15 + "px";
        const characterContainerHeight = this.$refs.characterContainer.offsetHeight;
        this.characterPosition.y = floorPosition.top - marginUpAndDown;
        this.defaultCharacterHeight = floorPosition.top - marginUpAndDown;
        const image = new Image();
        image.src = "/img/character/Anim-0.png";
        image.onload = () => {
          this.characterWidth = image.width;
          this.jumpLevel = characterContainerHeight - image.height;
          this.gameWidth = this.$refs.gameContainer.offsetWidth - this.characterWidth;
          this.ready = true;
        };
      });
    },
    characterHitBlock() {
      const characterMidPosition = this.characterCurrentPosition + (this.characterWidth / 2);
      this.blocks.forEach((block) => {
        if (
          characterMidPosition >= block.left &&
          characterMidPosition <= block.left + 220 &&
          this.characterIsJumping
        ) {
          const blockElement = document.getElementById("block" + block.id);
          setTimeout(() => {
            blockElement.classList.add("hit");
          }, 200);
          setTimeout(() => {
            blockElement.classList.remove("hit");
            this.openJob(13, block.id);
          }, 700);
        }
      });
    },
  },
  mounted() {
    this.getBlockPositions();
    this.setGameDimensions();
  },
  watch: {
    characterIsJumping(newValue) {
      if (newValue) {
        this.characterHitBlock();
      }
    },
  }
};
</script>

<template>
  <Window @child-to-parent="receiveDataFromChild">
    <div class="game-container" ref="gameContainer">
      <div class="block-container" ref="blockContainer">
        <Block v-for="block in blocks" :key="block.id" :id="'block' + block.id" @click="openJob(13, block.id)"/>
      </div>
      <div class="character-container" ref="characterContainer">
        <Character @update-position-x="handleCharacterLeftPosition" @update-is-jumping="handleCharacterJumping"
          v-if="ready" :position="characterPosition" :maxLeftPosition="0" :maxRightPosition="gameWidth"
          :defaultHeight="defaultCharacterHeight" :jumpValue="jumpLevel" />
      </div>
      <div class="floor" ref="floor"></div>
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

.character-container {
  width: 100%;
  position: relative;
  top: 20px;
}

.floor {
  width: 100%;
  height: 3%;
  background-color: var(--white);
  border-radius: 20px;
}

.hit {
  transform: translateY(-15px);
}

</style>
