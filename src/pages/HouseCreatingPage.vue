<template>
  <div class="body" :style="backgroundStyle">
    <div class="body-container">
      <div class="back-button">
        <BackToList :styling="black"></BackToList>
      </div>

      <form class="form" @submit.prevent="handleSubmit">
        <fieldset class="fieldset">
          <legend class="legend">
            <h1 class="title" :class="{ 'dark-text': isDarkMode }">
              {{ isEditing ? "Edit Listing" : "Create New Listing" }}
            </h1>
          </legend>
          <div class="form-group form-group-single">
            <label for="street-name" :class="{ 'dark-text': isDarkMode }"
              >Street name*</label
            >
            <input
              :class="{ 'dark-input': isDarkMode }"
              type="text"
              id="street-name"
              name="street"
              v-model="formData.street"
              placeholder="Enter the street name"
              required
            />
          </div>
          <div class="form-group-inline">
            <div class="form-group">
              <label for="house-number" :class="{ 'dark-text': isDarkMode }"
                >House number*</label
              >
              <input
                :class="{ 'dark-input': isDarkMode }"
                type="text"
                id="house-number"
                name="houseNumber"
                v-model="formData.houseNumber"
                placeholder="Enter house number"
                required
              />
            </div>
            <div class="form-group right-group-item">
              <label for="addition" :class="{ 'dark-text': isDarkMode }"
                >Addition (optional)</label
              >
              <input
                :class="{ 'dark-input': isDarkMode }"
                type="text"
                id="addition"
                name="houseNumberAddition"
                v-model="formData.houseNumberAddition"
                placeholder="e.g. A"
              />
            </div>
          </div>

          <div class="form-group form-group-single">
            <label for="postal-code" :class="{ 'dark-text': isDarkMode }"
              >Postal code*</label
            >
            <input
              :class="{ 'dark-input': isDarkMode }"
              type="text"
              id="postal-code"
              name="zip"
              v-model="formData.zip"
              placeholder="e.g.1000 AA"
              required
            />
          </div>
          <div class="form-group form-group-single">
            <label for="city" :class="{ 'dark-text': isDarkMode }">City*</label>
            <input
              :class="{ 'dark-input': isDarkMode }"
              type="text"
              id="city"
              name="city"
              v-model="formData.city"
              placeholder="e.g. Utrecht"
              required
            />
          </div>
          <Uploaded
            :imageUrl="formData.housePhoto?.url"
            @fileChange="uploadImage"
            @removeImage="removeImage"
          ></Uploaded>
          <span
            :class="{ 'dark-text': isDarkMode }"
            v-if="vuelidateResult.housePhoto.$error"
            >The image is required</span
          >

          <div class="form-group form-group-single">
            <label for="price" :class="{ 'dark-text': isDarkMode }"
              >Price*</label
            >
            <input
              :class="{ 'dark-input': isDarkMode }"
              type="number"
              id="price"
              name="price"
              v-model="formData.price"
              placeholder="e.g. €150.000"
              required
            />
          </div>
          <div class="form-group-inline">
            <div class="form-group">
              <label for="size" :class="{ 'dark-text': isDarkMode }"
                >Size*</label
              >
              <input
                :class="{ 'dark-input': isDarkMode }"
                type="number"
                id="size"
                name="size"
                v-model="formData.size"
                placeholder="e.g. 60m2"
                required
              />
            </div>
            <div class="form-group right-group-item">
              <label for="garage" :class="{ 'dark-text': isDarkMode }"
                >Garage*</label
              >
              <select
                :class="{ 'dark-input': isDarkMode, 'dark-text': isDarkMode }"
                id="garage"
                name="hasGarage"
                v-model="formData.hasGarage"
                required
              >
                <option :class="{ 'dark-text': isDarkMode }" value="">
                  Select
                </option>
                <option :class="{ 'dark-text': isDarkMode }" value="true">
                  Yes
                </option>
                <option :class="{ 'dark-text': isDarkMode }" value="false">
                  No
                </option>
              </select>
            </div>
          </div>
          <div class="form-group-inline">
            <div class="form-group">
              <label for="bedrooms" :class="{ 'dark-text': isDarkMode }"
                >Bedrooms*</label
              >
              <input
                :class="{ 'dark-input': isDarkMode }"
                type="text"
                id="bedrooms"
                name="bedrooms"
                v-model="formData.bedrooms"
                placeholder="Enter amount"
                required
              />
            </div>
            <div class="form-group right-group-item">
              <label for="bathrooms" :class="{ 'dark-text': isDarkMode }"
                >Bathrooms*</label
              >
              <input
                :class="{ 'dark-input': isDarkMode }"
                type="text"
                id="bathrooms"
                name="bathrooms"
                v-model="formData.bathrooms"
                placeholder="Enter amount"
                required
              />
            </div>
          </div>
          <div class="form-group form-group-single">
            <label for="construction-date" :class="{ 'dark-text': isDarkMode }"
              >Construction date*</label
            >
            <div class="input-wrapper">
              <input
                :class="{ 'dark-input': isDarkMode }"
                type="text"
                id="construction-date"
                name="constructionYear"
                v-model="formData.constructionYear"
                placeholder="e.g.1990"
                required
              />
              <div class="construction-year-info-container">
                <img
                  class="construction-year-info"
                  src="@/assets/icons/mobile/info-active-icon.png"
                  alt="info"
                />
                <p class="info-text">
                  The construction year should be more than 1901
                </p>
              </div>
            </div>
            <span v-if="vuelidateResult.constructionYear.$error">{{
              vuelidateResult.constructionYear.$errors
                .map((error) => error.$message)
                .join(", ")
            }}</span>
          </div>

          <div class="form-group form-group-single">
            <label for="description" :class="{ 'dark-text': isDarkMode }"
              >Description*</label
            >
            <textarea
              :class="{ 'dark-input': isDarkMode }"
              id="description"
              class="description"
              name="description"
              v-model="formData.description"
              placeholder="Enter description"
              required
            ></textarea>
          </div>
        </fieldset>
        <PostButton
          :class="{ 'dark-text': isDarkMode }"
          :isEditing="isEditing"
          :allFieldsFilled="allFieldsFilled"
        ></PostButton>
      </form>
    </div>
  </div>
</template>

<script setup>
import { computed, ref, onMounted, inject } from "vue";
import backgroundImage from "@/assets/images/create-new-property-background.png";
import { useRouter, useRoute } from "vue-router";
import BackToList from "@/components/BackToList.vue";
import Uploaded from "@/components/HouseCreatePage/Uploaded.vue";
import PostButton from "@/components/HouseCreatePage/PostButton.vue";
import useVuelidate from "@vuelidate/core";
import { helpers, minValue, numeric, required } from "@vuelidate/validators";
import { apiService } from "@/services/apiService";

const isDarkMode = inject("isDarkMode");

const black = "black";

const formData = ref({
  price: "",
  bedrooms: "",
  bathrooms: "",
  size: "",
  street: "",
  houseNumber: "",
  houseNumberAddition: "",
  zip: "",
  city: "",
  constructionYear: "",
  hasGarage: "",
  description: "",
  housePhoto: {
    file: null,
    url: null,
  },
});

// Determine if we are editing an existing item
const isEditing = ref(false);
const itemId = ref(null);

const rules = {
  constructionYear: {
    required,
    minValue: helpers.withMessage("Minimal year is 1901", minValue(1901)),
    numeric: numeric,
  },
  housePhoto: {
    url: { required },
  },
};

const vuelidateResult = useVuelidate(rules, formData);

const router = useRouter();
const route = useRoute();

onMounted(async () => {
  if (route.params.id) {
    isEditing.value = true;
    itemId.value = route.params.id;
    try {
      const response = await apiService.getHouse(itemId.value);
      const item = response.data;
      if (item && item.rooms && item.location) {
        formData.value.price = item.price;
        formData.value.bedrooms = item.rooms.bedrooms;
        formData.value.bathrooms = item.rooms.bathrooms;
        formData.value.size = item.size;
        formData.value.street = item.location.street;
        formData.value.houseNumber = item.location.houseNumber;
        formData.value.houseNumberAddition = item.location.houseNumberAddition;
        formData.value.zip = item.location.zip;
        formData.value.city = item.location.city;
        formData.value.constructionYear = item.constructionYear;
        formData.value.hasGarage = item.hasGarage;
        formData.value.description = item.description;
        formData.value.housePhoto.url = item.image;
      } else {
      }
    } catch (error) {
      alert("There was an error from API");
    }
  }
});

const isImageUploaded = computed(() => {
  const hasFile = !!formData.value.housePhoto.file;
  const hasUrl = !!formData.value.housePhoto.url;
  console.log("isImageUploaded:", hasFile || hasUrl, formData.value.housePhoto);
  return hasFile || hasUrl;
});

const allFieldsFilled = computed(() => {
  const result = !!(
    formData.value.price &&
    formData.value.bedrooms &&
    formData.value.bathrooms &&
    formData.value.size &&
    formData.value.street &&
    formData.value.houseNumber &&
    formData.value.zip &&
    formData.value.city &&
    formData.value.constructionYear &&
    formData.value.description &&
    isImageUploaded.value
  );
  console.log("allFieldsFilled:", result);
  return result;
});

const uploadImage = ({ url, file }) => {
  formData.value.housePhoto.file = file;
  formData.value.housePhoto.url = url;
};

const handleSubmit = async () => {
  vuelidateResult.value.$touch();

  if (vuelidateResult.value.$invalid) {
    return;
  }

  try {
    const payload = {
      location: {
        street: formData.value.street,
        houseNumber: formData.value.houseNumber,
        houseNumberAddition: formData.value.houseNumberAddition,
        zip: formData.value.zip,
        city: formData.value.city,
      },
      rooms: {
        bedrooms: parseInt(formData.value.bedrooms, 10),
        bathrooms: parseInt(formData.value.bathrooms, 10),
      },
      price: parseFloat(formData.value.price),
      size: parseFloat(formData.value.size),
      constructionYear: parseInt(formData.value.constructionYear, 10),
      hasGarage: formData.value.hasGarage,
      description: formData.value.description,
    };

    let response;
    if (isEditing.value) {
      response = await apiService.updateHouse(itemId.value, payload);

      if (formData.value.housePhoto.file) {
        await apiService.uploadHouseImage(
          itemId.value,
          formData.value.housePhoto.file
        );
      }
    } else {
      response = await apiService.createHouse(payload);

      const houseId = response.data.id || response.data.itemId;

      if (formData.value.housePhoto.file) {
        await apiService.uploadHouseImage(
          houseId,
          formData.value.housePhoto.file
        );
      }
    }

    router.push({ name: "HouseDetailsPage", params: { id: response.data.id } });
  } catch (error) {
    console.error("Error creating or updating house:", error);
  }
};

const removeImage = () => {
  formData.value.housePhoto.file = null;
  formData.value.housePhoto.url = null;
};

const backgroundStyle = computed(() =>
  isDarkMode.value
    ? { backgroundColor: "#2c2e30" }
    : {
        backgroundImage: `url(${backgroundImage})`,
        backgroundSize: "cover",
        backgroundPosition: "center",
        display: "flex",
        flexDirection: "column",
        alignItems: "flex-start",
      }
);
</script>

<style scoped>
.back-button {
  margin-top: 15px;
}

span {
  color: red;
}

.input-wrapper {
  position: relative;
}

.construction-year-info-container {
  position: absolute;
  top: 50%;
  left: 108%;
  transform: translateY(-50%);
  display: flex;
  align-items: center;
}

.construction-year-info {
  width: 30px;
  height: 30px;
  margin-right: 10px;
  cursor: pointer;
}

.info-text {
  display: none;
  position: absolute;
  left: 150%;
  background-color: #f6f6f6cc;
  color: #4a4b4c;
  padding: 10px;
  border-radius: 5px;
  white-space: nowrap;
}

.construction-year-info-container:hover .info-text {
  display: block;
}

.description {
  white-space: pre-wrap;
}

.form-group input {
  color: rgb(0, 0, 0);
}

.form-group-singl input {
  width: 100%;
  box-sizing: border-box;
}

.form-group select {
  width: 100%;
  box-sizing: border-box;
}

.body-container {
  display: flex;
  align-items: baseline;
  flex-direction: column;
  justify-content: center;
  margin: 30px 15%;
}

.body {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.form-group {
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: flex-start;
  margin: 10px 0px;
  width: 100%;
}

.fieldset {
  border: none;
  padding: 0px;
}

.form-group input,
textarea,
select {
  font-family: Montserrat;
  font-weight: 500;
  font-size: 14px;
  padding: 15px 20px;
  border: none;
  border-radius: 10px;
  margin: 5px 0px;
  color: #4a4b4c;
}

.form-group input:focus,
textarea:focus,
select:focus {
  border: none;
  outline: none;
}

.form-group textarea {
  width: 100%;
  box-sizing: border-box;
  resize: none;
  height: 200px;
}

.form-group input::placeholder,
textarea::placeholder {
  font-family: Montserrat;
  font-weight: 400;
  font-size: 14px;
  color: #c3c3c3;
}

.form-group label {
  font-family: Montserrat;
  font-weight: 600;
  font-size: 14px;
  color: #4a4b4c;
}

.form-group-inline {
  display: flex;
  flex-direction: row;
}

.right-group-item {
  margin-left: 20px;
}

.dark-input {
  background-color: #4a4e51 !important;
  color: white !important;
}

.dark-text {
  color: white !important;
}

@media (max-width: 880px) {
  .construction-year-info-container {
    display: none;
  }

  .body {
    margin-bottom: 50px;
  }

  .form-group input,
  textarea,
  select {
    width: 100%;
  }

  .body-container {
    margin: 0px;
    padding: 20px 15px;
    width: 100%;
  }

  .post-button button {
    width: 100%;
  }

  label.plus[data-v-d92a4f87] {
    padding: 55px;
  }

  .plus img {
    width: 30px;
    height: auto;
  }

  .title {
    font-size: 18px;
    margin: 0 auto;
  }

  .legend {
    display: flex;
    align-items: center;
    width: 100%;
    margin-bottom: 20px;
  }

  .form {
    width: 100%;
  }
}
</style>
