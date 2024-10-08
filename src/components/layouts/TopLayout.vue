<template>
  <div class="site-wrapper">
    <div class="heading">
      <h1>{{ header }}</h1>
      <p>{{ subHeader }}</p>
    </div>
    <div class="image-section">
      <div class="right-section">
        <div ref="image1Ref" class="image-wrapper fade-from-left">
          <img v-if="image1" :src="getImage(image1)" :alt="image1">
        </div>
        <div class="text-section">
          <h3>{{ textTitle }}</h3>
          <div v-html="textContent"></div>
        </div>
      </div>
      <div class="left-section">
        <div ref="image2Ref" class="image-wrapper fade-from-right">
          <img v-if="image2" :src="getImage(image2)" :alt="image2">
        </div>
      </div>
    </div>
    <slot></slot>
  </div>
</template>


<script setup lang="ts">
import { ref, onMounted } from "vue";
import { getImage } from "@/utils/ImageUtils";

defineProps<{
  header: string;
  subHeader: string;
  image1: string;
  image2: string;
  textTitle: string;
  textContent: string;
}>();

const image1Ref = ref<HTMLElement | null>(null);
const image2Ref = ref<HTMLElement | null>(null);

const fadeInObserver = (el: HTMLElement, className: string) => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add(className);
        observer.unobserve(entry.target);
      }
    });
  }, {
    threshold: 0.1
  });
  observer.observe(el);
};

onMounted(() => {
  if (image1Ref.value) {
    fadeInObserver(image1Ref.value, 'fade-in-left');
  }
  if (image2Ref.value) {
    fadeInObserver(image2Ref.value, 'fade-in-right');
  }
});
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

    .image-wrapper {
      display: flex;
      align-items: center;
      justify-content: center;

      img {
        width: 100%;
        height: 100%;
        max-height: 200px;
        border-radius: 14px;
        object-fit: cover;
        object-position: top;

      }
    }

    .text-section {
      display: flex;
      flex-direction: column;
      gap: 8px;
    }
  }

  .left-section {
    .image-wrapper {
      display: flex;
      align-items: center;
      justify-content: center;


      img {
        width: 100%;
        height: 100%;
        max-height: 320px;
        border-radius: 14px;
        object-fit: cover;
        object-position: top;

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

      .image-wrapper {
        img {
          max-width: 242px;
        }
      }

      .text-section {
        display: flex;
        flex-direction: column;
        gap: 8px;
      }
    }

    .left-section {
      width: 60%;
      align-self: flex-end;

      .image-wrapper {
        img {
          max-width: 360px;
          max-height: 360px;
          min-height: 360px;
        }
      }

    }
  }

  @media (min-width: 1200px) {
    .heading {
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: space-between;

      h1 {
        word-break: keep-all;
        width: 400px;
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
            max-width: 400px;
            max-height: 400px;
            min-height: 400px;
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
            max-width: 320px;
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
            max-width: 500px;
            min-height: 500px;
            max-height: 500px;
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
  }
}
.image-wrapper {
  opacity: 0;
  transition: transform 0.6s ease-out, opacity 0.6s ease-out;
}

.fade-from-left {
  transform: translateX(-50px);
}

.fade-in-left {
  transform: translateX(0);
  opacity: 1;
}

.fade-from-right {
  transform: translateX(50px);
}

.fade-in-right {
  transform: translateX(0);
  opacity: 1;
}

</style>