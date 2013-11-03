# Bela Vista Dev Log


## Hiding Yoast for non-admin users
http://wordpress.stackexchange.com/questions/70879/wordpress-seo-by-yoast-hide-meta-boxes-in-posts-for-non-admins

## Reference for Linotype webfont help

Help for Linotype Webfonts
http://www.linotype.com/7032/webfonts.html
https://www.linotype.com/account/web-fonts-stats

## Working with qTranslate

I wish I found this sooner
http://shailan.com/3283/displaying-content-based-on-current-language-using-qtranslate/

## Search

### Step 1 - Expanding Wordpress' built in search to include custom post types and custom content fields

Which one did I end up using?

Improve Search
http://www.wpsitecare.com/best-wordpress-search-plugin/

http://wordpress.org/plugins/search-everything/
???

http://wordpress.org/plugins/custom-search-plugin/
Trying this

http://wordpress.org/plugins/wp-ultimate-search/
http://www.hongkiat.com/blog/wordpress-search-plugin-snippet/
http://wordpress.org/plugins/highlight-search-terms/

### Step 2 - Grouping custom content types on search results

http://wordpress.org/support/topic/order-search-results-by-post-type
http://wordpress.stackexchange.com/questions/94762/how-to-order-separated-custom-post-search-results
http://wordpress.stackexchange.com/questions/14881/seperating-custom-post-search-results

### Step 3 - Styling the search results and proiding multilingual versions of the text

This was relatively within my capability.

### Step 4 - Route users to the correct search page (english or chinese) based on which page they did the search from

http://www.qianqin.de/qtranslate/forum/viewtopic.php?f=3&t=64&start=20


## Custom Excerpts
I cant spell excerpts. I keep saying "exerpts"

http://wordpress.org/support/topic/custom-excerpt-text-in-functionsphp
http://wordpress.org/support/topic/how-to-pull-excerpt-from-advanced-custom-field

But didnt work for chinese! Because it counts words by spaces
https://dusijun.wordpress.com/2013/03/09/wrodpress-excerpt-length/
in mandarin but thank god for google translate

Declaring defaults for functions in PHP
http://www.devshed.com/c/a/PHP/PHP-Functions/2/

## Search

## Selection colour
```
::selection {
	background-color: @belavista-orange;
	color: #fff;/* Safari */
	}
::-moz-selection {
	background-color: @belavista-orange;
	color: #fff;	/* Firefox */
}
```

## Hooking into the nav menu
http://codex.wordpress.org/Function_Reference/wp_nav_menu
http://wordpress.stackexchange.com/questions/2574/remove-wrapping-div-and-ul-from-output-of-wp-nav-menu

## Translating slugs
http://wpml.org/documentation/getting-started-guide/translating-page-slugs/
http://not-only-code.github.io/qtranslate-slug/
https://github.com/not-only-code/qtranslate-slug
http://www.wpchef.net/recipe/extending-the-page-template-name-space
http://roots.io/an-introduction-to-the-roots-theme-wrapper/

Useful
http://rishida.net/tools/conversion/

## 2 google analytics on the same page
https://github.com/roots/roots/blob/master/lib/scripts.php
https://developers.google.com/analytics/devguides/collection/analyticsjs/method-reference
https://developers.google.com/analytics/devguides/collection/gajs/?csw=1#MultipleCommands

http://stackoverflow.com/questions/1239042/google-analytics-multiple-trackers-on-one-page-cookie-conflict

## Opening links in a new window
http://www.poseidonwebstudios.com/wordpress-2/make-external-links-open-in-a-new-window-in-wordpress/

## Getting queries and memory usage

A mash up of
http://www.wwvalue.com/tuts/tut-wp/wordpress-better-way-get-number-queries-and-page-load-time.html
and 
http://wp-mix.com/display-performance-stats-wordpress/

```
function interrobang_query_page_load_time() {
	if (current_user_can('administrator'))
	
	{
		global $wpdb;
		// Get the total page generation time
		$totaltime = timer_stop( false, 22 );
		 
		// Calculate the time spent on MySQL queries by adding up the time spent on each query
		$mysqltime = 0;
		foreach ( $wpdb->queries as $query )
			$mysqltime = $mysqltime + $query[1];
		 
		// The time spent on PHP is the remainder
		$phptime = $totaltime - $mysqltime;
		 
		// Create the percentages
		$mysqlper = number_format_i18n( $mysqltime / $totaltime * 100, 2 );
		$phpper   = number_format_i18n( $phptime / $totaltime * 100, 2 );
		 
		// Output the stats
		echo '<br>';
		
		echo 'Page generated in ' . number_format_i18n( $totaltime, 5 ) . " seconds ( {$phpper}% PHP, {$mysqlper}% MySQL )";
		 
		echo get_num_queries().' queries';
		echo 'MB Peak Memory Used: '.round(memory_get_peak_usage() / 1024 / 1024, 3).'<br />';
	 
	}

}
```

There's a slightly more through one here:
http://roots.io/timing-requests/

----

## I should update this more
Now I've lost track.

## Jquery for printing a section of a page
https://github.com/jasonday/printThis

## Email obfuscation
Used this, but modified
http://wordpress.org/plugins/email-obfuscate-shortcode/
http://techblog.tilllate.com/2008/07/20/ten-methods-to-obfuscate-e-mail-addresses-compared/
http://stackoverflow.com/questions/483212/effective-method-to-hide-email-from-spam-bots
http://stackoverflow.com/questions/769894/how-to-stop-spammers-from-getting-the-email-address-from-a-mailto-link

## Reference for transporting DB
http://webdesignerwall.com/tutorials/exporting-and-importing-wordpress

## Adding a tag automatically on creating a post/publishing a post

```function set_archive_tag_on_publish($post_id,$post) {
  if ($post->post_type == 'andytoday'
    && $post->post_status == 'publish') {
      wp_set_post_tags( $post_id, 'archive', true );
    }
  }
add_action('save_post','set_archive_tag_on_publish',10,2);
```

## Using shortcodes in php templates
http://contactform7.com/faq/#Can_I_embed_a_contact_form_into_my_template_file

## Useful git command for finding deleted files
```git log --diff-filter=D --summary```

## Things I wish notpad++ could do
- Auto-complete html/css syntax/tags

Consider trying sublime text?

## Floats
http://css-tricks.com/containers-dont-clear-floats/

## IE!!

http://stackoverflow.com/questions/15342250/avoid-grey-background-on-ie-10-anchors-links

## Making those custom post type archives

So I got my custom post types for News and Press Releases working, and even got an archive page up. 

It was easy to register the custom post type.
has-archives: yes

Then I had to add two custom functions:
- 
- Rewrites for the archive dates
http://wordpress.stackexchange.com/questions/22992/rewrite-rule-for-custom-post-type-monthly-and-yearly-archive

But I couldn't get the wp_get_archives function to return the right permalink with the right slug. It was returning clientsite.com/2011 when it should return clientsite.com/slug/2011

http://wordpress.stackexchange.com/questions/50530/custom-post-types-wp-get-archives-and-add-rewrite-rule

Crazy ass manual method
http://www.dev4press.com/2012/tutorials/wordpress/practical/url-rewriting-custom-post-types-date-archive/

It seems like a semi-common problem
http://wordpress.stackexchange.com/questions/83797/custom-post-type-yearly-monthly-archive-permalinks

This wasn't very helpful
http://wpadventures.wordpress.com/2011/02/24/custom-post-type-archives-part-4/


http://codex.wordpress.org/Function_Reference/get_query_var
http://codex.wordpress.org/WordPress_Query_Vars

## Purging
http://wordpress.org/support/topic/deleting-post-revisions-do-not-use-the-abc-join-code-you-see-everywhere?replies=3

http://wordpress.org/plugins/revision-control/

http://wordpress.org/plugins/rvg-optimize-database/

## Advanced mode
http://www.stickybeakmedia.com.au/wordpress/wordpress-git-local-staging-production-database-connection/

http://codex.wordpress.org/Running_a_Development_Copy_of_WordPress


## More Roots
http://kalenjohnson.com/customizing-roots-sass/

## Forms

Using WPCF7
http://contactform7.com/loading-javascript-and-stylesheet-only-when-it-is-necessary/

http://www.daobydesign.com/free-plugins/honeypot-module-for-contact-form-7-wordpress-plugin

http://stackoverflow.com/questions/2918707/turn-off-iphone-safari-input-element-rounding

## Shortcodes
http://wp.smashingmagazine.com/2012/05/01/wordpress-shortcodes-complete-guide/

## Performance Optimisations
http://wordpress.org/plugins/debug-objects/

## Deployment
http://webdesignerwall.com/tutorials/exporting-and-importing-wordpress


### GIT FTP DEPLOY
https://github.com/git-ftp/git-ftp

### Ftploy
1 Project, unlimited Deployments is free
Commit -> Deploy. No option to disable.
http://ftploy.com/dashboard

## Maps

This is useful
http://gmaps-samples-v3.googlecode.com/svn/trunk/styledmaps/wizard/index.html

http://viper-7.com/

## .htaccess

For prioritising index.html vs index.php
`DirectoryIndex index.html index.php`

## Rapid Protyping

## Reflections on Grunt

Grunt:
- extremely useful
- catches bad syntax in CSS/JS
- livereload

Nuff said.

----


## Sticky
https://github.com/mojotech/stickymojo

http://davist11.github.io/jQuery-Stickem/

## Hoverintent
http://cherne.net/brian/resources/jquery.hoverIntent.html

http://trentwalton.com/2011/11/18/workspace/
http://trentwalton.com/2011/09/20/unitasking/

http://opentype.info/blog/2012/07/05/webtext-100-percent-width/

http://letteringjs.com/

http://stackoverflow.com/questions/306583/this-selector-and-children/6781092#6781092

http://stackoverflow.com/questions/3654829/jquery-mouse-over-div-slideup-and-mouse-out-div-slidedown
http://jsfiddle.net/nick_craver/JcBAd/

## Admin Changes
Roll this into a plugin
http://www.instantshift.com/2012/03/06/21-most-useful-wordpress-admin-page-hacks/

## Smaller bullets in css

```
	li {
	margin-bottom: 6px;
	position:relative;
	padding-left: 16px;
	list-style: none;
	  } 
	li:before { 
	position: absolute; 
	left: 0; 
	top: 3px; 
	content:"•";
	font-size: 12px;
	}
```

## Smooth scrolling

Do I need:
http://flesler.blogspot.sg/2007/10/jqueryscrollto.html and
http://flesler.blogspot.sg/2007/10/jquerylocalscroll-10.html

or just

```
$(function() {
  $('a[href*=#]:not([href=#])').click(function() {
    if (location.pathname.replace(/^\//,'') == this.pathname.replace(/^\//,'') 
        || location.hostname == this.hostname) {

      var target = $(this.hash);
      target = target.length ? target : $('[name=' + this.hash.slice(1) +']');
      if (target.length) {
        $('html,body').animate({
          scrollTop: target.offset().top
        }, 1000);
        return false;
      }
    }
  });
});
// from http://css-tricks.com/snippets/jquery/smooth-scrolling/
```

## Revisions
http://wpmu.org/wordpress-delete-revisions/

## Stupid chrome text rendering

http://stackoverflow.com/questions/11487427/is-there-any-font-smoothing-in-google-chrome
http://www.dev-metal.com/fix-ugly-font-rendering-google-chrome/
http://www.adtrak.co.uk/blog/font-face-chrome-rendering/
http://blog.typekit.com/2011/01/26/css-properties-that-affect-type-rendering/
http://css-tricks.com/beefing-up-dull-text-in-webkit/

## interesting Flat UI libaries
http://purecss.io/buttons/ 
http://designmodo.github.io/Flat-UI/ 

## jquery show/hide 

Doing Forms
Partly inspired by
http://designshack.net/articles/css/expanding-html5-css3-search-input-field/

This was useful
http://stackoverflow.com/questions/12016725/check-textbox-focus-using-jquery#comment16041973_12016750

Styling placeholder text
http://css-tricks.com/snippets/css/style-placeholder-text/
http://stackoverflow.com/questions/2610497/change-an-inputs-html5-placeholder-color-with-css

IE bugger, inverses my focusin and focusout events
http://stackoverflow.com/questions/12809388/jquery-focus-and-focusout-conflict-in-ie

## Hide Posts from Menu 

Where `$menu_items_to_remove` can be:

- Appearance
- Comments
- Links
- Media
- Pages
- Plugins
- Posts
- Settings
- Tools
- Users

```
function interrobang_remove_menu_items() {

		global $menu;
		$menu_items_to_remove = array(__('Posts'));
		end ($menu);
		while (prev($menu)){
			$value = explode(' ',$menu[key($menu)][0]);
			if(in_array($value[0] != NULL?$value[0]:"" , $menu_items_to_remove)) {
				unset($menu[key($menu)]);
			}
		}
	
}

add_action('admin_menu', 'interrobang_remove_menu_items');
```

(https://managewp.com/wordpress-admin-sidebar-remove-unwanted-items)

## CSS 3 Transitions
http://codepen.io/firya/pen/jqaig
http://thecodeplayer.com/walkthrough/simple-yet-amazing-css3-border-transition-effects

## Logo as image
http://csswizardry.com/2010/10/your-logo-is-an-image-not-a-h1/

http://jsfiddle.net/wHRsq/1/

Gotta sign up for this:
http://www.fonts.com/web-fonts/free-agency-program

## PHP DONE!

I declare the end of php hacking! (Except for some stuff to insert the Contact form, and the search box)

CSS/HTML time!

text-shadow: 0 0 1px rgba(51,51,51,0.2);

----


## Removing whitespace from inline-block elements


On parent:
```
font-size: 0 ; //to remove space in between inline-block elements so they conform to my grid
```

http://www.lifeathighroad.com/web-development/css-web-development/inline-block-whitespace-workaround/

http://www.broken-links.com/2013/03/25/removing-the-whitespace-from-inline-block-elements/

----


## More Looping

This time it's PHP

http://stackoverflow.com/questions/12698135/how-do-i-add-a-class-to-every-nth-item-in-a-php-loop-wordpress

http://stackoverflow.com/questions/7341371/table-tr-each-2-loop-php-html

----


## Php Quotes Syntax

TL:DR: Use single quotes in php and double quotes in HTML.

http://stackoverflow.com/questions/16576116/which-method-is-more-efficient-using-double-quotes-inside-single-quotes-or-esca
http://www.trans4mind.com/personal_development/phpTutorial/quotes.htm

----


## Sanitize
Had to sanitize a string to use as a hash.
`$hash = sanitize_title_with_dashes($title); `

http://codex.wordpress.org/Function_Reference/sanitize_title_with_dashes

----


## The Loop
### 9:22 PM Tuesday, 15 October, 2013

http://codex.wordpress.org/The_Loop#Multiple_Loops

http://wordpress.stackexchange.com/questions/1753/when-should-you-use-wp-query-vs-query-posts-vs-get-posts

http://wp.smashingmagazine.com/2013/01/14/using-wp_query-wordpress/

----


## Debugging
### 8:30 PM Tuesday, 15 October, 2013
Useful debugging code to help in debugging Advanced Custom Fields

This will just output a dump of the data:

```
<?php
echo '<pre>';
    print_r( get_field('your_custom_field_here')  );
echo '</pre>';
die;
?>
```

## granuality
### 7:56 PM Tuesday, 15 October, 2013
Trying to hide the editor for only certain posts:
https://gist.github.com/ramseyp/4060095

## CMS Parts
### 5:48 PM Tuesday, 15 October, 2013
I started out today with a little list of things I wanted to get done:

CMS Parts

- [x] Archives PHP for News and Press Releases

- Home Page Boxes
- Home Page Template PHP

- Portfolio Listing Template PHP

- Test 6 portfolio items
- Test 3-5 news items (in different years)
- Test 3-5 press releases (in different years)
- Test 4 home page boxes

CSS Parts
- Everthing [to be expanded]

I need to square away the CMS parts and 
----


## This is getting out of hand
### 5:16 PM Tuesday, 15 October, 2013
665 lines. I think I need pagination.

http://www.dev4press.com/2012/tutorials/wordpress/practical/debug-wordpress-rewrite-rules-matching/

Archives for News and Press Releases
just set `has_archive = true`! Easy peasy.
http://www.wpbeginner.com/wp-tutorials/how-to-create-a-custom-post-types-archive-page-in-wordpress/
http://thereforei.am/2011/01/12/custom-post-type-archives-in-wordpress-3-1/
http://www.wphub.com/wordpress-3-1-custom-post-type-archives/

But I want nicer urls like www.clientsite/custom-post-type/2011
http://wordpress.org/support/topic/yearly-archives-for-custom-post-types


Then I had to extend wp_get_archives (which generates links) to include custom post types:
http://wpquestions.com/question/showChrono?id=8827

Supposed to use this to add to functions.php:

```
add_filter( "getarchives_where","node_custom_post_type_archive",10,2);

function node_custom_post_type_archive($where, $args)

	{
		$post_type  = isset($args["post_type"]) ? $args["post_type"]  : "post";
		$where = "WHERE post_type = "$post_type" AND post_status = "publish"";

		return $where;  

}
```

But that $where line caused a PHP error. Using this instead

```
 add_filter( 'getarchives_where' , 'ucc_getarchives_where_filter' , 10 , 2 ); 

 function ucc_getarchives_where_filter( $where , $r ) { 

	$args = array( 'public' => true , '_builtin' => false );
    $output = 'names'; 
	$operator = 'and';

	$post_types = get_post_types( $args , $output , $operator ); 
	$post_types = array_merge( $post_types , array( 'post' ) ); 
	$post_types = "'" . implode( "' , '" , $post_types ) . "'";

	return str_replace( "post_type = 'post'" , "post_type IN ( $post_types )" , $where ); 

}
```

Query
```
<?php wp_get_archives(array("post_type" => "custom-post-type", "type" => "monthly")); ?>
```


## Custom Post Type Archives by Date
These are mostly useless
http://wordpress.org/plugins/custom-post-type-archives/
http://www.wphub.com/monthy-custom-post-type-archives/
http://www.dev4press.com/2012/tutorials/wordpress/practical/url-rewriting-custom-post-types-date-archive/


a million confusing posts on stack exchange
http://wordpress.stackexchange.com/questions/33897/custom-post-type-archives-by-year-month
http://wordpress.stackexchange.com/questions/15851/custom-post-type-pagination-when-cpt-rewrite-rule-and-a-page-have-the-same-slu?rq=1
http://wordpress.stackexchange.com/questions/20206/wordpress-rewrite-rules-for-custom-post-type-and-taxonomy?rq=1
http://wordpress.stackexchange.com/questions/83797/custom-post-type-yearly-monthly-archive-permalinks?rq=1

https://gist.github.com/manifestcreative/1263202

Useful Plugin
http://wordpress.org/plugins/duplicate-post/

## Catching Up
### 10:26 AM Tuesday, 15 October, 2013
I'm technically 2 days behind schedule.

To do:
Make 'set featured image' mandatory for Portfolio items.
Add thumbnail support for Portfolio item

How to best handle mailto links
http://stackoverflow.com/questions/483212/effective-method-to-hide-email-from-spam-bots
http://techblog.tilllate.com/2008/07/20/ten-methods-to-obfuscate-e-mail-addresses-compared/

## The Mysterious $post object
http://wordpress.org/support/topic/the-post-object

## Epic Looping

http://stackoverflow.com/questions/665135/find-the-last-element-of-an-array-while-using-a-foreach-loop-in-php

## Roots Template Hierachy

http://codex.wordpress.org/Template_Hierarchy
http://codex.wordpress.org/images/1/18/Template_Hierarchy.png

## qTranslate is one giant hack
### 10:26 PM Sunday, 13 October, 2013
A smart one, but because it is fundamentally a hack it tends to conflict with quite a few things, especially when other plugin authors (rightfully) assume certain default/native behaviour which has been hijacked by qTranslate.

TinyMCE
http://www.qianqin.de/qtranslate/forum/viewtopic.php?f=3&t=3497
alternative: http://wordpress.org/support/topic/qtranslate-with-other-plugins-that-generate-tinymce-blocks

Another problem is that it writes in the wrong content area. I didn't experience it but patched it anyway:
http://old.support.advancedcustomfields.com/discussion/comment/15537
http://www.qianqin.de/qtranslate/forum/viewtopic.php?f=4&t=3436 

----


## Image Sizes
### 8:51 PM Sunday, 13 October, 2013
Used this to create some custom sizes for our client:
http://www.limecanvas.com/adding-custom-image-sizes-to-wordpress-3-5-media-manager/
http://stackoverflow.com/questions/14179524/custom-wordpress-image-size-not-showing-in-3-5-media-manager

Reference
http://codex.wordpress.org/Function_Reference/add_image_size

----


## New Plan
### 8:30 PM Sunday, 13 October, 2013
It's coming along nicely, just too slowly.

The plan is now:

- CMS work and templates today 
- Theming tomorrow, when I'm fresh (and I'm pretty comfortable with it)

Service Category 1

Service Category 2


----

## Custom Post Types
### 5:52 PM Sunday, 13 October, 2013
Custom Post Types are the big deal in WordPress today. They enable developers to easily extend WP from a blogging platform to a do-it-all CMS. However, there are some language, concepts and conventions to pick up.

So I'm creating the Portfolio section of the site. 

I want to namespace my custom post types for this site, as it is best practice to prevent conflicts/corruption. So I go with "bv_portfolio". 

However this will have an effect on the slug/permalink for this post type, it will be `clientsite.com/bv_portfolio/item_1`. I want it to be `clientside.com/portfolio/item_1`.

WP has a rewrite argument for this purpose.

Okay so 
```
Post Type Name: bv_portfolio
Label: Portfolio
Singular Label: Portfolio Item
Description: "Used for the Portfolio section of Bela Vista's website" //this doesn't seem to be used anywhere

I decided to leave the labels array alone, the defaults seem fine for my needs.

Arguments:

Public:	True // would be stupid to set this to false
Show UI:True // unless I want to build my own UI
Has Archive: False // Whether the post type has an index/archive/root page like the "page for posts" for regular posts. If set to TRUE, the post type name will be used for the archive slug.  You can also set this to a string to control the exact name of the archive slug.
Exclude from Search: False // I want it to show up. Double negative...
Capability Type: post // Default, I'll sort capabilities out later
Hierarchical: False // Not needed 
Rewrite: True // Handle URLs
Custom Rewrite Slug: portfolio //I need this to not be 'bv_portfolio'. It defaults to Post Type Name
With Front: True // Not sure what this does actually, leaving at default
Query Var: True // Defaults to Post Type Name, which I think is what I want
Menu Position: 6 // Before 'Media'
Show in Menu: True // Duh. Interestingly I can nest the menu under another, which means I can easily create, say a "Bela Vista" top level menu and have other menus nested under it.
Menu Icon: null // To be customised later
Supports: Title, Editor, Exerpt, Author, Thumbnail (featured image), custom-fields, revisions,  NO Trackbacks, Comments, Attributes, Post-Formats

```

This was a useful resource:
https://gist.github.com/justintadlock/6552000

More resources:
http://wp.smashingmagazine.com/2012/11/08/complete-guide-custom-post-types/
http://css-tricks.com/creating-meet-team-page-wordpress/

----


## Basic structure of containers done, now for individual templates
### 2:15 PM Sunday, 13 October, 2013

Roots uses this theme wrapper idea which makes it very modular and slightly confusing, but reduces the amount of code you write, and is easier to update, once you get your head around the nesting. (http://roots.io/an-introduction-to-the-roots-theme-wrapper/)

Managed to 'integrate' qTranslate, ACF, and Roots. Made a Custom Field for the intro paragraph that appears on every page (in both languages) and let the template display based on the current language. Neat. Commit. [With the help of a forum post](http://old.support.advancedcustomfields.com/discussion/2684/php-question-qtranslate/p1)

I have a few things to figure out:

- How to handle the Services page (and allow for auto hash linking)
- How to handle the 3 boxes on the home page (as a custom post type, one post for each box and let the user select which posts to use, or all in one page?)


Enhancements:
http://wordpress.org/plugins/codepress-admin-columns/



## Getting the basic structure
### 1:23 PM Sunday, 13 October, 2013

Editing base.php, header.php, footer.php to remove Bootstrap containers and structure the output HTML to my liking.

Took a while to decide what structure I wanted my output to have.
http://stackoverflow.com/questions/4781077/html5-best-practices-section-header-aside-article-tags

I realize that what I'm removing from Roots is basically most of Bootstrap. The integration goes -a little- too deep for my liking. So this goes back to me wanting to strip down Roots to basically a HTML5BP theme. I might do that sometime as a separate project. (Or learn/use enough of Bootstrap that I don't have or want to)

I should check out this [WP Super Cache](http://wordpress.org/plugins/wp-super-cache/) plugin, I think it does what I want it to in terms of generating static HTML files and serving up those instead. Most sites I create don't have any dynamically loaded content or comments anyway. Only question is how does it work with forms. Maybe use in tandem with [WP-HTML-Compression](http://wordpress.org/plugins/wp-html-compression/faq/)

**Read up on using IDs sometime**

- http://2002-2012.mattwilcox.net/archive/entry/id/1054/
- http://screwlewse.com/2010/07/dont-use-id-selectors-in-css/
- http://oli.jp/2011/ids/

----


## Bootstrap.less reduction
### 6:50 PM Saturday, 12 October, 2013
Took me longer than I expected to whittle down the bootstrap.less import lines down to what I wanted to keep. 

I also removed Bootstrap JS files that I didn't want to use from `js/plugins/bootstrap`. 

I could have thrown out everything but I guess I wanted to familarize myself with what Bootstrap has to offer. That became quite distracting.
http://jquery.malsup.com/cycle2/
`affix.js` - Use for the left scrolling (so that it doesn't overscroll the bottom) on Portfolio pages
`carousel.js` - Keep for now, may replace with [cycle2](http://jquery.malsup.com/cycle2/). 
`scrollspy.js` - It seems a bit unnecessary, but I can use it to highlight the nav bar based on what is currently in view. I might use it on the Contact page (as they have a "Join Us" link on the main nav that is actually an anchor hash to contact#joinus)
`transition.js` - Dependency for effects for the above

**Kickstrap**
This is crazy. It's like everything and the kitchen sink.http://getkickstrap.com/

The next step is to actually start 'theming'. Ahem.

----


## Progress
### 5:25 PM Saturday, 12 October, 2013
Man, I keep getting sidetracked.

Installed Disable Feeds plugin, which turns off RSS generation. I hope to put this in my own "Static Sites" plugin someday, together with a few other things.

----


## Less
### 5:17 PM Saturday, 12 October, 2013
Roots uses LESS, which meant that I had to get syntax highlighting for notepad ++. Used this. https://github.com/azrafe7/LESS-for-Notepad-plusplus

Grunt means I don't have to use [Prepros](http://alphapixels.com/prepros/), or any other CodeKit-like software to watch folders and compile. Basically CodeKit/Prepros is a gui for what grunt does.

Prepros does have some features worth exploring sometime though:

- Live Refresh
- Multi device testing
- 1 click FTP Deployment


----


## Grunt for Roots
### 3:49 PM Saturday, 12 October, 2013
I'm installing the dependencies grunt for roots needs by running `npm install` from a command prompt from the roots theme directory. Seems to work fine.

Next step is to activate Roots from within the WordPress admin.

#### Security
Making note of something here for security: 
I want to change `/wp-admin` to something else, but I'll have to check that it doesn't break the rewrites that Roots makes (which is likely)
http://codex.wordpress.org/Giving_WordPress_Its_Own_Directory
http://codex.wordpress.org/Editing_wp-config.php

Also I should change the database prefix
http://www.siteground.com/tutorials/wordpress/wordpress_security.htm


#### Additional things to do
Actually I should create a checklist for: 

- Security
- Performance
	- custom modernizr.js
	- disable feeds
		- either with a plugin
		- or with
		
		```
		function fb_disable_feed() {
		wp_die( __('No feed available,please visit our <a href="'. get_bloginfo('url') .'">homepage</a>!') );
		}

		add_action('do_feed', 'fb_disable_feed', 1);
		add_action('do_feed_rdf', 'fb_disable_feed', 1);
		add_action('do_feed_rss', 'fb_disable_feed', 1);
		add_action('do_feed_rss2', 'fb_disable_feed', 1);
		add_action('do_feed_atom', 'fb_disable_feed', 1);
		add_action('do_feed_rss2_comments', 'fb_disable_feed', 1);
		add_action('do_feed_atom_comments', 'fb_disable_feed', 1);
		```
								
	-


Anyway the catch-all list for now:

- Disable RSS feeds
- More security optimisations - http://www.labnol.org/internet/wordpress-optimization-guide/3931/
- This is interesting http://wordpress.org/plugins/google-authenticator/

This plugin might be useful in the future. http://wordpress.org/plugins/remove-link-url/installation/

---- 


## Submodule not required
### 3:44 PM Saturday, 12 October, 2013
That was quite a distraction. After looking closely at the Roots files, there wasn't much to strip out to create a 'bare' version that I will build off. It's already pretty bare. 

Just for logging, what I did was:
- created a new folder in `/themes` called roots-stripped
- created a new repo in bitbucket
- init a new git repo locally and set the remote to bitbucket
- pushed up an unchanged Roots 6.5.0

I was worried about possible conflicts nesting git repos, as I basically had a repo for the whole project and another repo in `/wp-content/themes/roots-stripped`. It seemed to work though, the master repo basically treated the nested repo like it was invisible (fine by me, as I was going to create a theme for bela vista by copying the roots-stripped into `/themes/belavista` when I was done with the stripping.

Oh well, what a git adventure. I used the command line for some of it, just to reduce the level of intimidation it gives me.

Also, Roots isnt exactly meant to work well with child themes. http://alittlecode.com/roots-wordpress-theme-customization-hack-the-original-or-child-theme-it/

Okay so I'm back to developing in `/themes/belavista`. Work starts now. 

----


## Working Roots
### 3:02 PM Saturday, 12 October, 2013
I often do this, and I don't want to do it again, so I've decided I'm going to set up a git subrepo for my stripped version of Roots. Sounds like fun.

----


## Back to the Roots
### 12:31 PM Saturday, 12 October, 2013

#### Roots
I've decided to go back to the Roots starter theme. (http://roots.io/) 

I've used it before, it's the king of best practices for Wordpress. It's a starter theme based on HTML5BP and Twitter Bootstrap (that I should really get around to playing with), two epic best practice/jumpstart projects.

Roots has the following features:
- Minimal, accessible markkup - Based off HTML5BP with ARIA roles and microformats
- Cleaned up wordpress output aggressively
- Theme Wrapper - Write less code
- Comes with Bootstrap (optional)
- Theme Activation does a while bunch of things
- Clean URLs
- Automated workflow[with Grunt](http://roots.io/using-grunt-for-wordpress-theme-development/)
- It used to come with .htaccess from HTML5BP, but that is now in a [plugin](https://github.com/roots/wp-h5bp-htaccess)

A whole bunch of useful stuff, more here: http://roots.io/features/

#### Grunt
Roots has had some sort of build script for some time, which, due to my adversion to CLIs, I've never used. But now that I want to develop a more streamlined, future-process, and use a CSS preprocessor (write less code, DRY), I figured it's a good time.

The Roots buildscript uses Grunt, which is built on Node.js. I had to use npm, the Node package manager, to install it, and since I didn't have npm, I had to insteal Node.js, which I've always wanted to play with. http://nodejs.org/.

NodeJS has a fancy .msi installer, which saved me a huge amount of hassle and I was able to get (aside from a cranky internet connection which made me have to download the .msi three times) node and npm in my cmd prompt easily.

Then to install Grunt, I just had to run `npm install -g grunt`, which installs all the dependencies that Grunt needs, and Grunt itself. http://gruntjs.com/getting-started

Grunt promises the following:
>  The less work you have to do when performing repetitive tasks like minification, compilation, unit testing, linting, etc, the easier your job becomes. After you've configured it, a task runner can do most of that mundane work for you - and your team - with basically zero effort.

There's a million plugins available which help with doing other things, no time to explore now. http://gruntjs.com/plugins

It's all a bit above me, and all I want to/should be doing right now is to get Roots on my Wordpress install, use the script to compile my LESS or whatever and combine/minify my JS, and get down to work. 

The downside of having intellectual curiousity. (Actually that's not a good excuse, I should just learn to manage it and be able to have a high intellectual curiousity and get shit done.)

I'm going to save some node.js basics here to play with when I get the time:
- http://dailyjs.com/2012/05/03/windows-and-node-1/

#### More tools
To look at when I have the time
- [Vagrant](http://www.vagrantup.com/) - Helps create virtual deployment environments on your local computer
- [Composer](http://roots.io/using-composer-with-wordpress/) - Some sort of PHP package manager

----


## Getting Distracted
#### 10:15 AM Saturday, 12 October, 2013
I'm installing launchy now, as I realize that I spend quite a bit of time on my computer navigating to specific files/folders, and I often find myself wanting to go to "Bela Vista" folder, for example, and having to navigate through my folder structure. This is annoying and wastes time. Shortcuts will only partially solve this problem as they clutter up the desktop and are hard to scan through for a particular folder. I should probably have done this a long time ago. It requires configuration though, which takes up time. For now I'll just add two of my working folders to it's index/catalog and let it index those.

http://www.petersmittenaar.com/launchy-why-and-how-to-use-it-effectively

Also I should use Rescuetime (http://www.petersmittenaar.com/rescuetime-why-and-how-to-use-it-effectively)

I've also decided to ditch the whole idea of theme frameworks. I just don't see much benefit to be gained. 

Maybe after I get over the learning curve and learn and understand how to use one properly, it might save me time. But in the context of this project, I think it's unlikely.

I wanted to use Thesis for the drag and drop editor, thinking it would save me time. Instead:

- The drag and drop editor is not easy to use
- They don't follow established Wordpress "best practices" (not sure how else to phrase this). 
	- They save templates in the database?
	- I can't edit the CSS outside of using their in-browser editor
	- They don't use child themese, instead using their own lingo of "Skins"
	- Many settings are buried in their own control panel
- The code generated by Thesis is not to my liking, and I can't find an easy way to change it
- It's expensive. $250sgd + $40-50usd per site. Urghh.

Looking at Genesis, here are the main features they claim on [their site](http://www.studiopress.com/features) and how I feel I won't gain from them:

- SEO
	- I can install SEO plugins separately and not have them tied to the theme
	- although Schema.org code is a great idea for websites that have blogs/rich content associated with them.
- Responsive HTML5 designs 
	- I like my HTML5 markup to be based on the HTML5 Boilerplate, which Genesis doesn't seem to use. 
	- Nothing wrong with that, it's just that I'm used to the HTML5BP and its collection of best practices.
	- This project doesn't need to be responsive, also. All the Genesis child themes (some of which look quite solid) are 
- Unlimited everything
	- This basically means it's great value, buy once, use on multiple sites, unlimited updates and support
	- This is great, but only if I want to use it for its features. No point having great value in something I won't use.
- Security
	- This is great, but I want to know what exactly they do to secure your Wordpress installation/what best practices they follow.
	- Perhaps this warrants dissecting the theme to see what they do
- Instant Updates
	- Nothing to shout about
- Customizable and Fast
	- Customizable - This doesn't affect me as I mostly hardcode my sites and my client's don't expect to change options frequently or at all.
	- Fast - This remains to be proven. I can't help but feel that running a large theme such as geneis will have some performance loss vs using native wordpress theming. The questions is whether the benefits outweigh the slight performance hit.
- Custom Widgets, Layout Optioons
	-  Basically not very applicable to me
- Developers you can trust
	- Uh. I trust myself.

Basically it sounds like these theme frameworks are more for consumer-level bloggers and less for developers like myself. I do know, however, that many people build on top of Genesis. [Such as this guy](http://www.billerickson.net/)


## #%#$&Y#&%#%@#! Thesis
### 7:17 PM Friday, 11 October, 2013

I'm gonna try using Genesis instead.

I'm not even sure why I must/should use a framework. 

What an incredibly frustrating day.

----

## Learning about Thesis
### 4:01 PM Friday, 11 October, 2013
Late start to the day.

I figure I should get a basic page up and in the right theme before I start with all the Custom Post Types and whatnot.

I'd also lke to use SASS to streamline CSS work. 

Fiddling around with Thesis.

So far it's been rather annoying, I HAVE to use their built-in editor to edit the skin and even the CSS file. When I try to edit the css file manually it doesn't seem to do anything. When I create or modify templates there are no .php files generated or created. It seems that it saves it to the database, or somewhere, I don't know.

I was hoping that Thesis gives me a GUI to edit wordpress template files, something I used to do manually and was error-prone and slow. Instead it seems to do everything in its own schema, saving things in its own way. What an extremely douchily written thing.

It's all extremely lock-in. 

I don't understand why they can't use the built in, native wordpress features.

Also, it's annoying to be developing when my browser (chrome) keeps crashing and the internet connection is slow/error-prone. I miss working on a mac.

----

## Scheduling
### 6:06 PM Thursday, 10 October, 2013
I'm done for the day, but there's a lot to do.

This is the todo list for the next few days:

#### 11 Oct #####

- Register Custom Post Types
- Register Custom Fields
- HTML/CSS Templates for the following pages:
	- Home
	- About
	
#### 12 Oct ####

- HTML/CSS Templates for:
	- Portfolio
	- News
	- Press Releases

#### 13 Oct ####

- HTML/CSS Templates for:
	- Contact (including form)
- Chinese Typography

	
Everything needs to be done by 14th October, Monday. This leaves 15th October, Tuesday, for testing and remaining bugfixes/optimisations and then client training/content population on 16th October, Wednesday.

----


## on Logging
### 5:59 PM Thursday, 10 October, 2013
I realize I should just log more frequent, shorter updates. I guess what's a little annoying is that notepad++ doesn't have a shortcut for the TextFX Insert --> Date and Time Long Format. 

Okay I just created one. That wasn't too hard.

And I tend to leave my log entries unfinished. I should just log, and get out of here and back to work. 

----


## More Plugins
### 5:57 PM Thursday, 10 October, 2013
Added the Custom Post Type UI Plugin. This helps register Custom Post Types in Wordpress. Normally you have to use php code to do this, but this just gives you an easy GUI to do it. You can even opt for it to show you the generated code and plug that in yourself instead of having it register for you.

Disabled W3 Total Cache, optimization and SEO will be done towards the end of the project.

----

## Back on track
### 5:42 PM Thursday, 10 October, 2013
Managed to solve the "Undefined index: language" errors. This whole qTranslate debacle has thrown me off track and set progress back.

I used this to fix it, wasn't sure how to use a .patch file (I googled it, but it seemed complicated and urghh CLI tools again) so I just manually read it using common sense and made the changes in a text editor.
http://dl.dropboxusercontent.com/u/304233/wp-qtranslate-notices.patch

I saved the file out as well, not sure how long that will stay on dropbox.

----


## Enabling Plugins and Configuration
### 4:37 PM Thursday, 10 October, 2013
God, my internet connection is being cranky and its affecting my plugin downloading/installing as I keep downloading incomplete/partial archives, etc.

And I got a stupid error with qTranslate on the admin panel:
```Notice: Undefined index: pl in wp-content\plugins\qtranslate\qtranslate_configuration.php on line 621```

The plugin still seems to work regardless, so I'm just going to ignore it for now.

I might need this at a later time: http://wordpress.org/plugins/qtranslate-slug/screenshots/

Configured qTranslate for 2 languages, English and Mandarin, 

qTranslate also doesn't seem to play well with W3 total cache. Getting a whole bunch of "Undefined index: language" errors on the top of my admin screen. Apparently these won't show if I'm not in wordpress's "Debug Mode', which is cool.

Tried this fix but it didn't seem to do much:
http://www.qianqin.de/qtranslate/forum/viewtopic.php?f=3&t=1569

----


## Wordpress Vanilla, Plugins 
### 3:36 PM Thursday, 10 October, 2013
So I've created some semblance of a git/version-controlled setup to start developing. [Git Workflow Log](gitworkflow.md). 

Next step was to unzip Wordpress 3.6.1 into the folder, set up a database (Using phpMyAdmin, but I hope to just use the shell in the future, as my command-line-fu improves. If I have full control over the server environment, there's actually no need to install phpMyAdmin. The less things you have running, the better for security and simplicity.)

Apparently Wordpress 3.7 onwards will self-update, which is pretty awesome (as long as it doesn't break any plugins or themes). 

Then, the following plugins:

- Advanced Custom Fields - Seems to be the leading plugin for what I used to do semi-manually in functions.php, defining custom fields for content.
- Disable Comments - This can disable comments across the site, automatically hiding all comment-related features from the admin panel, and even has a "Persistent Mode" which hard-kills the comments in the database, which is good if you know you never ever want comments at all on a site.
- qTranslate - This seems to be competing with WPML for the leading multi-lingual plugin. It's written by a chinese guy (I think. AZN! Represent!) and seems to be really solid. While installing this I realize that quite a number of people
- W3 Total Cache - For performance. I would love to do more research into whether this is the best option, but it's used by many leading sites, so I trust that they've already done that. It has a ton of options to set and learn about.

If I'm not wrong I still need to set up the following things:

- Custom Content Types - Either using a plugin (preferred) or manually
- Gallery Manager - This site has a image slider used in the portfolio section, so I'll need to find the least-feature-packed yet most supported plugin to support this. (I don't like "everything and the kitchen sink" style plugins, as they add bloat. Bloat is evil.)
- Some SEO Plugin - I may or may not need this based on how Thesis handles SEO.

If I have time I'll explore the following

- jsdelivr - Free CDN for javascript http://wordpress.org/plugins/jsdelivr-wordpress-cdn-plugin/

I also need to choose a foundation/framework theme. There are a ton of them out there, I'm going to try Thesis as someone else recommended it, and I don't have the time to do through research now, maybe in the future. What I am looking for here, besides a solid HTML PHP theme framework to build upon, is a GUI to do theming work from the Wordpress back end admin area itself. I think this reduces the possibility for human error. (Assuming it's well written and bug-free, it'll always produce typo-free workable code, whereas manually editing files may introduce typos and naming errors). It's also less tedious and easier to work with, leading to higher productivity. 

----


## Gathering Tools
### 2:46 PM Thursday, 10 October, 2013
I always spend a little too much time on this part. An impending client deadline forces me to focus, which is good.

One of the things I love about web design is that the whole industry moves so quickly, there are new  best practices popping up all the time. It's great, as you get this feeling of worldwide collaboration, all striving towards perfection.

The downside, I suppose, is that seemingly each time I build a site I am also using a brand new workflow. (I should probably be creating websites more regularly, 3 wordpress sites in 2 years isn't particularly good for sustaining a lifestyle)

This time round I've got another project round the corner, so I am trying to learn as much as I can and build/design a relatively future-proof workflow. The core objectives would be:

- Version Controlled (git)
- Reusable Chunks of Code (I've recently learnt about custom plugins, which means I can put useful snippets of things that I used to put in the theme's functions.php file into a plugin instead, facilitating cross-site reuse. Perhaps I can even build out a proper plugin with selectable options in the future.)
- Following best practice for building out a multi-lingual site with custom post types and custom content areas. (This will be of interest to many clients)
- Documentation (such as this log) for future reference/better learning

I tend to spend a lot of time researching all possible options and find it hard to commit to one. Decision paralysis. Sometimes I wish there weren't so many competing offers in tech, and you could just go with a sensible default. Like HTML5 boilerplate. Or buying a mac.

----


## The Plan
### 2:02 PM Thursday, 10 October, 2013
So I outlned, briefly, the key steps/milestones to the completion of the site. This is all in the lead up to content population next Thursday, 17th October.

**Steps to Bela Vista Site**

- git/wordpress workflow (1d)
- vanilla wordpress installation (1h)
- base theme selection and installation (6h)
- plugins (3h)
	- Advanced Custom Fields (for custom fields)
	- qTranslate (for dual-language http://www.qianqin.de/qtranslate/forum/viewtopic.php?f=3&t=3)
	- contact form 7 (http://contactform7.com/contact-form-in-your-language/) http://wordpress.org/plugins/contact-form-7-phone-mask-module/faq/
- integration of ACF and qTranslate (4h)


- set up custom content types
	- portfolio
		- title
		- sub-title
		- overview
		- services
		- quotes/testimonials
		- photo gallery
		- project details
	- news
		- html content
		- exerpt
		- pdf
	- press releases
		- html content
		- exerpt
		- pdf
	
	- all posts will have
		- large headline text
	
- create a `<hr>` that uses the symbol we are using on the site http://codex.wordpress.org/TinyMCE_Custom_Buttons

- HTML/CSS Templates
	- Home Page 4h
	- About Page 2h
	- Portfolio Landing Page 3h
	- Portfolio Details Page 4h
	- News/Press Release Page 3h
	- News/Press Release Details Page 2h
	- Contact Page 3h
	- Search Results 3h
	
- Set up static pages
	- Home Page
	- About
	- Contact
	- News
	- Press Releases

- Chinese Typography (4h) 

- Contact Form
	
	
- SEO
	- title tags
	- meta desc for whole website
	- keywords

- test wordpress/mysql on BV server (set up "Production" environment) - 1h



http://www.snipercapital.com/zh-hans
http://www.snipercapital.com/en

http://watersidemacau.com/zh-hans/
http://watersidemacau.com/zh-hant/
http://watersidemacau.com/

http://www.apaclogistics.com/cs/
http://www.apaclogistics.com/en/

