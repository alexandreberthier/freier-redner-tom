<template>
  <div class="site-wrapper">
    <section ref="hero" class="hero fade-up">
      <h1>Gemeinsam gestalten wir unvergessliche Momente</h1>
      <p>
        Egal ob Hochzeit, Lebensfeier oder ein ganz besonderer Anlass
        – mit einfühlsamen Worten und deiner Geschichte machen wir deine
        Feier zu einem einzigartigen Erlebnis.
        Lass uns gemeinsam Erinnerungen schaffen, die im Herzen bleiben.
      </p>
      <div class="button-section">
        <DynamicButton
            :button-type="ButtonType.Primary"
            :has-link="true"
            path-name="home"
            hash="#contact"
            button-text="Lass uns Reden"
        />
        <DynamicButton
            :button-type="ButtonType.Secondary"
            :has-link="true"
            path-name="about"
            button-text="Über mich"
        />
      </div>
    </section>
    <section class="hero-images">
      <div ref="image1" class="image-wrapper fade-up">
        <img class="image1" :src="getImage('hochzeit1.png')" alt="hochzeit">
      </div>
      <div ref="image2" class="image-wrapper fade-up">
        <img class="image2" :src="getImage('hochzeit2.png')" alt="hochzeit">
      </div>
      <div ref="image3" class="image-wrapper fade-up">
        <img class="image3" :src="getImage('hochzeit3.png')" alt="hochzeit">
      </div>
    </section>
  </div>

  <section class="text-section">
    <div ref="textSection" class="text-wrapper fade-up">
      <h2>Deine einzigartige Zeremonie – ganz nach deinen Wünschen</h2>
      <p class="sub-heading-text">
        Jede Feier ist so individuell wie die Menschen, die sie erleben. Ob Hochzeit, Lebensfeier oder ein anderer
        besonderer Anlass – ich begleite dich dabei, deine Zeremonie unvergesslich zu gestalten. Mit einfühlsamen Worten
        und kreativen Ideen schaffen wir gemeinsam einen Moment, der lange in Erinnerung bleibt.
      </p>
      <div class="text text1">
        <h3>Individuelle Worte für deine einzigartige Geschichte</h3>
        <p>Ob romantische Hochzeit, emotionale Lebensfeier oder besondere Meilensteine – ich finde die richtigen Worte
          für dich. Persönlich, einfühlsam und mit viel Herz erzähle ich deine Geschichte so, wie du sie dir wünschst.
          Deine Feier wird dadurch zu einem einzigartigen Erlebnis.</p>
      </div>
      <div class="text text2">
        <h3>Gemeinsam schaffen wir unvergessliche Erinnerungen</h3>
        <p>Egal ob groß oder klein, fröhlich oder emotional – ich sorge dafür, dass deine Feier genau das ausdrückt, was
          dir wichtig ist. Mit viel Liebe zum Detail und einem Gespür für besondere Momente mache ich deine Zeremonie zu
          einem Highlight, das dich und deine Gäste berühren wird.</p>
      </div>
    </div>
  </section>

  <section class="slider-section">
    <h2>Besondere Momente, persönlich gestaltet</h2>
    <DynamicSlider :auto-rotate="false">
      <ServiceCard
          v-for="(service, index) in services"
          :key="index"
          :service="service"
      />
    </DynamicSlider>
  </section>

  <div class="site-wrapper">
    <section class="faq-section">
      <h2>FAQs</h2>
      <p>Fragen?</p>
      <div class="accordion-flex">
        <DynamicAccordion :accordion-items="faqs"/>
      </div>
    </section>

    <section id="contact" class="contact-section">
      <h2>Schreib mir eine Nachricht!</h2>
      <p>Egal ob per E-Mail, Telefon oder über das Kontaktformular – ich freue mich, von Dir zu hören und Deine Fragen
        zu beantworten.</p>
      <div class="contact-options">
        <a v-for="(option, index) in contactOptions"
           :key="index"
           :href="option.href">
          <div class="option">
            <div class="icon-wrapper">
              <img :src="getImage(option.image)" :alt="option.alt">
            </div>
            <p>{{ option.text }}</p>
          </div>
        </a>
      </div>
      <div class="form-section">
        <h3 class="extra-margin">Kontaktformular</h3>
        <div class="input-flex">
          <DynamicInputField
              :type="InputType.Text"
              label="Vorname"
              v-model:user-input="firstName"
              v-model:error="firstNameError"
          />
          <DynamicInputField
              :type="InputType.Text"
              label="Nachname"
              v-model:user-input="lastName"
              v-model:error="lastNameError"
          />
        </div>
        <div class="input-flex">
          <DynamicInputField
              label="E-Mail"
              :type="InputType.Email"
              v-model:user-input="email"
              v-model:error="emailError"
          />
          <DynamicInputField
              label="Telefonnummer"
              :type="InputType.Phone"
              v-model:user-input="phoneNumber"
              v-model:error="phoneNumberError"
          />
        </div>
        <DynamicInputField
            :type="InputType.Text"
            label="Deine Nachricht"
            :text-area="true"
            v-model:user-input="message"
            v-model:error="messageError"
        />
        <div class="button-wrapper">
          <DynamicButton
              @click="sendContactForm"
              button-text="Senden"
              :button-type="ButtonType.Primary"
          />
          <p v-if="successMessage">{{ successMessage }}</p>
          <p v-if="errorMessage">{{ errorMessage }}</p>
        </div>
      </div>
    </section>
  </div>

</template>

<script setup lang="ts">
import {nextTick, onMounted, type Ref, ref} from 'vue';
import DynamicButton from "@/components/DynamicButton.vue";
import {ButtonType} from "@/models/ButtonTypes";
import {getImage} from "@/utils/ImageUtils";
import DynamicSlider from "@/components/DynamicSlider.vue";
import ServiceCard from "@/components/ServiceCard.vue";
import type {Service} from "@/models/PropInterfaces";
import DynamicInputField from "@/components/DynamicInputField.vue";
import {InputType} from "@/models/Enums";
import emailjs from 'emailjs-com';
import DynamicAccordion from "@/components/DynamicAccordion.vue";

interface ContactOption {
  href: string,
  text: string,
  image: string,
  alt: string
}

const firstName: Ref<string> = ref('')
const lastName: Ref<string> = ref('')
const phoneNumber: Ref<string> = ref('')
const email: Ref<string> = ref('')
const message: Ref<string> = ref('')

const firstNameError: Ref<string> = ref('')
const lastNameError: Ref<string> = ref('')
const phoneNumberError: Ref<string> = ref('')
const emailError: Ref<string> = ref('')
const messageError: Ref<string> = ref('')

const successMessage: Ref<string> = ref('')
const errorMessage: Ref<string> = ref('')

const SERVICE_ID = import.meta.env.VITE_EMAILJS_SERVICE_ID;
const TEMPLATE_ID = import.meta.env.VITE_EMAILJS_TEMPLATE_ID;
const USER_ID = import.meta.env.VITE_EMAILJS_USER_ID;

function sendContactForm() {
  let isValid = true;

  const fields = [
    { value: firstName, error: firstNameError },
    { value: lastName, error: lastNameError },
    { value: email, error: emailError },
    { value: phoneNumber, error: phoneNumberError },
    { value: message, error: messageError }
  ];

  // Überprüfe jedes Feld
  fields.forEach(field => {
    if (!field.value.value) {
      field.error.value = 'Feld darf nicht leer sein';
      isValid = false;
    } else {
      field.error.value = '';
    }
  });

  // Falls es ungültige Felder gibt, scrolle zum ersten Fehlerfeld
  if (!isValid) {
    nextTick(() => {
      const firstErrorElement = document.querySelector('.input-wrapper .error');
      if (firstErrorElement) {
        firstErrorElement.scrollIntoView({ behavior: 'smooth', block: 'center' });
      }
    });
    return;
  }

  const templateParams = {
    firstName: firstName.value,
    lastName: lastName.value,
    email: email.value,
    phoneNumber: phoneNumber.value,
    message: message.value
  };

  emailjs.send(SERVICE_ID, TEMPLATE_ID, templateParams, USER_ID)
      .then(() => {
        successMessage.value = 'Formular erfolgreich gesendet!';
        firstName.value = '';
        lastName.value = '';
        email.value = '';
        phoneNumber.value = '';
        message.value = '';
      })
      .catch(error => {
        errorMessage.value = 'Formular konnte nicht gesendet werden';
        console.error('Fehler beim Senden der E-Mail:', error);
      });
}


const hero = ref(null);
const image1 = ref(null)
const image2 = ref(null)
const image3 = ref(null)
const textSection = ref(null)

const contactOptions: Ref<ContactOption[]> = ref([
  {
    href: 'mailto:hallo@freier-redner-tom.at',
    text: 'hallo@freier-redner-tom.at',
    image: 'ic_mail.png',
    alt: 'email'
  },
  {
    href: 'tel:+436701234567',
    text: '+436701234567',
    image: 'ic_phone.png',
    alt: 'telefon'
  }
])

const activeIndex: Ref<number | null> = ref(null)

function toggleContent(id: number) {
  activeIndex.value = activeIndex.value === id ? null : id
}

const services: Ref<Service[]> = ref([
  {
    image: 'bildhochzeit1.png',
    alt: 'hochzeit',
    heading: 'Hochzeit',
    text: 'Ich begleite Euch an Eurem besonderen Tag und gestalte eine Zeremonie, die Eure Liebe und Persönlichkeit auf ganz besondere Weise widerspiegelt.',
    pathName: 'wedding'
  },
  {
    image: 'kinderfest1.png',
    alt: 'kinderwillkommensfest',
    heading: 'Kinderwillkommensfest',
    text: '"Lasst uns gemeinsam die Ankunft Eures Kindes feiern und diesen neuen Lebensabschnitt mit einer herzlichen Zeremonie willkommen heißen',
    pathName: 'child-celebration'
  },
  {
    image: 'trauerfest1.png',
    alt: 'hochzeit',
    heading: 'Lebensfeier / Trauerfeier',
    text: 'Gemeinsam gestalten wir eine liebevolle Lebensfeier, die mit Wärme und persönlichem Trost an den verstorbenen Menschen erinnert.',
    pathName: 'celebrations'
  }
])

const faqs = ref([
  {
    id: 1,
    question: "Wie läuft die Vorbereitung auf die Zeremonie ab?",
    answer: "Wir treffen uns zu einem persönlichen Gespräch, um eure Wünsche und Vorstellungen genau zu besprechen. Danach bereite ich eine Zeremonie vor, die perfekt zu euch passt."
  },
  {
    id: 2,
    question: "Wie lange dauert eine Trauungs- oder Willkommenszeremonie?",
    answer: "In der Regel dauert eine Zeremonie zwischen 30 und 45 Minuten. Natürlich kann die Dauer je nach Programm und Wünschen angepasst werden."
  },
  {
    id: 3,
    question: "Können eigene Texte und Rituale in die Zeremonie eingebunden werden?",
    answer: "Absolut! Eure persönlichen Texte, Rituale oder Beiträge von Gästen sind herzlich willkommen und machen die Zeremonie noch individueller."
  },
  {
    id: 4,
    question: "Wie früh sollte man die Zeremonie planen und buchen?",
    answer: "Je früher, desto besser! Idealerweise meldet ihr euch 6 bis 12 Monate vor dem gewünschten Termin, damit genügend Zeit für die Vorbereitung bleibt."
  },
  {
    id: 5,
    question: "In welchem Umkreis bist du tätig?",
    answer: "Ich bin flexibel und arbeite in der Region und darüber hinaus. Gerne komme ich auch zu einer Location eurer Wahl – fragt einfach nach."
  }
]);


onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible');
        observer.unobserve(entry.target)
      }
    })
  }, {
    threshold: 0.1
  })

  if (hero.value) observer.observe(hero.value);
  if (image1.value) observer.observe(image1.value);
  if (image2.value) observer.observe(image2.value);
  if (image3.value) observer.observe(image3.value);
  if (textSection.value) observer.observe(textSection.value)
})
</script>

<style scoped>

.extra-margin {
  margin-bottom: 16px;
}

.hero {
  display: flex;
  flex-direction: column;
  gap: 16px;

  .button-section {
    display: flex;
    flex-direction: row;
    gap: 8px;
  }
}

.hero-images {
  display: flex;
  flex-direction: column;
  gap: 16px;

  .image-wrapper {
    display: flex;
    align-items: center;
    justify-content: center;

    img {
      object-fit: cover;
      width: 100%;
      height: auto;
      border-radius: 20px;
    }
  }
}

.text-section {
  background-color: #FFDAB9;
  width: 100%;
  padding: 60px 0;
  box-sizing: border-box;
  display: flex;
  justify-content: center;
  align-items: center;

  .text-wrapper {
    display: grid;
    width: 320px;
    grid-template-columns: auto;
    grid-template-rows: repeat(4, auto);
    grid-row-gap: 16px;
    grid-template-areas:
      "heading"
      "sub-text"
      "text1"
      "text2";

    h2 {
      grid-area: heading;
    }

    .sub-heading-text {
      grid-area: sub-text;
    }

    .text {
      display: flex;
      flex-direction: column;
      gap: 8px;

      &.text1 {
        grid-area: text1;
      }

      &.text2 {
        grid-area: text2;
      }
    }
  }
}

.slider-section {
  display: flex;
  flex-direction: column;
  gap: 16px;
  width: 320px;
  margin: 0 auto;
}

.faq-section {
  display: flex;
  flex-direction: column;
  gap: 16px;


  .accordion-flex {
    display: flex;
    flex-direction: column;
    gap: 8px;
  }
}

.contact-section {
  display: flex;
  flex-direction: column;
  gap: 16px;

  .contact-options {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 16px;

    .option {
      display: flex;
      align-items: center;
      flex-direction: column;
      gap: 8px;

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

  .form-section {
    display: flex;
    flex-direction: column;
    gap: 20px;

    .input-flex {
      display: flex;
      flex-direction: column;
      gap: 20px;
    }

    .button-wrapper {
      align-self: center;
    }
  }
}

@media (min-width: 740px) {
  .hero-images {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    height: 280px;

    .image-wrapper {
      .image1 {
        height: 250px;
        width: 300px;
        align-self: center;
      }

      .image2 {
        height: 142px;
        width: 142px;
        align-self: flex-end;
      }

      .image3 {
        height: 200px;
        width: 142px;
        align-self: flex-start;
      }
    }
  }

  .text-section {
    .text-wrapper {
      width: 620px;
      display: grid;
      grid-template-columns: repeat(2, auto);
      grid-template-rows: repeat(3, auto);
      grid-row-gap: 16px;
      grid-column-gap: 16px;
      grid-template-areas:
      "heading heading"
      "sub-text sub-text"
      "text1 text2";
    }
  }

  .slider-section {
    width: 640px;
  }

  .contact-section {
    .contact-options {
      display: flex;
      flex-direction: row;
      justify-content: center;
      align-items: center;
      gap: 80px;
    }

    .form-section {
      display: flex;
      flex-direction: column;
      gap: 20px;

      .input-flex {
        display: flex;
        flex-direction: row;

        & > * {
          width: 100%
        }
      }

      .button-wrapper {
        align-self: center;
      }
    }
  }
}


@media (min-width: 1200px) {
  .hero-images {
    display: flex;
    flex-direction: row;
    gap: 16px;
    height: 350px;

    .image-wrapper {
      .image1 {
        height: 280px;
        width: 400px;
      }

      .image2 {
        height: 180px;
        width: 170px;
      }

      .image3 {
        height: 200px;
        width: 170px;
      }
    }
  }

  .text-section {
    .text-wrapper {
      width: 830px;
    }
  }

  .slider-section {
    width: 970px;
  }
}

@media (min-width: 1920px) {
  .hero-images {
    display: flex;
    flex-direction: row;
    gap: 16px;
    height: 400px;

    .image-wrapper {
      .image1 {
        height: 350px;
        width: 600px;
      }

      .image2 {
        height: 190px;
        width: 190px;
      }

      .image3 {
        height: 250px;
        width: 190px;
      }
    }
  }

  .text-section {
    .text-wrapper {
      width: 1024px;
      display: grid;
      grid-template-columns: repeat(3, auto);
      grid-template-rows: repeat(2, auto);
      grid-row-gap: 16px;
      grid-column-gap: 16px;
      grid-template-areas:
      "heading sub-text sub-text"
      "heading text1 text2";
    }
  }
}

.fade-up {
  opacity: 0;
  transform: translateY(30px);
  transition: all 800ms ease-in-out;
}

.fade-up.visible {
  opacity: 1;
  transform: translateY(0);
}
</style>
