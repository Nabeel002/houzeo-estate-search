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
    if (dropBtn.value && !dropBtn.value.contains(event.target)) {
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
                <label>
                    <input type="checkbox" value="Option 2" :checked="isChecked" />
                    All
                </label>
                <label>
                    <input type="checkbox" value="Option 3" />
                    Single Family
                </label>
                <label>
                    <input type="checkbox" value="Option 2" />
                    Multi-Family
                </label>
                <label>
                    <input type="checkbox" value="Option 3" />
                    TownHouses
                </label>
                <label>
                    <input type="checkbox" value="Option 2" />
                    Condos
                </label>
                <label>
                    <input type="checkbox" value="Option 3" />
                    Lands/Lots
                </label>
                <label>
                    <input type="checkbox" value="Option 2" />
                    Manfactured Mobile Home
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

label {
    margin-bottom: 5px;
    max-width: 100%;
    padding: 5px;
    width: 100%;
}

@media screen and (max-width:650px) {
    #dropdown-wrapper{
        display: none;
    }
    
}
</style>