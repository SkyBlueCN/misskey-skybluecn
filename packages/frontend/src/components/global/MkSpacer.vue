<!--
SPDX-FileCopyrightText: syuilo and misskey-project
SPDX-License-Identifier: AGPL-3.0-only
-->

<template>
<div :class="[$style.root, { [$style.rootMin]: forceSpacerMin }]">
	<div :class="$style.content">
		<slot></slot>
	</div>
</div>
</template>

<script lang="ts" setup>
import { inject } from 'vue';
import { deviceKind } from '@/utility/device-kind.js';
import { DI } from '@/di.js';

const props = withDefaults(defineProps<{
	contentMax?: number | null;
	marginMin?: number;
	marginMax?: number;
}>(), {
	contentMax: null,
	marginMin: 12,
	marginMax: 24,
});

const forceSpacerMin = inject(DI.forceSpacerMin, false) || deviceKind === 'smartphone';
</script>

<style lang="scss" module>
.root {
	box-sizing: border-box;
	width: 100%;
}
.rootMin {
	padding: v-bind('props.marginMin + "px"') !important;
}

.content {
	margin: 0 auto;
	max-width: v-bind('props.contentMax + "px"');
	container-type: inline-size;
}

@container (max-width: 450px) {
	.root {
		padding: v-bind('props.marginMin + "px"');
	}
}

@container (min-width: 451px) {
	.root {
		padding: v-bind('props.marginMax + "px"');
	}
}
</style>
