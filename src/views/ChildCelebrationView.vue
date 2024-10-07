<template>
  <TopLayout
      header="Kinder-willkommens-fest"
      image1="children1.jpg"
      image2="children2.jpg"
      sub-header="Gemeinsam feiern wir die Ankunft eures kleinen Schatzes mit einer liebevollen und fröhlichen Zeremonie – ganz nach euren Wünschen."
      :text-title="text.childrenTextTitle"
      :text-content="text.childrenText"
  >
    <StaticSection>
      <DynamicAccordion :show-c-t-a="true" :accordion-items="faqs"/>
    </StaticSection>
  </TopLayout>
</template>

<script setup lang="ts">

import DynamicAccordion from "@/components/DynamicAccordion.vue";
import {ref} from "vue";
import StaticSection from "@/components/layouts/StaticSection.vue";
import TopLayout from "@/components/layouts/TopLayout.vue";
import text from "@/texts/text.json"

const faqs= ref([
  {
    id: 1,
    question: "Was ist ein Kinderwillkommensfest?",
    answer: "Ein Kinderwillkommensfest ist eine persönliche und feierliche Zeremonie, um die Geburt oder den neuen Lebensabschnitt eures Kindes zu feiern. Es ist eine Alternative zur traditionellen Taufe und bietet Raum für eure individuellen Wünsche."
  },
  {
    id: 2,
    question: "Wie läuft die Vorbereitung auf ein Kinderwillkommensfest ab?",
    answer: "Wir treffen uns zu einem persönlichen Gespräch, um eure Vorstellungen und Wünsche für die Zeremonie zu besprechen. Danach entwerfe ich eine Zeremonie, die perfekt auf euch und euer Kind abgestimmt ist."
  },
  {
    id: 3,
    question: "Können Paten oder andere wichtige Personen in die Zeremonie eingebunden werden?",
    answer: "Ja, selbstverständlich! Paten, Großeltern oder andere nahestehende Personen können gerne aktiv in die Zeremonie einbezogen werden, z.B. durch persönliche Worte, Rituale oder symbolische Handlungen."
  },
  {
    id: 4,
    question: "Wie lange dauert ein Kinderwillkommensfest?",
    answer: "Die Zeremonie dauert in der Regel etwa 30 bis 45 Minuten, je nach Programm und individuellen Beiträgen. Natürlich können wir die Dauer an eure Wünsche anpassen."
  },
  {
    id: 5,
    question: "In welcher Umgebung kann das Kinderwillkommensfest stattfinden?",
    answer: "Die Zeremonie kann an einem Ort eurer Wahl stattfinden – sei es im eigenen Garten, in einem Park oder an einem anderen besonderen Ort. Ich bin flexibel und komme gerne dorthin, wo ihr euch wohlfühlt."
  }
]);


</script>

<style scoped>

</style>