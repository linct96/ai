# Path Params

Use `$` prefix for dynamic segments:

## Path Params In Components

If we add a component to our postRoute, we can access the postId variable from the URL by using the route's useParams hook:

```typescript
// src/routes/posts/$postId.tsx
export const Route = createFileRoute('/posts/$postId')({
  component: PostComponent,
})

function RouteComponent() {
  const { postId } = Route.useParams()
  return <div>Post {postId}</div>
}
```

## Path Params In Loaders

Path params are passed to the loader as a params object. For example, if we were to visit the /posts/123 URL, the `params` object would be `{ postId: '123' }`:

```typescript
// src/routes/posts/$postId.tsx
import { createFileRoute } from '@tanstack/react-router'

export const Route = createFileRoute('/posts/$postId')({
  loader: async ({ params }) => {
    return fetchPost(params.postId)
  },
})
```

The `params` object is also passed to the `beforeLoad` option:

```typescript
// src/routes/posts/$postId.tsx
import { createFileRoute } from '@tanstack/react-router'

export const Route = createFileRoute('/posts/$postId')({
  beforeLoad: async ({ params }) => {
    // do something with params.postId
  },
})
```

