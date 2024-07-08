# Astro

By default uses SSG. Can use `directives` when you want more intractability. `client:load` will load js and hydrate the html (CSR) as soon as page loads. `client:visible` will do the same but only when island/component is visible.

## Islands

With islands you can have a mostly static page (SSR or SSG), and when you want more intractability you can use a client directive (CSR).
