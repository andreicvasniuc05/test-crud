<script setup lang="ts">
import { computed } from 'vue'
import { cn } from '@/lib/utils'
import { cva, type VariantProps } from 'class-variance-authority'

const alertVariants = cva(
  'relative w-full rounded-lg border p-4 [&>svg~*]:pl-7 [&>svg+div]:translate-y-[-3px] [&>svg]:absolute [&>svg]:left-4 [&>svg]:top-4 [&>svg]:text-foreground',
  {
    variants: {
      variant: {
        default: 'bg-background text-foreground',
        destructive: 'border-destructive/50 text-destructive dark:border-destructive [&>svg]:text-destructive',
        success: 'border-green-500/50 bg-green-50 text-green-800 [&>svg]:text-green-800',
      },
    },
    defaultVariants: {
      variant: 'default',
    },
  }
)

export interface AlertProps extends VariantProps<typeof alertVariants> {
  class?: string
}

const props = defineProps<AlertProps>()

const classes = computed(() =>
  cn(alertVariants({ variant: props.variant }), props.class)
)
</script>

<template>
  <div role="alert" :class="classes">
    <slot />
  </div>
</template>
