
# 1. Description :

```php

bloginfo("description");

```

# 2. Title 

```php

bloginfo("title");

```

# 3. add_theme_support

```php

    function bootstrapping(){
        load_theme_textdomain("alpha");
        add_theme_support( 'post-thumbnails' );
        add_theme_support( 'title-tag' );
    }
    add_action("after_setup_theme", "bootstrapping");
    
    
    function alpha_assets(){
        wp_enqueue_style("alpha", get_stylesheet_uri());
        wp_enqueue_style("bootstrap", "//maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css");



        
        // Js Script adding

        wp_enqueue_script("featherlight-js", "//cdn.jsdelivr.net/npm/featherlight@1.7.14/release/featherlight.min.js", array('jquery'),'0.0.1', true);
    }
    
    add_action("wp_enqueue_scripts", "alpha_assets");
```   

# 4. Post Tags list

```php

get_the_tag_list("<ul class='list-unstyled'><li>", "</li><li>", "</li></ul>");

```

# 5. Post Pagination

```php

the_posts_pagination( array( 'screen_reader_text' => '', ));

```

# 6. Post excerpt

```php

the_excerpt();

```

# 7. Post Permalink

```php

the_permalink(); 

```

# 8. Post Comments

```php

comments_template();

```

# 9. Get template Part

```php

get_template_part("hero");();

```

# 10. Home Page URL

```php

echo site_url();

```

# 11. Previous & Next Post URL

```php

next_post_link();
previous_post_link();

```

# 12. Register Sidebar 

```php

    function alpha_sidebar(){
        register_sidebar(
            array(
                'name' => __( 'Single Post Sidebar', 'alpha'),
                'id' => 'sidebar-1',
                'description' => __('Right Sidebar', 'alpha'),
                'before_widget' => '<section id="%1$s" class="widget %2$s">',
                'after_widget' => '</section>',
                'before_title' => '<h2 class="widget-title">',
                'after_title' => '</h2>',
            )
        );
    }

    add_action("widgets_init", "alpha_sidebar");

```

// active this hooks
```php
if(is_active_sidebar("sidebar-1")){
    dynamic_sidebar("sidebar-1");
}

```


# 13. Register Nav Menu 

```php

    // add this code functions.php files

    register_nav_menu("topmenu", __("Top Menu", "alpha"));    

    // displaying the menu where you want! 
    wp_nav_menu(
        array(
            'theme_location' => '',
            'menu_id' => '',
            'menu_class' => 'list-line text-center',
        )
    );

```

# 14. Add filter for Menu, Css class 

```php

    
    function alpha_menu_item_class($classes, $item){
        $classes[] = "list-inline-item";
        return $classes;
    }

    add_filter("nav_menu_css_class", "alpha_menu_item_class",10,2);

```


# 15. show the post thumbnail in href

```php

    $thumbnails_url = get_the_post_thumbnail_url(null, 'large');

```


