<script setup lang="ts">
import { Link } from '@inertiajs/vue3'
</script>

<template>
  <div class="min-h-screen bg-background">
    <!-- Header -->
    <header class="border-b border-border bg-card">
      <div class="container mx-auto flex h-16 items-center justify-between px-4">
        <div class="flex items-center gap-6">
          <Link href="/posts" class="text-xl font-bold text-foreground hover:text-primary transition-colors">
            Posts CRUD
          </Link>
          <nav class="flex items-center gap-4">
            <Link
              href="/posts"
              class="text-sm font-medium text-muted-foreground hover:text-foreground transition-colors"
            >
              Posts
            </Link>
          </nav>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <main class="container mx-auto px-4 py-8">
      <slot />
    </main>
  </div>
</template>
