<script setup lang="ts">
import { ref } from 'vue'
import { Link, router, usePage } from '@inertiajs/vue3'
import AppLayout from '@/Layouts/AppLayout.vue'
import { Button } from '@/Components/ui/button'
import { Badge } from '@/Components/ui/badge'
import { Alert, AlertDescription } from '@/Components/ui/alert'
import {
  Table,
  TableBody,
  TableCell,
  TableHead,
  TableHeader,
  TableRow,
} from '@/Components/ui/table'
import {
  AlertDialog,
  AlertDialogAction,
  AlertDialogCancel,
  AlertDialogContent,
  AlertDialogDescription,
  AlertDialogFooter,
  AlertDialogHeader,
  AlertDialogTitle,
  AlertDialogTrigger,
} from '@/Components/ui/alert-dialog'

interface Post {
  id: number
  title: string
  content: string
  is_published: boolean
  created_at: string
  updated_at: string
}

const props = defineProps<{
  posts: Post[]
}>()

const page = usePage()
const flash = page.props.flash as { success?: string }

const deletePost = (id: number) => {
  router.delete(`/posts/${id}`)
}

const formatDate = (dateString: string) => {
  return new Date(dateString).toLocaleDateString(undefined, {
    year: 'numeric',
    month: 'short',
    day: 'numeric',
  })
}
</script>

<template>
  <AppLayout>
    <div class="space-y-6">
      <!-- Page Header -->
      <div class="flex items-center justify-between">
        <div>
          <h1 class="text-3xl font-bold tracking-tight">Posts</h1>
          <p class="text-muted-foreground">Manage your blog posts</p>
        </div>
        <Link href="/posts/create">
          <Button>
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-2"><line x1="12" y1="5" x2="12" y2="19"></line><line x1="5" y1="12" x2="19" y2="12"></line></svg>
            Create Post
          </Button>
        </Link>
      </div>

      <!-- Flash Message -->
      <Alert v-if="flash?.success" variant="success">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"></polyline></svg>
        <AlertDescription>{{ flash.success }}</AlertDescription>
      </Alert>

      <!-- Posts Table -->
      <div class="rounded-md border">
        <Table>
          <TableHeader>
            <TableRow>
              <TableHead>Title</TableHead>
              <TableHead>Status</TableHead>
              <TableHead>Created</TableHead>
              <TableHead class="text-right">Actions</TableHead>
            </TableRow>
          </TableHeader>
          <TableBody>
            <TableRow v-if="posts.length === 0">
              <TableCell colspan="4" class="h-24 text-center text-muted-foreground">
                No posts yet. Create your first post!
              </TableCell>
            </TableRow>
            <TableRow v-for="post in posts" :key="post.id">
              <TableCell class="font-medium">
                <div>
                  <p class="font-semibold">{{ post.title }}</p>
                  <p class="text-sm text-muted-foreground line-clamp-1">{{ post.content }}</p>
                </div>
              </TableCell>
              <TableCell>
                <Badge :variant="post.is_published ? 'success' : 'secondary'">
                  {{ post.is_published ? 'Published' : 'Draft' }}
                </Badge>
              </TableCell>
              <TableCell class="text-muted-foreground">
                {{ formatDate(post.created_at) }}
              </TableCell>
              <TableCell class="text-right">
                <div class="flex items-center justify-end gap-2">
                  <Link :href="`/posts/${post.id}/edit`">
                    <Button variant="outline" size="sm">
                      <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-1"><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"></path><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"></path></svg>
                      Edit
                    </Button>
                  </Link>
                  <AlertDialog>
                    <AlertDialogTrigger as-child>
                      <Button variant="destructive" size="sm">
                        <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-1"><polyline points="3 6 5 6 21 6"></polyline><path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a1 1 0 0 1 1-1h4a1 1 0 0 1 1 1v2"></path></svg>
                        Delete
                      </Button>
                    </AlertDialogTrigger>
                    <AlertDialogContent>
                      <AlertDialogHeader>
                        <AlertDialogTitle>Are you sure?</AlertDialogTitle>
                        <AlertDialogDescription>
                          This action cannot be undone. This will permanently delete the post
                          <span class="font-semibold">"{{ post.title }}"</span>.
                        </AlertDialogDescription>
                      </AlertDialogHeader>
                      <AlertDialogFooter>
                        <AlertDialogCancel>Cancel</AlertDialogCancel>
                        <AlertDialogAction
                          class="bg-destructive text-destructive-foreground hover:bg-destructive/90"
                          @click="deletePost(post.id)"
                        >
                          Delete
                        </AlertDialogAction>
                      </AlertDialogFooter>
                    </AlertDialogContent>
                  </AlertDialog>
                </div>
              </TableCell>
            </TableRow>
          </TableBody>
        </Table>
      </div>
    </div>
  </AppLayout>
</template>
