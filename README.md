
PHP Caching library
----
PageCache is a lightweight PHP library for full page cache, works out of the box with zero configuration. 
Use it when you need a simple yet powerful file based PHP caching solution. Page caching for mobile devices is built-in.

Install PHP PageCache and start caching your PHP's browser output code using Composer:
```
composer require mmamedov/page-cache
```
Or manually add to your composer.json file:
```json
{
  "require": {
      "mmamedov/page-cache": "^2.0"
  }
}
```
Once PageCache is installed, include Composer's autoload.php file, or implement your own autoloader. 
Composer autoloader is recommended.

Do not use `master` branch, as it may contain unstable code, use versioned branches instead.

No Database calls
----
Once page is cached, there are no more database calls needed! Even if your page contains many database calls and complex logic, 
it will be executed once and cached for period you specify. No more overload!

This is a very efficient and simple method, to cache your most visited dynamic pages. 

Why another PHP Caching class?
----
Short answer - simplicity. If you want to include a couple lines of code on top of your dynamic PHP pages and be able 
to cache them fully, then PageCache is for you. No worrying about cache file name setup for each URL, no worries 
about your dynamically generated URL parameters and changing URLs. PageCache detects those changed and caches accordingly.

PageCache also detects $_SESSION changes and caches those pages correctly. This is useful if you have user 
authentication enabled on your site, and page contents change per user login while URL remains the same.

Lots of caching solutions focus on keyword-based approach, where you need to setup a keyword for your 
content (be it a full page cache, or a variable, etc.). There are great packages for keyword based approach. 
One could also use a more complex solution like a cache proxy, Varnish. 
PageCache on the other hand is a simple full page only caching solution, that does exactly what its name says - 
generates page cache in PHP.   

###### Random early and late expiration
Using random logarithmic calculations, producing sometimes negative and at times positive results, cache expiration
for each client hitting the same URL at the same time is going to be different. While some clients might still get
the same cache expiration value as others, overall distribution of cache expiration value among clients is random.

Making pages expire randomly at most 6 seconds before or after actual cache expiration of the page, ensures that we have
less clients trying to regenerate cache content. File locking already takes care of simultaneous writes of cache page, 
random expiration takes it a step further minimizing the number of such required attempts. 

To give an example, consider you have set expiration to 10 minutes `config()->setCacheExpirationInSeconds(600)`. 
Page will expire for some clients in 594 seconds, for some in 606 seconds, and for some in 600 seconds. 
Actual page expiration is going to be anywhere  in between 594 and 606 seconds inclusive, this is randomly calculated. 
Expiration value is not an integer internally, so there are a lot more of random expiration values than you can think of. 


That's it!

