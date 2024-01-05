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
      <ul>
        <li>
          <img src="/img/icons/Name-Icon.svg" alt="Name Icon" />Nicolas Meuwly
        </li>
        <li><img src="/img/icons/Age-Icon.svg" alt="Age Icon" />25 ans</li>
        <li>
          <img src="/img/icons/Location-Icon.svg" alt="Location Icon" />Cugy FR
        </li>
        <li>
          <img src="/img/icons/Diploma-Icon.svg" alt="Diploma Icon" />Bachelor
          en Ingénierie des médias (en cours)
        </li>
      </ul>
      <div id="profile-picture-container">
        <img
          src="/img/Profile-Picture.jpeg"
          alt="Profile Picture"
          id="profile-picture"
        />
        <MainButton :name="'LinkedIn'" :link="'https://www.linkedin.com/in/nicolas-meuwly/'"/>
      </div>
    </div>
  </Window>
</template>

<style scoped>
ul {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: left;
  gap: 25px;
}

li {
  color: var(--white);
  font-weight: bold;
  font-size: 2rem;
  display: flex;
  align-items: center;
  list-style: none;
}

li img {
  width: 50px;
  height: 50px;
  margin-right: 25px;
}

#profile-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  height: 100%;
}

#profile-picture {
  width: 250px;
  height: 250px;
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
