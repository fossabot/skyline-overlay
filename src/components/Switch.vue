<template>
  <div class="select">
    <div :class="['select-on', modelValue && 'active']" @click="handleClick(true)">
      <slot name="true" :color="modelValue ? '#333333' : '#ffffff'">
        <ICheck :color="modelValue ? '#333333' : '#ffffff'" />
      </slot>
    </div>
    <div :class="['select-off', !modelValue && 'active']" @click="handleClick(false)">
      <slot name="false" :color="!modelValue ? '#333333' : '#ffffff'">
        <IClose :color="!modelValue ? '#333333' : '#ffffff'" />
      </slot>
    </div>
  </div>
</template>

<script>
// icons
import ICheck from '../assets/svgs/ICheck.vue';
import IClose from '../assets/svgs/IClose.vue';

/**
 * custom select component, use with `v-model`
 * receives two icon componets, fallbacks to `ICheck` and `IClose`
 * @param {boolean} modelValue
 */
export default {
  name: 'Switch',
  components: {
    ICheck,
    IClose,
  },
  props: {
    modelValue: {
      type: Boolean,
      required: true,
    },
  },
  setup(props, context) {
    // handle value change
    const handleClick = (value) => {
      if (props.modelValue !== value) {
        context.emit('update:modelValue', value);
      }
    };

    return {
      handleClick,
    };
  },
};
</script>

<style lang="scss" src="./Switch.scss">
</style>
