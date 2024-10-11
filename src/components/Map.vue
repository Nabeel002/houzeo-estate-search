<template>
    <div id="map"></div>
</template>

<script setup>
import "dotenv";
import { onMounted, ref } from "vue";
import { Loader } from "@googlemaps/js-api-loader";
import markerIcon from "../assets/map-marker.svg";
// Reference for the map object
const map = ref(null);

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

            const markers = [
                { position: { lat: 40.7128, lng: -74.0060 }, title: "New York" },
                { position: { lat: 34.0522, lng: -118.2437 }, title: "Los Angeles" },
                { position: { lat: 41.8781, lng: -87.6298 }, title: "Chicago" },
            ];

            const infoWindow = new InfoWindow();

            markers.forEach(({ position, title }) => {
                const marker = new Marker({
                    map: map.value,
                    position: position,
                    title: title,
                    icon: {
                        url: markerIcon,
                        size: new Size(38, 31),
                    },
                });

             
                marker.addListener("mouseover", () => {
                    infoWindow.setContent(title);
                    infoWindow.open(map.value, marker);
                });

            });
        } else {
            console.error("Google Maps API not loaded");
        }
    });
});
</script>

<style scoped>
#map {
    width: 100%;
    height: 100vh;
}

:deep(.gm-ui-hover-effect){
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
            height:auto !important;
            border: 0px !important;
            outline:0px !important; 
            display: none !important;
}
</style>
