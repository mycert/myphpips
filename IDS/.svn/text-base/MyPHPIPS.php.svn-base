<?php

/**
 * MyPHPIPS (Based on PHPIDS) - v0.1.0.7 Alpha
 * http://code.google.com/p/myphpips/
 *
 * PHPIPS is free software; you can redistribute it and/or modify
 * it under the terms of the GNU Lesser General Public License as published by
 * the Free Software Foundation, version 3 of the License, or
 * (at your option) any later version.
 *
 * MyPHPIPS is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
 * GNU Lesser General Public License for more details.
 *
 * You should have received a copy of the GNU Lesser General Public License
 * along with PHPIDS. If not, see <http://www.gnu.org/licenses/>.
 *
 * PHP version 5.1.6+
 *
 * @MyPHPIPS author   Adnan bin Mohd Shukor <adnan@cybersecurity.my>
 * @PHPIDS author     Mario Heiderich <mario.heiderich@gmail.com>
 * @PHPIDS author     Christian Matthies <ch0012@gmail.com>
 * @PHPIDS author     Lars Strojny <lars@strojny.net>
 * @license  http://www.gnu.org/licenses/lgpl.html LGPL
 */

if ( !defined('IDSPATH') )
        define('IDSPATH', dirname(__FILE__) . '/');
require_once(IDSPATH . 'Init.php');
require_once(IDSPATH . 'Config.php');

if(!isset($MyPHPIPS_cache_path))
   $MyPHPIPS_cache_path = "cache";

if(isset($MyPHPIPS_blocking_mode))
   switch($MyPHPIPS_blocking_mode)
   {
      case "aggressive":
         $MyPHPIPS_blocking_mode = "aggressive";
      default:
         $MyPHPIPS_blocking_mode = "normal";
   }
else
   $MyPHPIPS_blocking_mode = "normal";

if(isset($MyPHPIPS_request_mode))
   switch($MyPHPIPS_request_mode)
   {
      case "aggressive":
         $MyPHPIPS_request_mode = "aggressive";
      default:
         $MyPHPIPS_request_mode = "normal";
   }
else
   $MyPHPIPS_request_mode = "normal";

try {

    if($MyPHPIPS_request_mode == "aggressive")
       $request = array('REQUEST' => $_REQUEST, 'COOKIE' => $_COOKIE);
    else
       $request = array('REQUEST' => $_REQUEST);

    $init = IDS_Init::init(IDSPATH . 'CoreConf.php');

    $init->config['General']['base_path'] = IDSPATH ;
    $init->config['General']['use_base_path'] = true;
    $init->config['General']['tmp_path'] = $MyPHPIPS_cache_path;
    if($MyPHPIPS_blocking_mode == "aggressive")
       $init->config['General']['filter_path'] = 'default_filter.xml';

    $MyPHPIPS_ids = new IDS_Monitor($request, $init);
    $MyPHPIPS_result = $MyPHPIPS_ids->run();

    if (!$MyPHPIPS_result->isEmpty()) {
        $MyPHPIPS_Tags = $MyPHPIPS_result->getTags();

    $MyPHPIPS_err403 = false;
	$MyPHPIPS_high_impact = false;

	foreach($MyPHPIPS_Tags as $impact)
	   if($impact == "dt" || $impact == "rfe" || $impact == "lfi" || $impact == "sqli" || $impact == "id")
	      $MyPHPIPS_high_impact = true;

	if($MyPHPIPS_result->getImpact() > $MyPHPIPS_impact_threshold)
	   if(($MyPHPIPS_blocking_mode == "normal" && $MyPHPIPS_high_impact) || $MyPHPIPS_blocking_mode == "aggressive")
	      $MyPHPIPS_err403 = true;

	if($MyPHPIPS_err403)
        {
           header('HTTP/1.1 403 Forbidden');
           die($MyPHPIPS_error_message);
        }
    }
} catch (Exception $e) {
    /*
    * sth went terribly wrong - maybe the
    * filter rules weren't found?
    */
    printf(
        'An error occured: %s',
        $e->getMessage()
    );
}
