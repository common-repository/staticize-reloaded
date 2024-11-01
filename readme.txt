=== Staticize Reloaded ===
Tags: caching, performance
Contributors: matt, billzeller

Staticize Reloaded is a plugin to make your site faster by caching the output of some WordPress pages. It creates a unique key based on the page variables and user and then if a request is made with identical variables it serves the request from a static file rather than building the page from the database. When a post is updated or a comment is left the cache is cleared. It is ideal for sites with a lot of anonymous reads and not too many updates. (For example, during a Slashdotting.)

== Installation ==

1. Upload to your plugins folder, usually `wp-content/plugins/`
2. If you have Compression turned on under Miscellaneous options, turn it off
3. Activate the plugin on the plugin screen
4. Caching should begin immediately. It's a good idea to deactivate when making template changes. To flush the cache just edit a post or comment.

== Frequently Asked Questions ==

= Do I really need to use this plugin? =

Probably not, WordPress is fast enough that caching usually only adds a few milliseconds of performance that isn't really perceptible by users. Some reasons you may want to use Staticize Reloaded:

* If your site gets Slashdotted
* If you're on a very slow server
* If you've had a complaint from your host about performance

= How can I tell if it's working? =

Staticize Reloaded adds some stats to the very end of a page in the HTML, so you can view source to see the time it took to generate a page and rather it was cached or not. Remember that the cache is created on demand, so the first time you load a page it'll be generated from the database.

= I see gibberish on the screen when I activate this plugin? =

Make sure that you deactivated compression on the Miscellaneous options screen and that gzip encoding is turned off on the PHP level

= How do I make certain parts of the page stay dynamic? =

There are two ways to do this, you can have functions that say dynamic or include entire other files. To have a dynamic function in the cached PHP page use this syntax around the function:

`<!--mfunc function_name('parameter', 'another_parameter') -->
<?php function_name('parameter', 'another_parameter') ?>
<!--/mfunc-->`

The HTML comments around the mirrored PHP allow it to be executed in the static page. To include another file try this:

`<!--mclude file.php-->
<?php include_once(ABSPATH . 'file.php'); ?>
<!--/mclude-->`

That will include file.php under the ABSPATH directory, which is the same as where your `wp-config.php` file is located.

== Screenshots ==

1. This is a chart showing the performance of a WordPress blog under very high loads with and without Staticize. It was taken from <a href="http://weblogtoolscollection.com/archives/2004/07/26/staticise-analysis/">this post</a>.
