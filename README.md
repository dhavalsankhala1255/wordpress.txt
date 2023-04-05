/*--------Iamge code-------*/

<?php echo get_template_directory_uri(); ?>/

/*------------ CSS and JS ---------------*/

fuction.php

wp_enqueue_style( 'zeden-slick', get_template_directory_uri() . '/css/slick.css', array(), _S_VERSION);

wp_enqueue_script( 'zeden-script', get_template_directory_uri() . '/js/script.js', array(), _S_VERSION, true );



/*------------ Logo ---------------*/

<?php
	if(has_custom_logo()){
		the_custom_logo();
	}else{
	?>
<?php } ?>

/*------------ Navbar ---------------*/

<nav class="navbar">
	<?php
		wp_nav_menu(
			array(
				'theme_location' => 'menu-1',
				'menu_id'        => 'primary-menu',
				'menu_class'        => 'header-menu',
				'container' => false,
			)
		);
	?>
</nav>

/*------------ content PHP code ---------------*/

<?php if( get_field('banner_heading') ): ?>
		<h1><?php the_field('banner_heading'); ?></h1>
<?php endif; ?>

/*------------ Button link Array PHP code ---------------*/

<?php 
	$link = get_field('banner_btn');
	if( $link ): 
		$link_url = $link['url'];
		$link_title = $link['title'];
		$link_target = $link['target'] ? $link['target'] : '_self';
		?>
		<a class="btn" href="<?php echo esc_url( $link_url ); ?>" target="<?php echo esc_attr( $link_target ); ?>"><?php echo esc_html( $link_title ); ?></a>
<?php endif; ?>


/*------------ Image Array PHP code ---------------*/

<?php 
	$image = get_field('banner_img');
	if( !empty( $image ) ): ?>
		<img src="<?php echo esc_url($image['url']); ?>" alt="<?php echo esc_attr($image['alt']); ?>" />
<?php endif; ?>



/*------------ Repeter ---------------*/
slider
 ----- image Id
<?php if( have_rows('client_logo_slider') ): ?>
	<ul class="client-logo__slider">
		<?php while( have_rows('client_logo_slider') ): the_row(); ?>
		<li>
			<?php echo wp_get_attachment_image( get_sub_field('logo_img'), 'full' ); ?>
		</li>
		<?php endwhile; ?>
	</ul>
<?php endif; ?>



/*---------Custom post type-----------------*/ 


add_action('init', 'codex_service_init');
function codex_service_init()
{
    $labels = array(
        'name'               => _x('Services', 'post type general name', 'webyant'),
        'singular_name'      => _x('Services', 'post type singular name', 'webyant'),
        'menu_name'          => _x('Services', 'admin menu', 'webyant'),
        'name_admin_bar'     => _x('Services', 'add new on admin bar', 'webyant'),
        'add_new'            => _x('Add New', 'press', 'webyant'),
        'add_new_item'       => ('Add New Services', 'webyant'),
        'new_item'           => ('New Services', 'webyant'),
        'edit_item'          => ('Edit Services', 'webyant'),
        'view_item'          => ('View Services', 'webyant'),
        'all_items'          => ('All Services', 'webyant'),
        'search_items'       => ('Search Services', 'webyant'),
        'parent_item_colon'  => ('Parent Services:', 'webyant'),
        'not_found'          => ('No service found.', 'webyant'),
        'not_found_in_trash' => ('No service found in Trash.', 'webyant')
    );

    $args = array(
        'labels'             => $labels,
        'description'        => ('Description.', 'webyant'),
        'public'             => true,
        'publicly_queryable' => true,
        'show_ui'            => true,
        'show_in_menu'       => true,
        'query_var'          => true,
        'rewrite'            => array('slug' => 'services'),
        'capability_type'    => 'post',
        'has_archive'        => true,
        'hierarchical'       => false,
        'exclude_from_search' => false,
        'menu_position'      => null,
        'supports'           => array('title', 'editor', 'thumbnail')
    );

    register_post_type('service', $args);
    flush_rewrite_rules();
}



