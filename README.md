
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



        // Extarnal Jquery file load library

        wp_enqueue_script("featherlight-js", "//cdn.jsdelivr.net/npm/featherlight@1.7.14/release/featherlight.min.js", array('jquery'),'0.0.1', true);

        // internal Jquery file load
        wp_enqueue_script("main-js", get_template_directory_uri()."/assets/js/main.js", array('jquery'),'0.0.1', true);

    }
    
    add_action("wp_enqueue_scripts", "alpha_assets");
```   

# 4. Post Tags list

```php

get_the_tag_list("<ul class='list-unstyled'><li>", "</li><li>", "</li></ul>");

```

# 5. Loop Post Query

```php

    <?php while(have_posts()):
        the_post();
    ?>
        // Here your Content
    <?php 
        endwhile;
    ?>
```

# 6. Post Pagination

```php

the_posts_pagination( array( 'screen_reader_text' => '', ));

```

# 7. Post excerpt

```php

the_excerpt();

```

# 8. Post Permalink

```php

the_permalink(); 

```

# 9. Post Comments

```php

comments_template();

```

# 10. Get template Part

```php

get_template_part("hero");

```

# 11. Home Page URL

```php

echo site_url();

```

# 12. Previous & Next Post URL

```php

next_post_link();
previous_post_link();

```

# 13. Register Sidebar 

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


# 14. Register Nav Menu 

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

# 15. Add filter for Menu, Css class 

```php

    
    function alpha_menu_item_class($classes, $item){
        $classes[] = "list-inline-item";
        return $classes;
    }

    add_filter("nav_menu_css_class", "alpha_menu_item_class",10,2);

```


# 16. Show the post thumbnail in href

```php

    $thumbnails_url = get_the_post_thumbnail_url(null, 'large');

```



# 17. cache busting Solution -> use time() function

```php

    wp_enqueue_style("alpha", get_stylesheet_uri(), null, time());


    // Live server caches Solution

    if(site_url() == "https://example.com"){
        define("VERSION", time());
    }else{
        define("VERSION", wp_get_theme()->get("Version"));
    }


```



# 18. Remove the inline css function hook

```php


    function alpha_about_banner(){
        if(is_page()):
        $feat_image = get_the_post_thumbnail_url(null, "large");
    ?>
    <style>
        .page-header{
            background-image: url(<?php echo $feat_image;?>);
        }
    </style>
    <?php
        endif;
    }

    add_action("wp_head","alpha_about_banner",11);


```


# 19. Custom header Support

```php


    function bootstrapping(){
        
        add_theme_support( 'custom-header' );
    }
    add_action("after_setup_theme", "bootstrapping");
    

    if(is_front_page()):
        if(current_theme_supports("custom-header")):
    ?>
    <style>
        .header{
            background-image: url(<?php echo header_image();?>);
            background-repeat: no-repeat;
            background-size: cover;
            margin-bottom: 50px;
        }

        .header h1.heading a, h3.tagline{
            color: #<?php echo get_header_textcolor();?>;

            <?php 
                if(!display_header_text()){
                    echo "display:none;";
                }
            ?>

        }
    </style>

    <?php
        endif;
    endif;
    }




```




# 20. Custom Logo Support

```php


    function bootstrapping(){

        $alpha_logo = array(
            'width'   => 100,
            'height' => 100,
        );
        add_theme_support( 'custom-logo' ,$alpha_logo);

    }
    add_action("after_setup_theme", "bootstrapping");
    

    // where you want to show you logo

    <?php if(current_theme_supports("custom-logo")):?>
        <div class="header-logo text-center">
            <?php the_custom_logo();?>
        </div>
    <?php endif;?>


```


# 21. If Post thumbnail exist

```php
 <?php 
    if(has_post_thumbnail()){
        the_post_thumbnail('large', array('class'=> 'img-fluid'));
    }
?>

```

# 22. the Post Single Views otherwise show excerpt.

```php

<?php 
    if(is_single()){
        the_content();
    }else{
        the_excerpt();
    }
?>

```

# 23. If the comments doesn't open 

```php

<?php if(comments_open()):?>
    <div class="comments">
        <?php comments_template();?>
    </div>
<?php endif;?>


```


# 24. Custom Header Text Color 

```php

// Function Hook
function alpha_bootstraping(){  
    add_theme_support('custom-header');

    $alpha_custom_header= array(
        'header-text' => true,
        'default-text-color' => '#222',
    );

    add_theme_support('custom-header', $alpha_custom_header);

}

add_action("after_setup_theme", "alpha_bootstraping");

<?php
    endif;

    if(is_front_page()):
        if(current_theme_supports("custom-header")):

?>

<style>
    .header h1.heading a, h3.tagline{
        color: #<?php echo get_header_textcolor();?>;

        <?php if(!display_header_text()){
            echo "display:none;";
        }
        ?>
    }
</style>

<?php 
        endif;
    endif;
}


```


