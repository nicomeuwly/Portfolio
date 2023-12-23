<script>
import Window from "@/components/Window.vue";
import ListElement from "@/components/listElement.vue";

export default {
  name: "PathWindow",
  components: {
    Window,
    ListElement,
  },
  methods: {
    receiveDataFromChild(data) {
      this.$emit("parent-to-grandparent", data);
    },
  },
  data() {
    return {
      education: {
        1: {
          title: "Bachelor en Ingénierie des médias",
          date: "2024",
          description: "HEIG-VD, Yverdon-les-Bains",
        },
        2: {
          title: "Brevet de promotion sous-officier",
          date: "2020",
          description: "ER av 81-2/20, Payerne",
        },
        3: {
          title: "Maturité professionnelle commerciale",
          date: "2019",
          description: "GYB, Payerne",
        },
        4: {
          title: "CFC employé de commerce",
          date: "2019",
          description: "GYB, Payerne",
        },
      },
      experience: {
        1: {
          title: "Customer Service Representative",
          date: "2021-23",
          description: "Digitec Galaxus AG, Lausanne, 20-40%",
        },
        2: {
          title: "Customer Service Representative",
          date: "2021",
          description: "Digitec Galaxus AG, Lausanne, 100%",
        },
        3: {
          title: "Chef de groupe",
          date: "2020",
          description: "ER av 81-2/20, Payerne, 100%",
        },
        4: {
          title: "Ordonnance de bureau",
          date: "2020",
          description: "ER av 81-1/20, Payerne, 100%",
        },
        5: {
          title: "Employé d’administration",
          date: "2019",
          description: "Police cantonale Fribourg, Granges-Paccot, 100%",
        },
        6: {
          title: "Stagiaire 3+1",
          date: "2018-19",
          description: "Police cantonale Fribourg, Granges-Paccot, 100%",
        },
      },
    }
  }
};
</script>

<template>
  <Window @child-to-parent="receiveDataFromChild">
    <div class="list-element-container">
      <ListElement v-for="(element, id) in education" :key="parseInt(id)" :id="parseInt(id)" :idName="'education'"
        :title="element.title" :date="element.date" :description="element.description" />
    </div>
  </Window>
</template>

<style scoped>
.list-element-container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  gap: 50%;
  height: 76%;
  overflow-y: scroll;
}
.list-element-container::-webkit-scrollbar {
  display: none;
}
</style>
