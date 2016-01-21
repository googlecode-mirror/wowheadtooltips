The following instructions only apply if you're using [phpBB3 Portal](http://www.phpbb3portal.com/).

  * Open `./portal/includes/functions.php` and look for the following line (it should be near the top of the page):
```
include($phpbb_root_path . 'includes/message_parser.'.$phpEx);
```
  * Immediately after it add:
```
include_once($phpbb_root_path . 'wowhead/parse.php');
```
  * Next, inside the same file, look for the following lines:
```
// Parse the message and subject
$message = censor_text($row['post_text']);
$message = str_replace("\n", '<br />', $message);
```
  * Immediately after it add:
```
$message = whp_parse($message);
```
  * Save and close `functions.php` and reupload it to your website, as needed.
  * You may or may not have to clear your cache, I'm not sure if the cache is used by the portal.
  * That's it, you're done.  Enjoy!