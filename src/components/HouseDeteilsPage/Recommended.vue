<template>
  <div class="recommended">
    <div class="title" :class="{ dark: isDarkMode }">Recommended for you</div>
    <div class="item">
      <div
        v-for="item in recommendedItems"
        :key="item.id"
        class="item-recommended"
        :class="{ 'item-recommended-dark': isDarkMode }"
        @click="goToHouseDetails(item.id)"
      >
        <div
          class="item-img-recommended"
          :style="`background-image: url(${item.image})`"
        ></div>
        <div class="item-container-recommended">
          <div class="item-text-container">
            <div class="item-title" >
              <h5 :class="{ dark: isDarkMode }" >
                {{ item.location.street }} {{ item.location.houseNumber }}
                {{ item.location.houseNumberAddition }}
              </h5>
            </div>
            <div class="item-price" :class="{ dark: isDarkMode }">
              € {{ currencyFormatWithoutSimbol(item.price) }}
            </div>
            <div class="item-address" :class="{ dark: isDarkMode }">
              {{ item.location.zip }} {{ item.location.city }}
            </div>
          </div>
          <div class="item-properties-recommended">
            <img
              class="property"
              src="@/assets/icons/properties/bed.png"
              alt="icon of bad"
            />
            <p :class="{ dark: isDarkMode }">{{ item.rooms.bedrooms }}</p>
            <img
              class="property"
              :class="{ dark: isDarkMode }"
              src="@/assets/icons/properties/bath.png"
              alt="icon of bath"
            />
            <p :class="{ dark: isDarkMode }">{{ item.rooms.bathrooms }}</p>
            <img
              class="property"
              :class="{ dark: isDarkMode }"
              src="@/assets/icons/properties/size.png"
              alt="icon of size"
            />
            <p :class="{ dark: isDarkMode }">{{ item.size }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, inject } from "vue";
import { useRouter } from "vue-router";

const isDarkMode = inject("isDarkMode");

// Props to receive from parent component
const props = defineProps({
  item: Object,
  items: Array,
  currencyFormatWithoutSimbol: Function,
});

// Computed property for recommended items using random selection
const getRandomItems = (array, numberOfItems) => {
  const shuffled = array.sort(() => 0.5 - Math.random());
  return shuffled.slice(0, numberOfItems);
};

const recommendedItems = computed(() => {
  if (!props.item || !props.items.length) return [];
  // Filter out the currently selected item
  const filteredItems = props.items.filter((i) => i.id !== props.item.id);
  // Get 3 random items from the filtered list
  return getRandomItems(filteredItems, 3);
});

const router = useRouter();

// Define the method to navigate to the House Details page
const goToHouseDetails = (itemId) => {
  router
    .push({ name: "HouseDetailsPage", params: { id: itemId } })
    .then(() => {
      // Scroll to the top after navigation
      window.scrollTo({ top: 0, behavior: "smooth" });
    })
    .catch((error) => {
      console.error("Navigation error:", error);
    });
};
</script>

<style scoped>
.dark {
  color: white !important;
}

.item-text-container {
  min-width: 160px;
  max-width: 200px;
}

.title {
  font-size: 24px;
}

.title-dark {
  color: white;
}

.item-address {
  display: flex;
}

.item {
  width: 100%;
}

.item-container-recommended {
  padding: 0 15px;
}

.property {
  width: 20px;
  height: 20px;
  margin-right: 5px;
}

.item-properties-recommended p {
  margin-right: 10px;
}

.item-recommended {
  background-color: #ffffff;
  margin-top: 30px;
  border-radius: 8px;
  width: 100%;
  cursor: pointer;
}

.item-recommended-dark {
  background-color: #4a4e51;
}

.item-recommended,
.item-properties-recommended,
.item-title {
  display: flex;
  align-items: center;
}

.item-img-recommended {
  width: 100px;
  height: 100px;
  background-size: cover;
  border-radius: 5px;
  margin-left: 10px;
}

.recommended {
  padding-left: 60px;
  width: 100%;
  margin-top: 50px;
}

.item-title h5 {
  font-size: 14px;
  font-family: "Montserrat";
  color: black;
  font-weight: 700;
  margin-bottom: 10px;
  margin-top: 15px;
  cursor: pointer;
}

.item-price {
  color: #454647;
  font-weight: 600;
  font-family: "Open Sans";
  margin-bottom: 10px;
  font-size: 14px;
}

.item-price-dark {
  color: white;
}

.item-address,
.item-properties-recommended {
  font-size: 13px;
  font-family: "Open Sans";
  color: #4a4b4c;
  font-weight: 500;
}

@media (max-width: 915px) {
  .item-img {
    width: 100%;
  }

  .recommended {
    margin-bottom: 80px;
    padding: 0px 15px;
    padding-left: 30px;
  }

  .title {
    font-size: 18px;
  }

  .item-address,
  .item-properties-recommended,
  .item-price {
    font-size: 11px;
  }
}
</style>
