<template>
  <div class="back-to-list-from-details">
    <img
      class="back-to-list-img"
      @click="goToHousesPage"
      src="@/assets/icons/actions/grey-back-icon.png"
      alt="Back to list button"
    />
    <p @click="goToHousesPage">Back to overview</p>
  </div>
  <div @click="goToHousesPage" class="back-mobile">
    <button>
      <img :src="backImg" alt="back icon" />
    </button>
  </div>
</template>

<script setup>
import { useRouter } from "vue-router";
import { computed, defineProps } from "vue";
import backImgBlack from "@/assets/icons/actions/grey-back-icon.png";
import backImgWhite from "@/assets/icons/actions/white-back-icon.png";

const props = defineProps({
  styling: {
    type: String,
    required: true,
    default: "black",
  },
});

const backImg = computed(() => {
  if (props.styling === "black") {
    return backImgBlack;
  } else if (props.styling === "white") {
    return backImgWhite;
  }
});

const router = useRouter();

const goToHousesPage = () => {
  router.push({ name: "HousesPage" }).catch((error) => {});
};
</script>

<style>
@media (min-width: 880px) {
  .back-mobile {
    display: none;
  }
}

.back-to-list-from-details {
  display: flex;
  flex-direction: row;
  align-items: center;
  font-family: Montserrat;
  font-weight: 700;
  font-size: 14px;
  margin-bottom: 10px;
}

.back-to-list-from-details img {
  margin-right: 10px;
  width: 25px;
  height: auto;
  cursor: pointer;
}

.back-to-list-from-details p {
  margin-right: 10px;
  cursor: pointer;
}

@media (max-width: 880px) {
  .back-to-list-from-details {
    display: none;
  }

  .back-mobile {
    position: absolute;
    top: 30px;
    left: 20px;
  }

  .back-mobile img {
    margin: 3px 8px;
    width: 20px;
    height: 20px;
  }

  .back-mobile button {
    background-color: rgba(44, 45, 45, 0);
    border: none;
    cursor: pointer;
    border-radius: 5px;
    margin-left: 2px;
    padding: 3px;
  }
}
</style>
