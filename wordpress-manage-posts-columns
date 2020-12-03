/* Admin columns */
add_filter( 'manage_myposttype_posts_columns', 'set_custom_edit_myposttype_columns' );
function set_custom_edit_myposttype_columns( $columns ) {
	$date = $columns['date'];
	unset( $columns['date'] );

	$columns['views'] = 'Views';
	$columns['votes'] = 'Votes';

	$columns['date']  = $date;

	return $columns;
}

add_filter( 'manage_edit-myposttype_sortable_columns', 'set_custom_myposttype_sortable_columns' );
function set_custom_myposttype_sortable_columns( $columns ) {
	$columns['views'] = 'views';
	$columns['votes'] = 'votes';

	return $columns;
}

add_action( 'manage_myposttype_posts_custom_column' , 'custom_myposttype_column', 10, 2 );
function custom_myposttype_column( $column, $post_id ) {
	if ( $column == 'views' ) {
		echo esc_html( get_post_meta( $post_id, 'views', true ) );
	}

	if ( $column == 'votes' ) {
		echo esc_html( get_post_meta( $post_id, 'votes', true ) );
	}
}

add_action( 'pre_get_posts', 'custom_myposttype_orderby' );
function custom_myposttype_orderby( $query ) {
	if ( !is_admin() || !$query->is_main_query() || $query->get('post_type') != 'myposttype' )
		return;

	$orderby = $query->get( 'orderby');

	if ( 'views' == $orderby ) {
		$query->set( 'meta_key', 'views' );
		$query->set( 'orderby', 'meta_value_num' );
	}

	if ( 'votes' == $orderby ) {
		$query->set( 'meta_key', 'votes' );
		$query->set( 'orderby', 'meta_value_num' );
	}
}
