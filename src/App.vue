<script>
import Home from "@/views/Home.vue";

export default {
  name: "App",
  components: {
    Home,
  },
};
</script>

<template>
  <div id="portfolio">
    <Home />
  </div>
  <div id="mobileview">
    <span class="material-symbols-rounded">error</span>
    <h1>Affichage sur mobile</h1>
    <p>
      Désolé pour le désagrément, mais mon site n'est pas encore pleinement
      adapté à votre appareil. Pour une expérience optimale, je vous recommande
      de consulter le site sur un ordinateur. Je travaille activement à
      améliorer cette compatibilité. Merci de votre compréhension !
    </p>
    <div class="links">
      <a href="https://github.com/nicomeuwly"
        ><img src="/img/logos/GitHub-White.png" alt="github"
      /></a>
      <a href="https://www.linkedin.com/in/nicolas-meuwly/"
        ><img src="/img/logos/LinkedIn-White.png" alt="linkedin"
      /></a>
    </div>
  </div>
</template>

<style>
#portfolio {
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
}
#mobileview {
  display: none;
}

#mobileview h1, #mobileview p{
  color: var(--white);
  width: 80%;
  text-align: center;
}
.links {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  width: 60%;
  height: 8%;
}
.links img {
  height: 100%;
}
#mobileview span {
  font-size: 5rem;
  color: var(--white);
}
.material-symbols-rounded {
  font-variation-settings: "FILL" 0, "wght" 400, "GRAD" 0, "opsz" 24;
}
@media screen and (max-width: 768px) {
  #portfolio {
    display: none;
  }
  #mobileview {
    width: 100vw;
    height: 100dvh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 1rem;
    background-color: var(--blue-dark);
  }
}
</style>
