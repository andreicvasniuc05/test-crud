<script setup lang="ts">
import { AlertDialogAction } from 'radix-vue'
import { cn } from '@/lib/utils'
import { buttonVariants } from '@/Components/ui/button'

const props = defineProps<{ class?: string }>()
</script>
<template>
  <AlertDialogAction :class="cn(buttonVariants(), props.class)">
    <slot />
  </AlertDialogAction>
</template>
