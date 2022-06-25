---
title: "Menambahkan Next dan Previous Post pada Wordpress REST API"
date: "2022-06-25"
tags: ['PHP', 'WordPress']
image: /menambahkan-next-dan-previous-post-wordpress-rest-api/images/screenshot-2022-06-05-wp-rest-api.png.png
---

**Menambahkan Next dan Previous Post pada Wordpress REST API** - Secara *default*, Wordpress REST API tidak menyediakan link next/previous di dalam output JSON nya. Kita bisa menambahkannya secara manual agar link next/previous muncul di dalamnya.

Yang perlu kita lakukan adalah menambahkan function ini ke dalam `functions.php` yang ada pada tema Wordpress kita.

```php
add_filter( 'rest_prepare_post', 'add_prev_next_to_rest' , 10, 3 );

function add_prev_next_to_rest( $response, $post, $request ) {
    global $post;
    // Get the next post.
    $next = get_adjacent_post( false, '', false );
    // Get the previous post.
    $previous = get_adjacent_post( false, '', true );
    // Only send id and slug (or null, if there is no next/previous post).
    $response->data['next'] = ( is_a( $next, 'WP_Post') ) ? array( "id" => $next->ID, "slug" => $next->post_name ) : null;
    $response->data['previous'] = ( is_a( $previous, 'WP_Post') ) ? array( "id" => $previous->ID, "slug" => $previous->post_name ) : null;

    return $response;
}
```

Function di atas akan menambahkan *key* baru ke dalam output JSON:
```json
"next": {
    "id": 1728,
    "slug": "bekerja-dengan-remote-repository"
},
"previous": {
    "id": 1651,
    "slug": "deploy-jekyll-ke-vercel-dengan-mudah"
},
```