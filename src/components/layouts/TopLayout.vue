<template>
  <div class="site-wrapper">
    <div class="heading">
      <h1>{{ header }}</h1>
      <p>{{ subHeader }}</p>
    </div>
    <div class="image-section">
      <div class="right-section">
        <div class="image-wrapper">
          <img :src="getImage(image1)" :alt="image1">
        </div>
        <div class="text-section">
          <h3>{{textTitle}}</h3>
          <div v-html="textContent">

          </div>
        </div>
      </div>
      <div class="left-section">
        <div class="image-wrapper">
          <img :src="getImage(image2)" :alt="image2">
        </div>
      </div>
    </div>
    <slot></slot>
  </div>
</template>

<script setup lang="ts">

import {getImage} from "@/utils/ImageUtils";

defineProps<{
  header: string,
  subHeader: string
  image1: string,
  image2: string
  textTitle: string
  textContent:string
}>()

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


</style>