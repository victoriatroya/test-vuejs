<script setup>
import { reactive, onMounted, ref } from "vue";
import SelectInput from "./components/SelectInput.vue";

const searchValue = ref("");

const dataObj = reactive({
    selectedValue: null,
    dataList: null,
    visible: false,
    notFoundMessage: "No items were found.",
});

const toggleDropdown = () => {
    dataObj.visible = !dataObj.visible;
};

const optionSelected = (option) => {
    dataObj.selectedValue = option;
};

const filterOptions = (searchValue) => {
    return searchValue
        ? dataObj.dataList.fruits.filter((option) =>
              option.toLowerCase().includes(searchValue.toLowerCase())
          )
        : dataObj.dataList.fruits;
};

onMounted(async () => {
    const { data } = await fetch("http://127.0.0.1:8888/api/fruits").then(
        (data) => data.json()
    );
    dataObj.dataList = data;
});
</script>

<template>
    <div v-if="dataObj.dataList">
        <SelectInput
            :input-value="searchValue"
            :data-list="dataObj.dataList"
            :toggle-dropdown="toggleDropdown"
            :option-selected="optionSelected"
            :visible="dataObj.visible"
            :filter-options="filterOptions"
            :selected-value="dataObj.selectedValue"
            :not-found-message="dataObj.notFoundMessage"
        />
    </div>
</template>

<style>
body {
    background-color: #e5e5e5;
}
</style>
