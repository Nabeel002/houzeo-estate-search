<template>
    <div class="card" @mouseover="mouseEvent">
        <swiper class="mySwiper" :slidesPerView="1" :pagination="{ clickable: true }" :navigation="true"
            :modules="[Pagination, Navigation]">
            <swiper-slide v-for="(img, index) in image" :key="index" class="image-wrapper">
                <img :src="img.src" alt="" class="image-max-cover" />
            </swiper-slide>
        </swiper>
        <div class="content-wrapper">
            <div>
                <div class="marker-pill pill-shape">
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

        <div id="heart" class="heart" @click="togglePulsate">
            <svg x="50" y="50" width="200" height="200" viewBox="0 0 20 20">
                <path
                    d="M8.612,2.347L8,2.997l-0.612-0.65c-1.69-1.795-4.43-1.795-6.12,0c-1.69,1.795-1.69,4.706,0,6.502l0.612,0.65L8,16l6.12-6.502l0.612-0.65c1.69-1.795,1.69-4.706,0-6.502C13.042,0.551,10.302,0.551,8.612,2.347z"
                    fill="none" stroke="white" stroke-width="3.5" transform="scale(0.954929658551372)"></path>

                <svg :class="['heart', heartFill ? 'heartFill' : '']" id="heart-svg" preserveAspectRatio="xMidYMid meet"
                    viewbox="0 0 20 20">
                    <use xlink:href="#shape" class="pulsate" />
                    <path id="shape"
                        d="M8.612,2.347L8,2.997l-0.612-0.65c-1.69-1.795-4.43-1.795-6.12,0c-1.69,1.795-1.69,4.706,0,6.502l0.612,0.65L8,16  l6.12-6.502l0.612-0.65c1.69-1.795,1.69-4.706,0-6.502C13.042,0.551,10.302,0.551,8.612,2.347z"
                        fill="currentColor" transform="scale( 0.954929658551372 )">
                    </path>
                </svg>
            </svg>


        </div>
    </div>
</template>

<script setup>
const formatPrice = (value) => {
    return value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
};

const props = defineProps({
    id: {
        type: Number,
        required: true
    },
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
const emit = defineEmits(["mouseEvent"]);

const mouseEvent = () => {
    emit("mouseEvent", props.id);
};
import { Swiper, SwiperSlide } from 'swiper/vue';
import { Navigation, Pagination } from 'swiper/modules';
import { onMounted, ref, computed } from 'vue';
import 'swiper/css';
import 'swiper/css/pagination';
import 'swiper/css/navigation';

const pulsate = ref(false);
const heartFill = ref(false);
const togglePulsate = () => {
    heartFill.value = !heartFill.value; 
    if (heartFill.value) {
        pulsate.value = true; 
    } else {
        pulsate.value = false; 
    }
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

#heart-svg {
    overflow: visible;
}

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
    display: block !important;
}
.main-description {
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

    svg {
        overflow: visible;
    }

    .pill-shape {
        border: 1px solid #0000001A;
        border-radius: 25px;
        padding-right: 8px;
        padding-left: 8px;
    }

    #address {
        margin-bottom: 8px;
        display: inline-block;
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
    color: #222222B2; 

    svg {
        cursor: pointer;
        transition: all 1s ease-in-out;
        width: 24px;
        height: 24px;

        &:hover {
            color: red;
        }
    }
}

.heartFill {
    color: red; 
}

.pulsate {
    stroke: red;
    opacity: 0; 
}

.heart:hover>.pulsate {
    animation: pulse 1.5s forwards;
}
use {
    stroke: red;
    opacity: 0;

}










@keyframes pulse {
    from {
        opacity: 0.5;
        stroke-width: 0;
    }

    to {
        opacity: 0;
        stroke-width: 15px;
    }
}


@media screen and (max-width: 1025px) {
    .card {
        margin-left: unset;
    }
}

@media screen and (max-width: 768px) {}
</style>
