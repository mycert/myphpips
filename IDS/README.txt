1) Go to the directory where the configuration file is located
2) Upload the whole IDS folder (and the content) there
3) Look for your configuration file. Usually:
  a) Joomla: configuration.php
  b) Wordpress: wp-config.php
  c) Drupal: sites/default/settings.php
  d) phpBB: config.php
  e) myBB: inc/config.php
4) Edit your config file, add the following lines and make sure it is within <?php    ?> code tag (if the is not database configuration file, use header/index file):

    define('MyPHPIPS', dirname(__FILE__).'/IDS/');
    require_once(MyPHPIPS.'MyPHPIPS.php');

5) Change the 'cache' folder permission inside the IDS folder so that it is writable
6) Test your installation with some attack :- http://www.example.com/yourcms/?page_id=../../../etc/passwd