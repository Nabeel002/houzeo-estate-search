<script setup>
import Navbar from './components/Navbar.vue'
import DropDown from './components/DropDown.vue'
import RangeDropDown from './components/RangeDropDown.vue'
import BedBathDropdown from './components/BedBathDropdown.vue'
import PropertyType from './components/PropertyType.vue'
import Card from './components/Card.vue'
import Map from './components/Map.vue'
import { ref, onMounted } from 'vue'
import DropdownFilters from './components/DropdownFilters.vue'

const transformClass = ref("transform-0")
const showMapToggle = ref(false)
const filteredHouses = ref([])
const searchInput = ref(null)
const searchQuery = ref("")
const mapText = ref("Map")
const searchResultText = ref("Austin, TX real estate & homes for sale")
const houses = ref([
  {
    image: [
      { src: '/assets/house1.png' },
      { src: '/assets/house2.png' }
    ],
    viewCount: 2.3,
    price: 3349000,
    beds: 4,
    baths: 3,
    squareFeet: 998,
    address: '2856 Meadow Park Ave, Henderson, NV 89052',
    description: 'Nashville (Real Tracs Mid) MLS-TN as distributed by MLS GRID',
    status: "sale"
  },
  {
    image: [
      { src: '/assets/house1.png' },
      { src: '/assets/house2.png' }
    ],
    viewCount: 2.3,
    price: 3349000,
    beds: 4,
    baths: 3,
    squareFeet: 998,
    address: '2856 Meadow Park Ave, Henderson, NV 89052',
    description: 'Nashville (Real Tracs Mid) MLS-TN as distributed by MLS GRID',
    status: "sold"
  },
  {
    image: [
      { src: '/assets/house1.png' },
      { src: '/assets/house2.png' }
    ],
    viewCount: 2.3,
    price: 3349000,
    beds: 4,
    baths: 3,
    squareFeet: 998,
    address: '2856 Meadow Park Ave, Henderson, NV 89052',
    description: 'Nashville (Real Tracs Mid) MLS-TN as distributed by MLS GRID',
    status: "sale"
  },
  {
    image: [
      { src: '/assets/house1.png' },
      { src: '/assets/house2.png' }
    ],
    viewCount: 2.3,
    price: 3349000,
    beds: 4,
    baths: 3,
    squareFeet: 998,
    address: '2856 Meadow Park Ave, Henderson, NV 89052',
    description: 'Nashville (Real Tracs Mid) MLS-TN as distributed by MLS GRID',
    status: 'sale',
  },
  {
    image: [
      { src: '/assets/house1.png' },
      { src: '/assets/house2.png' }
    ],
    viewCount: 2.3,
    price: 3349000,
    beds: 4,
    baths: 3,
    squareFeet: 998,
    address: '2856 Meadow Park Ave, Henderson, NV 89052',
    description: 'Nashville (Real Tracs Mid) MLS-TN as distributed by MLS GRID',
    status: 'sale',
  },
  {
    image: [
      { src: '/assets/house1.png' },
      { src: '/assets/house2.png' }
    ],
    viewCount: 2.3,
    price: 3349000,
    beds: 4,
    baths: 3,
    squareFeet: 998,
    address: '174 Abia Martin Drive',
    description: 'Nashville (Real Tracs Mid) MLS-TN as distributed by MLS GRID',
    status: 'sold',
  },

]);
const housesCount = ref(houses.value.length)



const clearSearch = () => {
  searchQuery.value = "";
  searchInput.value.focus();
  filteredHouses.value = houses.value;
  searchResultText.value = "Austin, TX real estate & homes for sale";
  housesCount.value = houses.value.length
}


const submitSearch = () => {
  if (!searchQuery.value) {
    filteredHouses.value = houses.value;
    searchResultText.value = "Austin, TX real estate & homes for sale";
    return;
  }

  searchResultText.value = searchQuery.value;

  filteredHouses.value = houses.value.filter(house =>
    house.description.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
    house.address.toLowerCase().includes(searchQuery.value.toLowerCase())
  );
  housesCount.value = filteredHouses.value.length
}

onMounted(() => {
  searchInput.value.focus();
  filteredHouses.value = houses.value;
});

const handleFilterChange = (filter) => {
  filteredHouses.value = houses.value.filter(house => {
    return (filter.sale && house.status === 'sale') || (filter.sold && house.status === 'sold');
  });
  housesCount.value = filteredHouses.value.length;
};
const showMap = () => {
  mapText.value = "List View"
  showMapToggle.value = !showMapToggle.value
  if (showMapToggle.value) {
    mapText.value = "List View"
    document.body.style.overflow = 'hidden';
  } else {
    mapText.value = "Map"
    document.body.style.overflow = 'auto';
  }

}
</script>

<template>
  <a href="https://vuejs.org/" target="_blank">
    <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
  </a>
  <Navbar />
  <div class="filter-wrapper">
    <div class="input-wrapper">
      <input type="search" id="search-bar" v-model="searchQuery" ref="searchInput"
        placeholder="Search by city, state, or zip" />
      <button class="cross-button" v-if="searchQuery" @click="clearSearch">
        <img src="./assets/crosshair.svg" alt="Clear search" />
      </button>
      <button class="cross-button search-input" @click="submitSearch">
        <img src="./assets/search-icon.svg" alt="Search" />
      </button>

    </div>
    <div class="mobile-filter-wrapper">
      <svg width="38" height="38" viewBox="0 0 38 38" fill="none" xmlns="http://www.w3.org/2000/svg">
        <rect x="0.5" y="0.497559" width="37" height="37.0049" rx="18.5" stroke="#0B5AA5" />
        <path
          d="M16 12C15.7348 12 15.4804 12.1054 15.2929 12.2929C15.1054 12.4804 15 12.7348 15 13C15 13.2652 15.1054 13.5196 15.2929 13.7071C15.4804 13.8947 15.7348 14 16 14C16.2652 14 16.5196 13.8947 16.7071 13.7071C16.8946 13.5196 17 13.2652 17 13C17 12.7348 16.8946 12.4804 16.7071 12.2929C16.5196 12.1054 16.2652 12 16 12ZM13.17 12C13.3766 11.4145 13.7597 10.9074 14.2666 10.5488C14.7735 10.1902 15.3791 9.99756 16 9.99756C16.6209 9.99756 17.2265 10.1902 17.7334 10.5488C18.2403 10.9074 18.6234 11.4145 18.83 12H26C26.2652 12 26.5196 12.1054 26.7071 12.2929C26.8946 12.4804 27 12.7348 27 13C27 13.2652 26.8946 13.5196 26.7071 13.7071C26.5196 13.8947 26.2652 14 26 14H18.83C18.6234 14.5855 18.2403 15.0926 17.7334 15.4512C17.2265 15.8099 16.6209 16.0025 16 16.0025C15.3791 16.0025 14.7735 15.8099 14.2666 15.4512C13.7597 15.0926 13.3766 14.5855 13.17 14H12C11.7348 14 11.4804 13.8947 11.2929 13.7071C11.1054 13.5196 11 13.2652 11 13C11 12.7348 11.1054 12.4804 11.2929 12.2929C11.4804 12.1054 11.7348 12 12 12H13.17ZM22 18C21.7348 18 21.4804 18.1054 21.2929 18.2929C21.1054 18.4804 21 18.7348 21 19C21 19.2652 21.1054 19.5196 21.2929 19.7071C21.4804 19.8947 21.7348 20 22 20C22.2652 20 22.5196 19.8947 22.7071 19.7071C22.8946 19.5196 23 19.2652 23 19C23 18.7348 22.8946 18.4804 22.7071 18.2929C22.5196 18.1054 22.2652 18 22 18ZM19.17 18C19.3766 17.4145 19.7597 16.9074 20.2666 16.5488C20.7735 16.1902 21.3791 15.9976 22 15.9976C22.6209 15.9976 23.2265 16.1902 23.7334 16.5488C24.2403 16.9074 24.6234 17.4145 24.83 18H26C26.2652 18 26.5196 18.1054 26.7071 18.2929C26.8946 18.4804 27 18.7348 27 19C27 19.2652 26.8946 19.5196 26.7071 19.7071C26.5196 19.8947 26.2652 20 26 20H24.83C24.6234 20.5855 24.2403 21.0926 23.7334 21.4512C23.2265 21.8099 22.6209 22.0025 22 22.0025C21.3791 22.0025 20.7735 21.8099 20.2666 21.4512C19.7597 21.0926 19.3766 20.5855 19.17 20H12C11.7348 20 11.4804 19.8947 11.2929 19.7071C11.1054 19.5196 11 19.2652 11 19C11 18.7348 11.1054 18.4804 11.2929 18.2929C11.4804 18.1054 11.7348 18 12 18H19.17ZM16 24C15.7348 24 15.4804 24.1054 15.2929 24.2929C15.1054 24.4804 15 24.7348 15 25C15 25.2652 15.1054 25.5196 15.2929 25.7071C15.4804 25.8947 15.7348 26 16 26C16.2652 26 16.5196 25.8947 16.7071 25.7071C16.8946 25.5196 17 25.2652 17 25C17 24.7348 16.8946 24.4804 16.7071 24.2929C16.5196 24.1054 16.2652 24 16 24ZM13.17 24C13.3766 23.4145 13.7597 22.9074 14.2666 22.5488C14.7735 22.1902 15.3791 21.9976 16 21.9976C16.6209 21.9976 17.2265 22.1902 17.7334 22.5488C18.2403 22.9074 18.6234 23.4145 18.83 24H26C26.2652 24 26.5196 24.1054 26.7071 24.2929C26.8946 24.4804 27 24.7348 27 25C27 25.2652 26.8946 25.5196 26.7071 25.7071C26.5196 25.8947 26.2652 26 26 26H18.83C18.6234 26.5855 18.2403 27.0926 17.7334 27.4512C17.2265 27.8099 16.6209 28.0025 16 28.0025C15.3791 28.0025 14.7735 27.8099 14.2666 27.4512C13.7597 27.0926 13.3766 26.5855 13.17 26H12C11.7348 26 11.4804 25.8947 11.2929 25.7071C11.1054 25.5196 11 25.2652 11 25C11 24.7348 11.1054 24.4804 11.2929 24.2929C11.4804 24.1054 11.7348 24 12 24H13.17Z"
          fill="#0B5AA5" />
      </svg>
    </div>

    <DropDown title="For Sale" :onFilterChange="handleFilterChange" />
    <RangeDropDown title="Price" :onFilterChange="handleFilterChange" />
    <BedBathDropdown title="Bed & Bath" :onFilterChange="handleFilterChange" />
    <PropertyType title="Property Type" :onFilterChange="handleFilterChange" />
    <DropdownFilters title="Filters" />
    <button class="desktopSave">
      <svg width="13" height="12" viewBox="0 0 13 12" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path
          d="M0.5 12V9.16667L9.3 0.383333C9.43333 0.261111 9.58067 0.166667 9.742 0.1C9.90333 0.0333334 10.0727 0 10.25 0C10.4278 0 10.6 0.0333334 10.7667 0.1C10.9333 0.166667 11.0778 0.266667 11.2 0.4L12.1167 1.33333C12.25 1.45556 12.3473 1.6 12.4087 1.76667C12.47 1.93333 12.5004 2.1 12.5 2.26667C12.5 2.44444 12.4696 2.614 12.4087 2.77533C12.3478 2.93667 12.2504 3.08378 12.1167 3.21667L3.33333 12H0.5ZM10.2333 3.2L11.1667 2.26667L10.2333 1.33333L9.3 2.26667L10.2333 3.2Z"
          fill="black" />
      </svg>
      Saved
    </button>
    <button class="mobile-only-btn">Save Search</button>

  </div>

  <div class="layout-wrapper">
    <div :class="['transform-0', showMapToggle ? 'active' : '']">
      <Map :display="showMapToggle" />
    </div>
    <div class="grid-wrapper">
      <h2 class="searchResultText">{{ searchResultText }}</h2>
      <p class="housesCount">{{ housesCount }} Home</p>
      <div class="card-wrapper">

        <Card v-for="(house, index) in filteredHouses" :key="index" :image="house.image"
          :description="house.description" :beds="house.beds" :baths="house.baths" :address="house.address"
          :price="house.price" :viewCount="house.viewCount" :squareFeet="house.squareFeet" />
      </div>
    </div>
  </div>

  <button class="tablet-map-button" @click="showMap">
    {{ mapText }}
    <svg width="21" height="20" viewBox="0 0 21 20" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path
        d="M8.09998 5.62501V12.5M13.1 7.50001V14.375M13.5191 17.2908L17.5816 15.2592C17.8991 15.1008 18.1 14.7758 18.1 14.4208V4.01668C18.1 3.32001 17.3666 2.86668 16.7433 3.17834L13.5191 4.79001C13.3891 4.85538 13.2455 4.88943 13.1 4.88943C12.9544 4.88943 12.8109 4.85538 12.6808 4.79001L8.51914 2.71001C8.38899 2.64495 8.24548 2.61108 8.09998 2.61108C7.95447 2.61108 7.81096 2.64495 7.68081 2.71001L3.61831 4.74084C3.4626 4.81868 3.33163 4.93833 3.24008 5.0864C3.14853 5.23446 3.10002 5.40509 3.09998 5.57918V15.9833C3.09998 16.68 3.83331 17.1333 4.45664 16.8217L7.68081 15.21C7.81087 15.1446 7.95441 15.1106 8.09998 15.1106C8.24554 15.1106 8.38908 15.1446 8.51914 15.21L12.6808 17.2908C12.945 17.4225 13.2558 17.4225 13.5191 17.2908Z"
        stroke="white" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" />
    </svg>
  </button>
</template>

<style scoped>
@import './assets/stylesheets/styles.scss';

.layout-wrapper {
  display: flex;
  gap: 25px;
  padding-right: 24px;
  height: 100vh;
}

.transform-0 {
  position: fixed;
  top: 158px;
  width: 51%;
  transition: transform 0.5s ease-in-out;
}

.searchResultText {
  position: absolute;
  top: 16px;
  font-weight: 600;
  font-size: 18px;
}

.housesCount {
  position: absolute;
  top: 49px;
  font-weight: 500;
  font-size: 14px;
  color: #00000066;
}

.card-wrapper {
  display: grid;
  gap: 25px;
  flex-wrap: wrap;
  grid-template-columns: repeat(2, 1fr);
  overflow-y: scroll;
  -webkit-overflow-scrolling: touch;
  scrollbar-width: none;
  -ms-overflow-style: none;
  padding-right: 25px;
  padding-top: 111px;
  padding-bottom: 50px;

}

.grid-wrapper {
  position: absolute;
  right: 28px;
  width: 44%;
  top: 143px;

}

.tablet-map-button {
  bottom: 30px;
  left: 50%;
  position: fixed;
  transform: translateX(-50%);
  z-index: 9999;
  background-color: #0c5aa5;
  border-radius: 4px;
  box-shadow: 0 0 7px 1px rgba(0, 0, 0, .25);
  color: #fff;
  padding: 13px 25px;
  border: none;
  display: flex;
  align-items: center;
  gap: 12px;
  font-weight: 500;
  cursor: pointer;
}

.tablet-map-button {
  display: none;
}

.filter-wrapper {
  flex-wrap: wrap;
}

.desktopSave {
  border-radius: 35px;
  background-color: transparent;
  border: 1px solid #00000033;
  width: fit-content;
  font-weight: 500;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor:pointer;
  gap: 1rem;
  padding: 15px;
  padding-right: 25px;
  padding-left: 28px;
  font-size: 14px;
  font-family: 'Poppins';
}

@media screen and (max-width:1180px) {
  .transform-0 {
    top: 237px;
  }

  .card-wrapper {
    top: 245px;
  }

}

.active {
  transform: translateX(0%) !important;
  width: 100% !important;
  z-index: 999;
  margin-left: -24px;

  #map {
    width: 100%;
    height: 100vh;
  }
}

@media screen and (max-width:1352px) {
  .transform-0 {
    width: 49%;
  }

}

@media screen and (max-width: 1025px) {
  .tablet-map-button {
    display: flex;
  }

  .transform-0 {
    transform: translateX(-200%);
    position: absolute;
  }

  .grid-wrapper {
    position: static;
    width: 100%;
    padding-right: 23px;
    margin-top: 250px;
  }

  .card-wrapper {
    padding: unset;
  }

  .layout-wrapper {
    margin: 0 auto;
    display: table;
    padding-right: 24px;
    padding-left: 24px;
  }
}


@media screen and (max-width:580px) {
  .card-wrapper {
    display: block;

    .card {
      margin-bottom: 25px;
    }
  }


}
</style>
