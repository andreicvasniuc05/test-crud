<script setup lang="ts">
import { Link, useForm } from '@inertiajs/vue3'
import AppLayout from '@/Layouts/AppLayout.vue'
import { Button } from '@/Components/ui/button'
import { Input } from '@/Components/ui/input'
import { Textarea } from '@/Components/ui/textarea'
import { Label } from '@/Components/ui/label'
import { Switch } from '@/Components/ui/switch'
import { Card, CardContent, CardHeader, CardTitle, CardDescription } from '@/Components/ui/card'

const form = useForm({
  title: '',
  content: '',
  is_published: false,
})

const submit = () => {
  form.post('/posts')
}
</script>

<template>
  <AppLayout>
    <div class="max-w-2xl mx-auto space-y-6">
      <!-- Page Header -->
      <div class="flex items-center gap-4">
        <Link href="/posts">
          <Button variant="outline" size="sm">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-1"><line x1="19" y1="12" x2="5" y2="12"></line><polyline points="12 19 5 12 12 5"></polyline></svg>
            Back
          </Button>
        </Link>
        <div>
          <h1 class="text-3xl font-bold tracking-tight">Create Post</h1>
          <p class="text-muted-foreground">Add a new blog post</p>
        </div>
      </div>

      <!-- Create Form -->
      <Card>
        <CardHeader>
          <CardTitle>Post Details</CardTitle>
          <CardDescription>Fill in the details for your new post.</CardDescription>
        </CardHeader>
        <CardContent>
          <form @submit.prevent="submit" class="space-y-6">
            <!-- Title -->
            <div class="space-y-2">
              <Label for="title">Title</Label>
              <Input
                id="title"
                v-model="form.title"
                type="text"
                placeholder="Enter post title..."
                :class="form.errors.title ? 'border-destructive' : ''"
              />
              <p v-if="form.errors.title" class="text-sm text-destructive">
                {{ form.errors.title }}
              </p>
            </div>

            <!-- Content -->
            <div class="space-y-2">
              <Label for="content">Content</Label>
              <Textarea
                id="content"
                v-model="form.content"
                placeholder="Write your post content..."
                class="min-h-[200px]"
                :class="form.errors.content ? 'border-destructive' : ''"
              />
              <p v-if="form.errors.content" class="text-sm text-destructive">
                {{ form.errors.content }}
              </p>
            </div>

            <!-- Is Published -->
            <div class="flex items-center justify-between rounded-lg border p-4">
              <div class="space-y-0.5">
                <Label for="is_published" class="text-base">Publish Post</Label>
                <p class="text-sm text-muted-foreground">
                  Make this post visible to the public
                </p>
              </div>
              <Switch
                id="is_published"
                :checked="form.is_published"
                @update:checked="form.is_published = $event"
              />
            </div>

            <!-- Actions -->
            <div class="flex items-center gap-3 pt-2">
              <Button type="submit" :disabled="form.processing">
                <svg v-if="form.processing" class="mr-2 h-4 w-4 animate-spin" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                  <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                  <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                </svg>
                Create Post
              </Button>
              <Link href="/posts">
                <Button type="button" variant="outline">Cancel</Button>
              </Link>
            </div>
          </form>
        </CardContent>
      </Card>
    </div>
  </AppLayout>
</template>
