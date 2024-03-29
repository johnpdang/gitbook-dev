# Snippets

### Locally add new admin user using functions.php

```
wp_insert_user(array('user_pass' => 'password_here', 'user_login' => 'username_here', 'user_email' => 'mail@email.com', 'role' => 'administrator'));
```

### PHP

{% tabs %}
{% tab title="php conditional logic" %}
{% code title="if h6 form description" %}
```php
<?php if ($form_desc): ?>
  <h6 class="footer__form__desc"><?php echo $form_desc; ?></h6>
<?php endif; ?>
```
{% endcode %}

{% code title="conditional php logic" %}
```php
if($text_eyebrow):
  $output .= '<h6 class="eyebrow">' . $text_eyebrow . '</h6>';
endif;
$output .= '

```
{% endcode %}
{% endtab %}

{% tab title="image source" %}
{% code title="image source" %}
```php
$html .= '<figure class="gallery-image">';
    $html .= '<img src="' . $image['url'] . '" alt="' . $image['title'] . '" />';
$html .= '</figure>';
```
{% endcode %}
{% endtab %}
{% endtabs %}

### WordPress

{% tabs %}
{% tab title="nav" %}
{% code title="register nav menus" %}
```php
	// This theme uses wp_nav_menu() in three locations.
	register_nav_menus( array(
		'top'    => __( 'Top Menu', 'traina' ),
		'footer'    => __( 'Footer Menu', 'traina' ),
		'social' => __( 'Social Links Menu', 'traina' ),
	) );
```
{% endcode %}

{% code title="navigation-top" %}
```php
	<?php  // Loop through nav object and output custom markup structure
    $menu_items = get_nav_menu_items_by_location('top');
	print_r($menu_items);?>
	<div class="menu-main-menu-container">
		<ul id="top-menu" class="menu">
			<?php
			// Loop through nav items
			foreach ($menu_items as $i => $menu_item) {

				// display top level items only first
				if( $menu_item->menu_item_parent == 0 ) {

	                $parent = $menu_item->ID;

					// loop through nav items again to display sub-menu items of this top level item
	                $menu_array = array();
	                foreach( $menu_items as $submenu ) {
	                    if( $submenu->menu_item_parent == $parent ) {
	                        $has_sub_menu = true;
	                        $menu_array[] = '<li><a href="' . $submenu->url . '">' . $submenu->title . '</a></li>' ."\n";
	                    }
	                }
					// If the top level item has a sub-menu, build the mega-menu and display the second level items.
	                if( $has_sub_menu == true && count( $menu_array ) > 0 ) {?>
						<?php
						echo '<li class="dropdown">';
	                    echo '<a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">' . $menu_item->title . ' <span class="caret"></span></a>';
						?>
						<div class="mega-menu-wrapper mega-menu-item-<?php echo $i;?>">
							<div class="container">
								<?php
			                    echo '<ul class="dropdown-menu">';
			                    echo implode( "\n", $menu_array );
			                    echo '</ul>';
								?>
							</div><!--.container-->
						</div><!--.mega-menu-wrapper-->
	                <?php } else {

	                    echo '<li>';
	                    echo '<a href="' . $menu_item->url . '">' . $menu_item->title . '</a>';
	                }

	            }
			}
			?>
		</ul>
	</div>
	<?php ?>
```
{% endcode %}
{% endtab %}

{% tab title="title" %}
{% code title="page title | site name" %}
```php
<title>	<?php wp_title('|',true,'right'); bloginfo('name'); ?></title>
```
{% endcode %}
{% endtab %}

{% tab title="rest api" %}
```javascript
dev.local/wp-json/wp/v2/posts
```
{% endtab %}
{% endtabs %}

### Traina

{% tabs %}
{% tab title="traina icons" %}
{% code title="get svg arrow icon" %}
```php
<?php echo traina_get_svg_icon('arrow-icon'); ?>
```
{% endcode %}
{% endtab %}

{% tab title="WP REST API" %}
By default, the REST API does not support the ‘menu\_order’ order\_by filter. Luckily, we can add to the allowed filters list. Place this in your functions.php or similar file:

```php
// This enables the orderby=menu_order for Posts
add_filter( 'rest_post_collection_params', 'filter_add_rest_orderby_params', 10, 1 );

// And this for a custom post type called 'beer'
add_filter( 'rest_beer_collection_params', 'filter_add_rest_orderby_params', 10, 1 );

/* Add menu_order to the list of permitted orderby values */
function filter_add_rest_orderby_params( $params ) {
	$params['orderby']['enum'][] = 'menu_order';
	return $params;
}
```

**FETCHING CUSTOM POST TYPES BY MENU ORDER IN ASCENDING ORDER:**

_Where the custom post type is “beer”_

```php
/wp-json/wp/v2/beer?orderby=menu_order&order=asc
```
{% endtab %}
{% endtabs %}

```
wp-json/wp/v2/posts
```
