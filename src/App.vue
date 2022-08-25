<script setup>
import {reactive} from "vue";
import SelectInput from "./components/SelectInput.vue";

const data = reactive({
    selected: "Select an item",
    options: [
        { text: "One", value: "A" },
        { text: "Two", value: "B" },
        { text: "Three", value: "C" },
    ],
    visible: false
});

const toggleDropdown = () => {
    data.visible = !data.visible;
};

const optionSelected = (option) => {
    data.selected = option;
};

</script>

<template>
    <SelectInput
        :value="data.selected"
        :options-list="data.options"
        :toggle-dropdown="toggleDropdown"
        :option-selected="optionSelected"
        :visible="data.visible"
    />
</template>

<style>
body {
    background-color: #e5e5e5;
}
</style>
