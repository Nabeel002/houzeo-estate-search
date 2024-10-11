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
            <h4 class="title-wrapper">Bedrooms</h4>
            <div class="bed-wrapper">
                <label class="label-button" for="option-0">
                    <input type="radio" checked class="input-radio" id="option-0" value="Any" v-model="selectedOption"
                        name="radio-options" />
                    <span class="input-span">Any</span>
                </label>
                <label class="label-button" for="option-1">
                    <input type="radio" class="input-radio" id="option-1" value="1" v-model="selectedOption"
                        name="radio-options" />
                    <span class="input-span">1</span>
                </label>
                <label class="label-button" for="option-2">
                    <input type="radio" class="input-radio" id="option-2" value="2" v-model="selectedOption"
                        name="radio-options" />
                    <span class="input-span">2</span>
                </label>
                <label class="label-button" for="option-3">
                    <input type="radio" class="input-radio" id="option-3" value="3" v-model="selectedOption"
                        name="radio-options" />
                    <span class="input-span">3</span>
                </label>
                <label class="label-button" for="option-4">
                    <input type="radio" class="input-radio" id="option-4" value="4" v-model="selectedOption"
                        name="radio-options" />
                    <span class="input-span">4</span>
                </label>
            </div>
            <h4 class="title-wrapper">Bathrooms</h4>
            <div class="bed-wrapper">

                <label class="label-button" for="option-any">
                    <input type="radio" checked class="input-radio" id="option-any" value="Any" v-model="selectedOption"
                        name="radio-options" />
                    <span class="input-span">Any</span>
                </label>
                <label class="label-button" for="option-one">
                    <input type="radio" class="input-radio" id="option-one" value="1" v-model="selectedOption"
                        name="radio-options" />
                    <span class="input-span">1</span>
                </label>
                <label class="label-button" for="option-two">
                    <input type="radio" class="input-radio" id="option-two" value="2" v-model="selectedOption"
                        name="radio-options" />
                    <span class="input-span">2</span>
                </label>
                <label class="label-button" for="option-three">
                    <input type="radio" class="input-radio" id="option-three" value="3" v-model="selectedOption"
                        name="radio-options" />
                    <span class="input-span">3</span>
                </label>
                <label class="label-button" for="option-four">
                    <input type="radio" class="input-radio" id="option-four" value="4" v-model="selectedOption"
                        name="radio-options" />
                    <span class="input-span">4</span>
                </label>
            </div>

            <div class="submitWrapper">
                <button class="dropdown-button">Done</button>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
@import '../assets/stylesheets/styles.scss';
.title-wrapper{
    margin: 10px;
}
#dropdown-wrapper {
    position: relative;
    display: inline-block;
}

.input-span {
    display: flex;
    width: 100%;
    height: 100%;
    align-items: center;
    justify-content: center;
}

.bed-wrapper {
    display: flex;
}

.label-button {
    width: 22%;
    border: 1px solid #185a9d;
    text-align: center;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

.input-radio {
    opacity: 0;
    position: absolute;
    visibility: hidden;
}

.label-button {
    display: inline-block;
    width: 22%;
    border: 1px solid #185a9d;
    text-align: center;
    height: 38px;
    cursor: pointer;
    transition: background-color 0.3s ease, color 0.3s ease;
    background-color: #fff;
    color: #000;
}

.input-radio {
    display: none;
}

.label-button input[type="radio"]:checked+span {
    background-color: #185a9d;
    color: #fff;
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
    width: 150%;
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


@media screen and (max-width:650px) {
    #dropdown-wrapper{
        display: none;
    }
    
}
</style>