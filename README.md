MyPHPIPS
--------

MyPHPIPS (MyPHP Intrusion Prevention System) is an open source PHP Web Application Intrusion Prevention System. It was based on PHPIDS (phpids.org) and distributed under the LGPL License. This work is supported by CyberSecurity? Malaysia.

MyPHPIPS intends to assist the web developer/maintainers to secure their PHP CMS/application deployments without having with minimal resources (i.e time and money)

MyPHPIPS is a portable and less-hassle framework that serves as an extra security layer to defend against invalid/malicious requests to the web application or content management systems.

### Installation

1. Go to the directory where the configuration file is located
2. Upload the whole IDS folder (and the content) there
3. Look for your configuration file. Usually:
* Joomla: configuration.php
* Wordpress: wp-config.php
* Drupal: sites/default/settings.php
* phpBB: config.php
* myBB: inc/config.php
4. Edit your config file, add the following lines and make sure it is within <?php    ?> code tag (if the is not database configuration file, use header/index file):

        define('MyPHPIPS', dirname(__FILE__).'/IDS/');
        require_once(MyPHPIPS.'MyPHPIPS.php');

5. Change the 'cache' folder permission inside the IDS folder so that it is writable
6. Test your installation with some attack :- http://www.example.com/yourcms/?page_id=../../../etc/passwd