<template>
  <div class="site-wrapper">
    <div class="heading">
      <h1>Über mich</h1>
      <p>Schön, dass du hier bist. Ich freue mich, dich bei der Gestaltung einer unvergesslichen Zeremonie zu begleiten
        – ganz nach deinen Wünschen und Vorstellungen.</p>
    </div>
    <div class="image-section">
      <div class="right-section">
        <div class="image-wrapper">
          <img :src="getImage('hochzeit1.png')" alt="">
        </div>
        <div class="text-section">
          <h3>einfach Ich</h3>
          <div>
            <p> Es freut mich sehr, dass es Euch auf meine Seite verschlagen hat!</p>
            <p> Gerne möchte ich euch ein bisschen von mir erzählen, aber natürlich noch viel lieber bei unserem
              persönlichen Erstgespräch.</p>
            <p> Seit Kurzem habe ich das Wandern mit meiner Frau und Tochter für mich entdeckt, es ist nur schade, dass
              unsere Josie (Katze) da nicht mitkommen kann. Natürlich werden dann zu Hause die Kuscheleinheiten
              nachgeholt.</p>
          </div>
        </div>
      </div>
      <div class="left-section">
        <div class="image-wrapper">
          <img :src="getImage('hochzeit2.png')" alt="">
        </div>
      </div>
    </div>
    <DynamicAccordion :accordion-items="faqs"/>
  </div>
  <div class="banner">
    <div class="inner-banner">
      <div class="text">
        <h2>"Ich möchte Menschen so ehren, dass sich die Gäste nicht über die Länge der Zeremonie beschweren."</h2>
        <p>Mit Feingefühl gestalte ich Zeremonien, die berühren und in guter Erinnerung bleiben.</p>

        <DynamicButton
            :has-link="true"
            path-name="home"
            hash="#contact"
            button-text="Kontakt"
            :button-type="ButtonType.Primary"
        />
      </div>
      <div class="image-wrapper">
        <img :src="getImage('hochzeit3.png')" alt="">
      </div>
    </div>
  </div>
  <div class="site-wrapper">
    <div class="video-section">
      <div class="image-wrapper">
        <img :src="getImage('tomvideo.png')" alt="tomvideo">
      </div>
      <div class="facts-wrapper">
        <div v-for="(fact,index) in facts"
             :key="index"
             class="fact">
          <div class="icon-wrapper">
            <img :src="getImage(fact.icon)" :alt="fact.alt">
          </div>
          <p>{{ fact.text }}</p>
        </div>
      </div>
    </div>
  </div>

</template>

<script setup lang="ts">

import DynamicAccordion from "@/components/DynamicAccordion.vue";
import {ref} from "vue";
import {getImage} from "@/utils/ImageUtils";
import {ButtonType} from "@/models/ButtonTypes";
import DynamicButton from "@/components/DynamicButton.vue";

const faqs = ref([
  {
    id: 1,
    question: "Wie bist du dazu gekommen, freier Redner zu werden?",
    answer: "Schon immer habe ich es geliebt, mit Worten Menschen zu berühren. Durch meine Leidenschaft für das Schreiben und Sprechen sowie die Freude an besonderen Momenten, habe ich mich entschieden, Menschen als freier Redner bei ihren Zeremonien zu begleiten."
  },
  {
    id: 2,
    question: "Was macht dir am meisten Freude an deiner Arbeit?",
    answer: "Es ist die Verbindung zu den Menschen, die Geschichten, die ich erzählen darf, und die Emotionen, die während einer Zeremonie spürbar werden. Jedes Paar und jede Familie ist einzigartig, und diese Einzigartigkeit in den Zeremonien widerzuspiegeln, erfüllt mich."
  },
  {
    id: 3,
    question: "Was unterscheidet dich von anderen freien Rednern?",
    answer: "Ich lege großen Wert darauf, jede Zeremonie individuell und persönlich zu gestalten. Mein Ziel ist es, eine Atmosphäre zu schaffen, in der sich alle wohlfühlen und in der eure Geschichte authentisch erzählt wird."
  },
  {
    id: 4,
    question: "Welche Sprachen sprichst du für Zeremonien?",
    answer: "Ich halte Zeremonien in Deutsch und Englisch. So können auch internationale Gäste die Zeremonie vollständig verstehen und erleben."
  },
  {
    id: 5,
    question: "Wie bereitest du dich auf eine Zeremonie vor?",
    answer: "Nach unserem ersten Gespräch beginne ich mit der Planung und Gestaltung der Zeremonie. Ich schreibe die Rede, stimme mich regelmäßig mit euch ab und sorge dafür, dass alles genau so wird, wie ihr es euch wünscht."
  }
]);

const facts = ref([
  {
    icon: 'ic_language.png',
    alt: 'buchstabe icon',
    text: 'Deutsch, Englisch'
  },
  {
    icon: 'ic_microphone.png',
    alt: 'mikrofon icon',
    text: 'Trauung, Kinderwillkommensfest'
  },
  {
    icon: 'ic_paint.png',
    alt: 'malen icon',
    text: 'Liebt Pizza,gute Serien und redet gern'
  },
  {
    icon: 'ic_graduation.png',
    alt: 'hut icon',
    text: 'Zertifizierter Freier Redner (ZFR)'
  }
])

</script>

<style scoped>

.heading {
  display: flex;
  flex-direction: column;
  gap: 16px;

  p {
    font-size: 16px;
  }
}

.image-section {
  display: flex;
  flex-direction: column;
  gap: 16px;

  .right-section {
    display: flex;
    flex-direction: column;
    gap: 16px;

    .text-section {
      display: flex;
      flex-direction: column;
      gap: 8px;
    }
  }

  .image-wrapper {
    display: flex;
    align-items: center;
    justify-content: center;

    img {
      width: 100%;
      height: 100%;
      border-radius: 14px;
    }
  }
}

.banner {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: var(--creme);
  box-sizing: border-box;
  padding: 24px 0;

  .inner-banner {
    width: 320px;
    display: flex;
    flex-direction: column;
    gap: 36px;

    .text {
      display: flex;
      flex-direction: column;
      gap: 16px;
    }

    .image-wrapper {
      display: flex;
      align-items: center;
      justify-content: center;

      img {
        width: 100%;
        height: 100%;
        border-radius: 14px;
        object-fit: cover;
      }
    }
  }
}

.video-section {
  display: flex;
  flex-direction: column;
  gap: 36px;

  .image-wrapper {
    img {
      width: 100%;
      height: 100%;
      border-radius: 14px;
    }
  }

  .facts-wrapper {
    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;
    gap: 8px;

    .fact {
      display: flex;
      flex-direction: column;
      align-items: center;
      text-align: center;


      .icon-wrapper {
        display: flex;
        align-items: center;
        justify-content: center;

        img {
          width: 40px;
          height: 40px;
        }
      }
    }
  }
}

@media (min-width: 740px) {
  .image-section {
    display: flex;
    flex-direction: row-reverse;
    gap: 16px;

    .right-section {
      width: 40%;
      display: flex;
      flex-direction: column;
      gap: 16px;

      .text-section {
        display: flex;
        flex-direction: column;
        gap: 8px;
      }
    }

    .left-section {
      width: 60%;
      align-self: flex-end;
    }

    .image-wrapper {
      display: flex;
      align-items: center;
      justify-content: center;

      img {
        width: 100%;
        height: 100%;
        border-radius: 14px;
      }
    }
  }

  .banner {
    .inner-banner {
      width: 620px;
      display: flex;
      flex-direction: column;
      gap: 36px;

      .text {
        display: flex;
        flex-direction: column;
        gap: 16px;
      }

      .image-wrapper {
        display: flex;
        align-items: center;
        justify-content: center;

        img {
          width: 100%;
          height: 300px;
          border-radius: 14px;
          object-position: center;
        }
      }
    }
  }

  .video-section {
    display: flex;
    flex-direction: row-reverse;
    gap: 36px;

    .image-wrapper {
      width: 50%;

      img {
        width: 100%;
        height: 100%;
        border-radius: 14px;
        object-fit: cover;
      }
    }

    .facts-wrapper {
      width: 50%;
      display: flex;
      align-items: center;
      flex-direction: column;
      justify-content: center;
      gap: 8px;

      .fact {
        display: flex;
        flex-direction: column;
        align-items: center;
        text-align: center;


        .icon-wrapper {
          display: flex;
          align-items: center;
          justify-content: center;

          img {
            width: 40px;
            height: 40px;
          }
        }
      }
    }
  }

}


@media (min-width: 1200px) {
  .heading {
    display: flex;
    flex-direction: row;
    align-items: flex-end;
    justify-content: space-between;


    h1 {
      white-space: nowrap;
    }

    p {
      width: 40%;
    }
  }

  .image-section {
    display: flex;
    flex-direction: row-reverse;
    gap: 16px;

    .right-section {
      width: 40%;
      display: flex;
      flex-direction: column;
      gap: 40px;

      .image-wrapper {
        justify-content: flex-end;

        img {
          width: 250px;
        }
      }
    }

    .left-section {
      width: 60%;
      align-self: flex-end;

      .image-wrapper {
        justify-content: flex-start;

        img {
          width: 400px;
        }
      }
    }

    .image-wrapper {
      display: flex;
      align-items: center;
      justify-content: center;

      img {
        width: 100%;
        height: 100%;
        border-radius: 14px;
      }
    }
  }


  .banner {
    padding: 50px 0;

    .inner-banner {
      width: 830px;
      display: flex;
      flex-direction: row;
      justify-content: space-between;

      .text {
        width: 50%;
        display: flex;
        flex-direction: column;
      }

      .image-wrapper {
        width: 400px;
        height: 300px;
        display: flex;
        align-items: center;
        justify-content: flex-end;

        img {
          width: 100%;
          height: 100%;
          border-radius: 14px;
          object-position: center;
        }
      }
    }
  }


  .video-section {
    display: flex;
    flex-direction: row-reverse;
    gap: 36px;

    .image-wrapper {
      width: 50%;

      img {
        width: 100%;
        height: 100%;
        border-radius: 14px;
        object-fit: cover;
      }
    }

    .facts-wrapper {
      width: 50%;
      display: flex;
      align-items: start;
      flex-direction: column;
      gap: 0;
      justify-content: space-between;

      .fact {
        display: flex;
        flex-direction: row;
        align-items: center;
        gap: 10px;


        .icon-wrapper {
          display: flex;
          align-items: center;
          justify-content: center;

          img {
            width: 40px;
            height: 40px;
          }
        }
      }
    }
  }
}

@media (min-width: 1920px) {
  .image-section {
    display: flex;
    flex-direction: row-reverse;
    gap: 16px;

    .right-section {
      width: 40%;
      display: flex;
      flex-direction: column;
      gap: 60px;

      .image-wrapper {
        justify-content: flex-end;

        img {
          width: 320px;
        }
      }
    }

    .left-section {
      width: 60%;
      align-self: flex-end;

      .image-wrapper {
        justify-content: flex-start;

        img {
          width: 500px;
        }
      }
    }

    .image-wrapper {
      display: flex;
      align-items: center;
      justify-content: center;

      img {
        width: 100%;
        height: 100%;
        border-radius: 14px;
      }
    }
  }

  .banner {
    padding: 50px 0;

    .inner-banner {
      width: 1048px;
      display: flex;
      flex-direction: row;
      justify-content: space-between;

      .text {
        width: 50%;
        display: flex;
        flex-direction: column;
      }

      .image-wrapper {
        width: 500px;
        height: inherit;
        display: flex;
        align-items: center;
        justify-content: flex-end;

        img {
          width: 100%;
          height: 100%;
          border-radius: 14px;
          object-position: center;
        }
      }
    }
  }

  .video-section {
    display: flex;
    flex-direction: row-reverse;
    gap: 36px;

    .image-wrapper {
      width: 40%;

      img {
        width: 100%;
        height: 100%;
        border-radius: 14px;
        object-fit: cover;
      }
    }


  }
}

</style>