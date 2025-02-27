# abovo
Slides and sample code on the training Nuxt, Abovo Media, Spring 2025

* See the various slides in the `./slides` directory. 
* This repo will be deleted on 1st April, 2025. Make sure you have a copy before that date.
* General example code: https://github.com/PeterKassenaar/nuxt-fundamentals


## Links
* https://www.youtube.com/watch?v=8aGhZQkoFbQ - meer over de werking van de Javascript event loop en Queue/Stack.

## Examples on <code>fetch</code>

```typescript
// 1. Native fetch() using async/await notation
const fetchPosts = async () => {
  try {
    const res = await fetch(url);
    if (!res.ok) throw new Error('Failed to fetch posts');
    posts.value = await res.json();
  } catch (error) {
    console.error(error);
  }
};

// 2. Native fetch() using traditional Promise-notation.
// Functionality EXACTLY the same. Only a different syntax.
const fetchPosts = () => {
  fetch(url)
      .then(res => {
        if (!res.ok) throw new Error('Failed to fetch posts');
        return res.json();
      })
      .then(data => {
        posts.value = data;
      })
      .catch(error => {
        console.error(error);
      })
      .finally(/*clear local storage ofzo.... */);

};

// 3. Call fetching the posts in a component lifeCycle hook.
// When using Nuxt useFetch(), do NOT use `onMounted()`, as this would result in errors.
// Using `useFetch()` eliminates the need for `onMounted` since `useFetch()`
// triggers immediately and attaches to the component's lifecycle.
onMounted(() => {
  fetchPosts();
});

// 4. Fetching posts using useFetch()
// The const {...} = useXYZ() is called "ES6 Destructuring"
const {refresh, data: myPosts, error} = useFetch<Post[]>(url);

// Watch for changes and handle fetched data
if (error.value) {
  console.error('Failed to fetch posts:', error.value);
} else {
  posts.value = myPosts.value || [];
}

// 5. Using $fetch() - a Nuxt-enhanced version of fetch(). No 
// need to manually parse .json()
const myData = await $fetch('/api/myData');
```

