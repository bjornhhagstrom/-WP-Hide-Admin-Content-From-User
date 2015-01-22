# -WP-Hide-Admin-Content-From-User

* Add to theme's functions.php file
* The function below alters the query on the admin edit.php page based on the current user's role ('editor' used below)

<pre><code>
// Hide pages from WP User Role
// Ref: http://wordpress.stackexchange.com/questions/91330/restrict-admin-access-to-certain-pages-for-certain-users
add_filter( 'parse_query', 'exclude_pages_from_admin' );
function exclude_pages_from_admin($query) {
    global $user_ID, $pagenow, $post_type;
    if ( current_user_can( 'editor' ) && $pagenow == 'edit.php') {
      if($post_type == 'page') {
        $query->query_vars['page_id'] = 107; // only show specific page
      } elseif($post_type == 'products') {
        $query->query_vars['product_cat'] = 'tshirts'; // only show posts from single/custom taxonomy term
      }
    }
}
</code><pre>
