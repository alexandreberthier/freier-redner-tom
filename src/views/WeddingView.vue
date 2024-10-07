<template>
  <div class="site-wrapper">
    <h1>Hochzeit</h1>
    <DynamicAccordion :show-c-t-a="true" :accordion-items="faqs"/>
  </div>
</template>

<script setup lang="ts">

import DynamicAccordion from "@/components/DynamicAccordion.vue";
import {ref} from "vue";

const faqs = ref([
  {
    id: 1,
    question: "Was unterscheidet eine freie Trauung von einer kirchlichen oder standesamtlichen Trauung?",
    answer: "Eine freie Trauung ist unabhängig von religiösen oder staatlichen Vorgaben. Sie bietet euch die Freiheit, eure Zeremonie nach euren eigenen Vorstellungen zu gestalten, sei es durch persönliche Gelübde, Rituale oder Beiträge von Freunden und Familie."
  },
  {
    id: 2,
    question: "Wie läuft die Planung einer freien Trauung ab?",
    answer: "Wir treffen uns zu einem persönlichen Gespräch, um eure Wünsche und Vorstellungen zu besprechen. Basierend darauf gestalte ich eine individuelle Zeremonie, die perfekt zu euch passt. Ihr habt dabei jederzeit die Möglichkeit, aktiv mitzuwirken und eigene Ideen einzubringen."
  },
  {
    id: 3,
    question: "Können Freunde und Familie in die Trauung eingebunden werden?",
    answer: "Ja, absolut! Freunde und Familie können durch Reden, Musik oder andere Beiträge aktiv an der Zeremonie teilnehmen. Ihr könnt auch gemeinsam mit ihnen besondere Rituale gestalten, die eure Trauung noch persönlicher machen."
  },
  {
    id: 4,
    question: "Kann eine freie Trauung auch im Ausland stattfinden?",
    answer: "Ja, ich bin flexibel und reise gerne an euren Wunschort – sei es im In- oder Ausland. Wichtig ist, dass die Location zu euch passt und eine schöne Atmosphäre für eure Trauung bietet."
  },
  {
    id: 5,
    question: "Wie lange dauert eine freie Trauung?",
    answer: "Eine freie Trauung dauert in der Regel zwischen 30 und 45 Minuten, je nach Ablauf und individuellen Beiträgen. Die Dauer kann selbstverständlich an eure Wünsche angepasst werden."
  }
]);




</script>

<style scoped>

</style>