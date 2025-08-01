<script setup>
import { reactive, ref } from 'vue';

import * as icons from 'macos-traffic-lights';

const order = ['close', 'minimize', 'maximize'];

const iconsByState = {
    close: {
        default: icons.closeDefault,
        hover: icons.closeHover,
        active: icons.closeActive,
        unfocused: icons.unfocused,
    },
    minimize: {
        default: icons.minimizeDefault,
        hover: icons.minimizeHover,
        active: icons.minimizeActive,
        unfocused: icons.unfocused,
    },
    maximize: {
        default: icons.maximizeDefault,
        hover: icons.maximizeHover,
        active: icons.maximizeActive,
        unfocused: icons.unfocused,
    },
};

const baseState = ref('default');
const iconStates = reactive({
    close: 'default',
    minimize: 'default',
    maximize: 'default',
});

const emit = defineEmits([
    'close',
    'minimize',
    'maximize',
]);

const getIconSrc = (name) => iconsByState[name][iconStates[name]];

const onGroupMouseEnter = () => {
    order.forEach((name) => {
        if (iconStates[name] !== 'active') {
            iconStates[name] = 'hover';
        }
    });
};

const onGroupMouseLeave = () => {
    order.forEach((name) => {
        iconStates[name] = baseState.value;
    });
};

const onMouseDown = (name) => {
    onGroupMouseEnter();
    iconStates[name] = 'active';
};

const onMouseUp = (name) => {
    iconStates[name] = 'hover';
};

const focus = () => {
    baseState.value = 'default';
    order.forEach((name) => (iconStates[name] = 'default'));
};

const unfocus = () => {
    baseState.value = 'unfocused';
    order.forEach((name) => (iconStates[name] = 'unfocused'));
};

const handleClick = (name) => {
    if (baseState.value === 'unfocused') {
        baseState.value = 'default';
    }
    emit(name);
};

defineExpose({
    focus,
    unfocus,
});

</script>

<template>
    <div
        @mouseenter="onGroupMouseEnter"
        @mouseleave="onGroupMouseLeave"
    >
        <img
            v-for="name in order"
            :key="name"
            :src="getIconSrc(name)"
            class="w-3 h-3"
            :alt="name"
            draggable="false"
            @mousedown="onMouseDown(name)"
            @mouseup="onMouseUp(name)"
            @click="handleClick(name)"
        />
    </div>
</template>
