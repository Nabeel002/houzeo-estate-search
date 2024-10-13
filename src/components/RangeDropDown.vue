<script setup>
const props = defineProps({
    title: {
        type: String
    }
})
import { ref, onMounted, onBeforeUnmount } from 'vue';

const isOpen = ref(false);
const dropBtn = ref(null);
const isChecked = ref(false);
const minPrice = ref(500);
const maxPrice = ref(1000000);

const toggleDropDown = () => {
    isOpen.value = !isOpen.value;
};

const handleClickOutside = (event) => {
    if (dropBtn.value && !dropBtn.value.contains(event.target) && !event.target.closest('.dropdown-content')) {
        isOpen.value = false;
    }
};

onMounted(() => {
    dropBtn.value.focus();
    isChecked.value = !isChecked.value;
    document.addEventListener('click', handleClickOutside);
});

onBeforeUnmount(() => {
    document.removeEventListener('click', handleClickOutside);
});

</script>

<template>
    <div id="dropdown-wrapper">
        <div class="inner-wrapper-dropdown" ref="dropBtn" tabindex="0" @click="toggleDropDown">
            <span>{{ title }}</span>
            <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M2.72914 5.5L8 10.5L13.2709 5.5H2.72914Z" fill="currentColor" />
            </svg>
        </div>
        <div id="dropdown-content" :class="['dropdown-content', isOpen ? 'open' : '']">
            <div>
                <h2>Price Range</h2>
                <div>
                    <label for="minPrice">Min Price: ${{ minPrice }}</label>
                    <input type="range" min="1" max="10000" value="50" class="slider" id="myRange" v-model="minPrice">

                </div>
                <div>
                    <label for="maxPrice">Max Price: ${{ maxPrice }}</label>
                    <input type="range" min="500" max="10000" value="50" class="slider" id="myRange" v-model="maxPrice">
                </div>
                <div>
                    <p>Selected Price Range: ${{ minPrice }} - ${{ maxPrice }}</p>
                </div>
            </div>

            <div class="submitWrapper">
                <button class="dropdown-button" @click="toggleDropDown">Done</button>
            </div>
        </div>
    </div>
</template>
<style lang="scss" scoped>
@import '../assets/stylesheets/styles.scss';

#dropdown-wrapper {
    position: relative;
    display: inline-block;
}

.submitWrapper {
    background: #185a9d;
    line-height: 0;
    margin: 10px -10px 0;
    padding: 10px;
    text-align: right;
}

.dropdown-button {
    background: #fff;
    color: #185a9d;
    cursor: pointer;
    display: inline-block;
    font-size: 13px;
    line-height: normal;
    padding: 8px 13px;
    text-transform: uppercase;
    outline: none;
    border: 0px;
}

.dropdown-content:after {
    border-bottom: 7px solid rgba(34, 36, 38, .15);
    border-left: 7px solid transparent;
    border-right: 7px solid transparent;
    bottom: 100%;
    content: "";
    height: 0;
    left: 20px;
    position: absolute;
    width: 0;

}

.inner-wrapper-dropdown {
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: space-between;
    background-color: #f0f0f0;
    padding: 10px;
    border-radius: 4px;
    border: 1px solid #ccc;
}

.inner-wrapper-dropdown svg {
    transition: transform 0.3s ease;
}

.inner-wrapper-dropdown.open svg {
    transform: rotate(180deg);
}

#dropdown-content {
    position: absolute;
    top: 112%;
    left: 0;
    background-color: white;
    border: 1px solid #ccc;
    padding: 10px 10px 0px 10px;
    border-radius: 4px;
    display: none;
    width: 22vw;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    transition: opacity 0.3s ease, visibility 0.3s ease;
}

#dropdown-content label {
    display: block;
    margin-bottom: 5px;
}

.dropdown-content.open {
    display: block !important;
    opacity: 1 !important;
    visibility: visible !important;
}
input[type="range"]{
    accent-color: #0B5AA5;
    height: 3px;
}
input[type="range"] {
    width: 100%;
}
@media screen and (max-width:650px) {
    #dropdown-content {
        position: absolute;
        top: 112%;
        left: -12px;
        background-color: white;
        border: 1px solid #ccc;
        padding: 10px 10px 0px 10px;
        border-radius: 4px;
        display: none;
        width: 84vw;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        transition: opacity 0.3s ease, visibility 0.3s ease;
        right: 0px;
        transform: translateX(-35%);
    }
.dropdown-content:after{
    left: 50%;
}

input[type="range"]{
    width: 100%;
}
}

@media screen and (max-width:312px) {
    #dropdown-content{
        left: -24px;
    }

    
}
</style>