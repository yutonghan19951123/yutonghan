<script setup lang="ts">
import { handleLinkClick, getTooltipText } from '~/utils/linkHandlers'

interface LinkLike {
  to?: string
  account?: string
  ariaLabel?: string
  [key: string]: unknown
}

defineProps<{
  link: LinkLike
}>()
</script>

<template>
  <CopyTooltip
    :text="String(getTooltipText(link))"
    :copy-text="String(link?.account ?? link?.to ?? '')"
    :aria-label="String(link?.ariaLabel ?? '')"
  >
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
