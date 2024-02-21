
# 1. description :

```php
 bloginfo("description");
```

# 2. Title 

```php
 bloginfo("title");
```

# 3. add_theme_support

    function bootstrapping(){
        load_theme_textdomain("alpha");
        add_theme_support( 'post-thumbnails' );
        add_theme_support( 'title-tag' );
    }
    add_action("after_setup_theme", "bootstrapping");
    
    
    function alpha_assets(){
        wp_enqueue_style("alpha", get_stylesheet_uri());
        wp_enqueue_style("bootstrap", "//maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css");
    }
    
    add_action("wp_enqueue_scripts", "alpha_assets");
```   

# 4. Post Tags list

```php
get_the_tag_list("<ul class='list-unstyled'><li>", "</li><li>", "</li></ul>");
```

# 5. Post Pagination

the_posts_pagination( array( 'screen_reader_text' => '', ));


# 6. Post excerpt

 the_excerpt();

# 7. Post Permalink

the_permalink(); 

# 8. Post Comments

comments_template();


# 9. Get template Part

get_template_part("hero");();


# 10. Home Site URL

echo site_url();

# 11. Home Site URL

next_post_link();
previous_post_link();


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

// active this hooks
if(is_active_sidebar("sidebar-1")){
    dynamic_sidebar("sidebar-1");
}
