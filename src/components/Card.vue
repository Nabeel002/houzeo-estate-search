<template>
    <div class="card">
        <swiper class="mySwiper" :slidesPerView="1" :pagination="{ clickable: true }" :navigation="true"
            :modules="[Pagination, Navigation]">
            <swiper-slide v-for="(img, index) in image" :key="index" class="image-wrapper">
                <img :src="img.src" alt="" class="image-max-cover" />
            </swiper-slide>
        </swiper>
        <div class="content-wrapper">
            <div>
                <div class="marker-pill">
                    <img src="../assets/green-marker.svg" alt="" />
                    <span>House For Sale</span>
                </div>
                <div class="view-counts">
                    <span class="marker-pill">
                        <img src="../assets/eye.svg" alt="" />
                        {{ viewCount }}K
                    </span>
                </div>
            </div>
            <div class="price-wrapper">
                <span class="price">${{ formatPrice(price) }}</span>
                <div class="area-info">
                    <span>{{ beds }} Beds</span>
                    <span>{{ baths }} Baths</span>
                    <span>
                        <span class="square-feet">{{ squareFeet }}</span>
                        Sqft.
                    </span>
                </div>
            </div>
            <div class="main-description">
                <span id="address" v-html="formattedAddress"></span> <br />
                {{ description }}
            </div>
        </div>

        <div class="counts-button">
            6 days on houzeo
        </div>

        <div class="heart" @click="togglePulsate" :class="{ heartFill }">
            <svg id="heart" width="24" height="25" viewBox="0 0 24 25" fill="none" xmlns="http://www.w3.org/2000/svg"
                :class="{ pulsate }">
                <path
                    d="M7 3.96143C4.239 3.96143 2 6.17743 2 8.91143C2 11.1184 2.875 16.3564 11.488 21.6514C11.6423 21.7453 11.8194 21.795 12 21.795C12.1806 21.795 12.3577 21.7453 12.512 21.6514C21.125 16.3564 22 11.1184 22 8.91143C22 6.17743 19.761 3.96143 17 3.96143C14.239 3.96143 12 6.96143 12 6.96143C12 6.96143 9.761 3.96143 7 3.96143Z"
                    fill="currentColor" fill-opacity="0.7" stroke="white" stroke-width="2" stroke-linecap="round"
                    stroke-linejoin="round" />
            </svg>
        </div>
    </div>
</template>

<script setup>
const formatPrice = (value) => {
    return value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
};

const props = defineProps({
    image: {
        type: Array,
        required: true
    },
    viewCount: {
        type: Number,
        required: true
    },
    price: {
        type: Number,
        required: true
    },
    description: {
        type: String,
        required: true
    },
    beds: {
        type: Number,
        required: true
    },
    baths: {
        type: Number,
        required: true
    },
    address: {
        type: String,
        required: true
    },
    days: {
        type: Number,
        required: true
    },
    squareFeet: {
        type: Number,
        required: true
    }
});

import { Swiper, SwiperSlide } from 'swiper/vue';
import { Navigation, Pagination } from 'swiper/modules';
import { onMounted, ref, computed } from 'vue';
import 'swiper/css';
import 'swiper/css/pagination';
import 'swiper/css/navigation';

const pulsate = ref(false);
const heartFill = ref(false);

const togglePulsate = () => {
    pulsate.value = !pulsate.value;
    heartFill.value = !heartFill.value;
};

const formattedAddress = computed(() => {
    const words = props.address.split(' ');
    const firstFourWords = words.slice(0, 4).join(' ');
    const remainingWords = words.slice(4).join(' ');
    return `<span style="color:black; font-weight:500;">${firstFourWords}</span> ${remainingWords}`;
});
</script>
<style lang="scss" scoped>
@import '../assets/stylesheets/styles.scss';

@mixin overlayButtons {
    position: absolute;
    top: 19.5px;
    z-index: 6;
    left: 24px;
    background-color: #FFF;
    border-radius: 22px;
    font-size: 12px;
    padding-left: 7px;
    padding-right: 7px;
}
.main-description{
    max-width: 43ch;
}
.card {
    box-shadow: 0px 0px 20px 0px #00000033;
    height: fit-content;
    width: 100%;
    border-radius: 16px;
    position: relative;
    margin-left: 10px;
    transition: box-shadow 0.5s ease-in-out;
    cursor: pointer;

    &:hover {
    box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
    }

    .image-wrapper {
        height: 200px;
        overflow: hidden;
        border-top-right-radius: 12px;
        border-top-left-radius: 12px;

        img {
            width: 100%;
            height: 100%;
        }
    }

    .area-info {
        gap: 12px;

        span {
            font-size: 12px;
        }

        span:first-letter {
            color: #0B5AA5;
            font-weight: 600;
        }

        .square-feet {
            color: #0B5AA5;
            font-weight: 600;
            margin-right: 4px;
        }
    }

    .marker-pill {
        border: 1px solid #0000001A;
        border-radius: 25px;
        padding-right: 8px;
        padding-left: 8px;
    }

    .marker-pill,
    .view-counts {
        font-size: 12px;
        display: flex;
        gap: 3px;
        align-items: center;
    }

    .content-wrapper {
        div {
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
        }
    }

    .price-wrapper {
        margin-top: 13px;
    }

    .price {
        color: #0B5AA5;
        font-weight: 600;
    }

    .content-wrapper {
        padding: 12px;
    }

    .main-description {
        color: #00000080;
        font-size: 12px;
        margin-top: 8px;
    }
}

.swiper-slide {
    width: 100% !important;
}

.counts-button {
    @include overlayButtons();

}

.heart {
    position: absolute;
    top: 19.5px;
    right: 24px;
    left: unset;
    z-index: 6;

    svg {
        cursor: pointer;
        transition: all 0.5s ease-in-out;

        &:hover {
            color: red;
        }

    }
}



.heart:hover {
    animation: pulse 0.6s forwards;

}

.heartFill {
    color: red;
}

.pulsate {
    animation: pulse 0.6s forwards;
}

@keyframes pulse {
    0% {
        transform: scale(1);
        fill: #222222;
    }

    50% {
        transform: scale(1.2);
        color: red;
    }

    100% {
        transform: scale(1);
        fill: #222222;
       
    }
}

@media screen and (max-width: 1025px) {
    .card {
        margin-left: unset;
    }
}

@media screen and (max-width: 768px) {}
</style>
