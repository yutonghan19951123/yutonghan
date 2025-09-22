<script setup lang="ts">
import { computed } from 'vue'
import { handleLinkClick, getTooltipText } from '~/utils/linkHandlers'

interface LinkLike {
  to?: string
  account?: string
  ariaLabel?: string
  [key: string]: unknown
}

defineProps<{ link: LinkLike }>()

type CopyTooltipProps = {
  text: string
  copyText: string
  ariaLabel: string
}

// Build a camelCase props object for <CopyTooltip>
const tooltipProps = computed<CopyTooltipProps>(() => ({
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
