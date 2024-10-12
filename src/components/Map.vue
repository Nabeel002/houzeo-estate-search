<template>
    <div id="map"></div>
</template>

<script setup>
import "dotenv";
import { onMounted, ref, defineExpose } from "vue";
import { Loader } from "@googlemaps/js-api-loader";
import markerIcon from "../assets/map-marker.svg";

const map = ref(null);
const markers = ref([]);
const infoWindow = ref(null);

onMounted(() => {
    const loader = new Loader({
        apiKey: import.meta.env.VITE_GOOGLE_MAP_API,
        version: "weekly",
    });

    loader.load().then(() => {
        if (window.google) {
            const { Map, Marker, Size, InfoWindow } = google.maps;

            map.value = new Map(document.getElementById("map"), {
                center: { lat: 37.0902, lng: -95.7129 },
                zoom: 4,
            });

            infoWindow.value = new InfoWindow();

            const markerData = [
                { id: 1, position: { lat: 35.9963, lng: -115.0776 }, title: "Las Vegas" },
                { id: 2, position: { lat: 34.0522, lng: -118.2437 }, title: "Los Angeles" },
                { id: 3, position: { lat: 41.8781, lng: -87.6298 }, title: "Chicago" },
            ];

            markerData.forEach(({ id, position, title }) => {
                const marker = new Marker({
                    map: map.value,
                    position: position,
                    title: title,
                    icon: {
                        url: markerIcon,
                        size: new Size(38, 31),
                    },
                });

                marker.id = id;
                markers.value.push(marker);

                marker.addListener("mouseover", () => {
                    openInfoWindow(marker);
                });
                marker.addListener("click", () => {
                    openInfoWindow(marker);})
                marker.addListener("mouseout", () => {
                    closeInfoWindow();
                });
                
            });
        } else {
            console.error("Google Maps API not loaded");
        }
    });
});

const openInfoWindow = (marker) => {
    if (infoWindow.value) {
        infoWindow.value.setContent(marker.title);
        infoWindow.value.open(map.value, marker);
    }
};
const closeInfoWindow = (marker) => {
    infoWindow.value.close();
};
defineExpose({
    openInfoWindow,
    markers,
});
</script>

<style scoped>
#map {
    width: 100%;
    height: 100vh;
}

:deep(.gm-ui-hover-effect) {
    background: white !important;
    display: block;
    border: 0px;
    margin: 0px;
    padding: 0px;
    text-transform: none;
    appearance: none;
    position: relative;
    cursor: pointer;
    user-select: none;
    width: fit-content !important;
    height: auto !important;
    border: 0px !important;
    outline: 0px !important;
    display: none !important;
}
</style>
