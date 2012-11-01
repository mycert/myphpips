* Go to the directory where the configuration file is located
* Upload the whole IDS folder (and the content) there
* Look for your configuration file. Usually:
 * Joomla: configuration.php
 * Wordpress: wp-config.php
 * Drupal: sites/default/settings.php
 * phpBB: config.php
 * myBB: inc/config.php
* Edit your config file, add the following lines and make sure it is within <?php    ?> code tag (if the is not database configuration file, use header/index file):

    define('MyPHPIPS', dirname(__FILE__).'/IDS/');
    require_once(MyPHPIPS.'MyPHPIPS.php');

* Change the 'cache' folder permission inside the IDS folder so that it is writable
* Test your installation with some attack :- http://www.example.com/yourcms/?page_id=../../../etc/passwd