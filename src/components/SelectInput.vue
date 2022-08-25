<script setup lang="ts">
    const props = defineProps({
        value: String,
        optionsList: Array,
        toggleDropdown: Function,
        visible: Boolean,
        optionSelected: Function,
    })
    console.log(props.visible)
</script>

<template>
  <div class="wrapper-input">
      <div :class="[!props.visible ? 'show-border-bottom' : 'hidden-border-bottom', 'selector']" @click="toggleDropdown">
          <div class="label">
              <input 
                  type="text" 
                 :placeholder="[visible ? 'This is a search input' : 'Select an item']"
              >
          </div>
          <div>
              <img v-if="!visible" src="../../src/assets/chevron-down.svg" class="arrow" alt="arrow-down">
              <img v-else src="../../src/assets/chevron-up.svg" class="arrow" alt="arrow-up">
          </div>
          <div :class="[!props.visible ? 'hidden' : 'visible']">
              <ul>
                  <li
                      v-for="option in optionsList"
                      @click="optionSelected(option.text)">
                      {{ option.text }}
                  </li>
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
            display: block;
            padding: 12px;
            font-size: 16px;
            color: #888;
            
            input {
                font-size: 16px;
                outline: none;
                border: 0;
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
        padding: 12px;
        
        &:hover {
            color: rgba(66, 153, 225, 1);
        }
    }
    
    .hidden {
        visibility: hidden;
    }
    
    .visible {
        visibility: visible;
    }
}
</style>
