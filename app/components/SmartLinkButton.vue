<script setup lang="ts">
import { computed } from 'vue'
import { handleLinkClick, getTooltipText } from '~/utils/linkHandlers'

interface LinkLike {
  to?: string
  account?: string
  ariaLabel?: string
  [key: string]: unknown
}

const { link } = defineProps<{ link: LinkLike }>()

const tooltipProps = computed(() => ({
  text: String(getTooltipText(link)),
  copyText: String(link?.account ?? link?.to ?? ''),
  ariaLabel: String(link?.ariaLabel ?? '')
}))
</script>

<template>
  <CopyTooltip v-bind="tooltipProps">
    <UButton
      v-bind="{
        size: 'xs',
        color: 'neutral',
        variant: 'ghost',
        ...link
      }"
      @click="handleLinkClick(link)"
    />
  </CopyTooltip>
</template>
