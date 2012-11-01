; <?php die(); ?>

; PHPIDS Config.ini

; General configuration settings


[General]

    ; basic settings - customize to make the PHPIDS work at all
    filter_type     = xml
    
    base_path       = /full/path/to/IDS/ 
    use_base_path   = false
    
    filter_path     = mycert_filter.xml
    tmp_path        = cache
    scan_keys       = false
    
    ; define which fields contain html and need preparation before 
    ; hitting the PHPIDS rules (new in PHPIDS 0.5)
    html[]          = POST.__wysiwyg
    
    ; define which fields contain JSON data and should be treated as such 
    ; for fewer false positives (new in PHPIDS 0.5.3)
    json[]          = POST.__jsondata

    ; define which fields shouldn't be monitored (a[b]=c should be referenced via a.b)
    exceptions[]    = GET.__utmz
    exceptions[]    = GET.__utmc

    ; you can use regular expressions for wildcard exceptions - example: /.*foo/i

    ; PHPIDS should run with PHP 5.1.2 but this is untested - set 
    ; this value to force compatibilty with minor versions
    min_php_version = 5.1.6

