<script>
import Window from "@/components/Window.vue";
import MainButton from "@/components/mainButton.vue";
export default {
  name: "AboutWindow",
  components: {
    Window,
    MainButton,
  },
  methods: {
    receiveDataFromChild(data) {
      this.$emit("parent-to-grandparent", data);
    },
  },
};
</script>

<template>
  <Window @child-to-parent="receiveDataFromChild">
    <div id="profile-container">
      <div class="left-side">
        <ul>
          <li><span class="material-symbols-rounded">account_circle</span>Nicolas Meuwly</li>
          <li><span class="material-symbols-rounded">cake</span>25 ans</li>
          <li><span class="material-symbols-rounded">location_on</span>Cugy FR</li>
          <li><span class="material-symbols-rounded">school</span>Bachelor en Ingénierie des médias</li>
        </ul>
      </div>
      <div class="right-side">
        <img
          src="/img/Profile-Picture.jpeg"
          alt="Profile Picture"
          id="profile-picture"
        />
        <MainButton
          :name="'LinkedIn'"
          :link="'https://www.linkedin.com/in/nicolas-meuwly/'"
        />
      </div>
    </div>
  </Window>
</template>

<style scoped>
ul {
  list-style-type: none;
  width: 100%;
  height: 60%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}
li {
  color: var(--white);
  font-size: 2rem;
  display: flex;
  align-items: center;
  gap: 1rem;
}
.material-symbols-rounded {
  font-variation-settings: "FILL" 0, "wght" 400, "GRAD" 0, "opsz" 24;
  font-size: 3rem;
}

#profile-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  height: 100%;
}

.left-side {
  width: 50%;
  height: 100%;
  display: flex;
  align-items: center;
}

.right-side {
  width: 50%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 5%;
}

#profile-picture {
  width: 50%;
  aspect-ratio: 1/1;
  border-radius: 50%;
  border: 2px solid var(--white);
  filter: grayscale(100%);
}

#profile-picture-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 40px;
}
</style>
