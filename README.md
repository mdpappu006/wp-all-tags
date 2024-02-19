
# 1. Description :

 bloginfo("description");


# 2. Title 

 bloginfo("title");


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
    

# 4. Post Tags list

get_the_tag_list("<ul class='list-unstyled'><li>", "</li><li>", "</li></ul>");


# 5. Post Pagination

the_posts_pagination( array( 'screen_reader_text' => '', ));


# 6. Post excerpt

 the_excerpt();

# 7. Post Permalink

the_permalink(); 
