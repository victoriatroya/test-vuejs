<script setup>
const props = defineProps({
    dataList: Object,
    toggleDropdown: Function,
    visible: Boolean,
    optionSelected: Function,
    filterOptions: Function,
    selectedValue: String,
    notFoundMessage: String,
    showValue: Boolean,
    modelValue: String
});
</script>

<template>
    <div class="wrapper-input">
        <div
            :class="[
                !visible ? 'show-border-bottom' : 'hidden-border-bottom',
                'selector',
            ]"
            @click="toggleDropdown"
        >
            <div class="label">
                <span v-if="selectedValue">{{ selectedValue }}</span>
                <input
                    :value="modelValue"
                    @input="$emit('update:modelValue', $event.target.value)"
                    type="text"
                    :placeholder="[!selectedValue ? (visible 
                            ? 'This is a search input'
                            : dataList.description) : ''
                    ]"
                    @keyup.delete="$emit('remove')"
                />
            </div>
            <div>
                <img
                    v-if="!visible"
                    src="../../src/assets/chevron-down.svg"
                    class="arrow"
                    alt="arrow-down"
                />
                <img
                    v-else
                    src="../../src/assets/chevron-up.svg"
                    class="arrow"
                    alt="arrow-up"
                />
            </div>
            <div :class="[!visible ? 'hidden' : 'visible']">
                <ul>
                    <li
                        v-for="option in filterOptions()"
                        @click="optionSelected(option)"
                    >
                        {{ option }}
                    </li>
                    <span
                        v-if="filterOptions().length === 0"
                        class="message"
                    >{{ notFoundMessage }}
                    </span>
                </ul>
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
.wrapper-input {
    width: 280px;
    margin: 20px auto;

    .selector {
        font-size: 16px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 5px 8px;
        height: 56px;
        box-shadow: 0 10px 15px 01px rgba(35, 78, 82, 0.1);
        background-color: rgba(255, 255, 255, 1);
        border-radius: 8px;
        position: relative;
        z-index: 1;

        .arrow {
            position: absolute;
            right: 22px;
            top: 46%;
        }

        .expanded {
            transform: rotateZ(180deg) translateY(2px);
        }

        .label {
            display: flex;
            padding: 12px;
            font-size: 16px;
            color: #888;

            input {
                font-size: 16px;
                outline: none;
                border: 0;
                width: 100%;
            }

            input::placeholder {
                color: rgba(160, 174, 192, 1);
            }
        }
    }

    .show-border-bottom {
        border-radius: 8px;
    }

    .hidden-border-bottom {
        border-radius: 8px 8px 0 0;
    }

    ul {
        width: 100%;
        height: 180px;
        overflow-y: auto;
        overflow-x: hidden;
        list-style-type: none;
        padding: 0;
        margin: 0;
        font-size: 16px;
        border-radius: 0 0 10px 10px;
        position: absolute;
        top: 100%;
        left: 0;
        z-index: 1;
        background-color: rgba(255, 255, 255, 1);
    }

    li {
        text-align: left;
        font-weight: 600;
        font-size: 14px;
        padding: 12px 16px;

        &:hover {
            color: rgba(66, 153, 225, 1);
        }
    }

    .message {
        display: flex;
        padding: 16px;
        font-size: 14px;
        font-weight: 600;
        color: rgba(160, 174, 192, 1);
        text-align: left;
    }

    .hidden {
        visibility: hidden;
    }

    .visible {
        visibility: visible;
    }
}
</style>
