<template>
  <div class="site-wrapper">
    <h1>Lebensfeier / Trauerfeier</h1>
    <DynamicAccordion :show-c-t-a="true" :accordion-items="faqs"/>
  </div>
</template>

<script setup lang="ts">

import DynamicAccordion from "@/components/DynamicAccordion.vue";
import {ref} from "vue";

const faqs = ref([
  {
    id: 1,
    question: "Was ist der Unterschied zwischen einer Lebensfeier und einer traditionellen Trauerfeier?",
    answer: "Eine Lebensfeier legt den Fokus darauf, das Leben und die Erinnerungen an die verstorbene Person zu würdigen. Im Gegensatz zu einer traditionellen Trauerfeier, bei der oft der Schmerz des Verlusts im Vordergrund steht, geht es bei der Lebensfeier darum, die positiven Momente und das Vermächtnis der Person zu feiern."
  },
  {
    id: 2,
    question: "Wie gestaltest du eine Lebensfeier oder Trauerfeier?",
    answer: "Jede Feier ist individuell und richtet sich nach den Wünschen der Angehörigen sowie dem Leben der verstorbenen Person. Gemeinsam besprechen wir, welche Elemente und Geschichten in die Zeremonie eingebunden werden sollen, um eine persönliche und würdige Verabschiedung zu gestalten."
  },
  {
    id: 3,
    question: "Welche Rituale können in eine Lebens- oder Trauerfeier eingebunden werden?",
    answer: "Es gibt viele Möglichkeiten: Von symbolischen Handlungen wie dem Entzünden von Kerzen über musikalische Beiträge bis hin zu persönlichen Erinnerungen von Familie und Freunden. Wir können traditionelle Rituale ebenso integrieren wie individuell gestaltete Elemente."
  },
  {
    id: 4,
    question: "Wie lange dauert eine Lebensfeier oder Trauerfeier?",
    answer: "In der Regel dauert eine Feier etwa 30 bis 60 Minuten, je nachdem, wie viele Beiträge und Rituale integriert werden. Die Dauer kann flexibel an die Wünsche der Familie angepasst werden."
  },
  {
    id: 5,
    question: "In welcher Umgebung kann eine Lebens- oder Trauerfeier stattfinden?",
    answer: "Die Feier kann an jedem Ort stattfinden, der für die Familie und die verstorbene Person von Bedeutung ist. Ob im Freien, in einer Trauerhalle oder an einem besonderen Ort – ich bin flexibel und unterstütze euch bei der Auswahl des passenden Rahmens."
  }
]);



</script>

<style scoped>

</style>