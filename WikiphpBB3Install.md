# phpBB3 Installation Instructions #

  * Download the zip file from http://code.google.com/p/wowheadtooltips/downloads/list
  * Unzip the folder and open the file `config.php`.  Change these settings to your liking; more information on each setting is provided inside `config.php`.
  * Upload the `wowhead` folder to the base directory of your phpBB installation.
  * Upload `wowhead.css` file to the `./styles/<your style>/theme/` folder of your phpBB installation, where <your style> is the name of the theme you use.
  * Open `./includes/functions_content.php`, located relative to your phpBB installation.
    * Find:
```
/**
* @ignore
*/
if (!defined('IN_PHPBB'))
{
	exit;
}
```
    * Immediately after add:
```
require_once($phpbb_root_path . '/wowhead/parse.php');
```
    * Then, find the following code (somewhere around line 671):
```
function bbcode_nl2br($text)
{
	// custom BBCodes might contain carriage returns so they
	// are not converted into <br /> so now revert that
	$text = str_replace(array("\n", "\r"), array('<br />', "\n"), $text);
	return $text;
}
```
    * After:
```
$text = str_replace(array("\n", "\r"), array('<br />', "\n"), $text);
```
    * Add:
```
$text = whp_parse($text);
```
  * Save and close and reupload to your website as necessary.

  * Open `./styles/<your style>/template/overall_header.html` and add the following lines inside of the 

&lt;head&gt;



&lt;/head&gt;

 tags.
```
<!-- Wowhead Item Links -->
<link href="{T_THEME_PATH}/wowhead.css" rel="stylesheet" type="text/css" />
<script src="http://www.wowhead.com/widgets/power.js"></script>
```
  * Save and close the file and reupload it to your website as needed.

  * **Do this step only if you intend on using item cache.** Point your browser to `create_table.php`, located in the "wowhead" directory you uploaded earlier.  This script will create the necessary MySQL table inside the database that you specified inside of `config.php`.  After the script tells you it has completed the operation then you may delete `create_table.php` and `table_scheme.php`.
  * Goto your admin control panel aka ACP, and clear your cache.
  * That's it, you're done.  Told you it wasn't that bad.