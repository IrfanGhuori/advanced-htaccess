

# Don't Copy this Readme file download from the repository

######  BEGIN cPanel-generated php ini directives, do not edit
######  Manual editing of this file may result in unexpected behavior.
######  To make changes to this file, use the cPanel MultiPHP INI Editor (Home >> Software >> MultiPHP INI Editor)
######  For more information, read our documentation (https://go.cpanel.net/EA4ModifyINI)
######  END cPanel-generated php ini directives, do not edit

######  ----------------------------------------------------------------------
######  | Cross-origin images                                                |
######  ----------------------------------------------------------------------
######  Send the CORS header for images when browsers request it.

<IfModule mod_setenvif.c>
    <IfModule mod_headers.c>
        <FilesMatch "\.(bmp|cur|gif|ico|jpe?g|a?png|svgz?|webp)$">
            SetEnvIf Origin ":" IS_CORS
            Header set Access-Control-Allow-Origin "*" env=IS_CORS
        </FilesMatch>
    </IfModule>
</IfModule>

######  ----------------------------------------------------------------------
######  | Cross-origin web fonts Allow cross-origin access to web fonts.   |
######  ----------------------------------------------------------------------

<IfModule mod_headers.c>
    <FilesMatch "\.(eot|otf|tt[cf]|woff2?)$">
        Header set Access-Control-Allow-Origin "*"
    </FilesMatch>
</IfModule>

######  Show 404 Pages
ErrorDocument 404 /404

######  ----------------------------------------------------------------------
######  | Error prevention  Disable the pattern matching based on filenames.  |
######  ----------------------------------------------------------------------
Options -MultiViews

######  ----------------------------------------------------------------------
######  | Document modes                                                     |
######  ----------------------------------------------------------------------
<IfModule mod_headers.c>
    Header always set X-UA-Compatible "IE=edge" "expr=%{CONTENT_TYPE} =~ m#text/html#i"
</IfModule>

######  ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### #
######  ######  MEDIA TYPES AND CHARACTER ENCODINGS                                #
######  ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### ###### #

######  ----------------------------------------------------------------------
######  | Media types                                                        |
######  ----------------------------------------------------------------------

<IfModule mod_mime.c>

  ######  Data interchange

    AddType application/atom+xml                        atom
    AddType application/json                            json map topojson
    AddType application/ld+json                         jsonld
    AddType application/rss+xml                         rss
    AddType application/geo+json                        geojson
    AddType application/rdf+xml                         rdf
    AddType application/xml                             xml


  ######  JavaScript
    AddType text/javascript                             js mjs


  ######  Manifest files

    AddType application/manifest+json                   webmanifest
    AddType application/x-web-app-manifest+json         webapp
    AddType text/cache-manifest                         appcache


  ######  Media files

    AddType audio/mp4                                   f4a f4b m4a
    AddType audio/ogg                                   oga ogg opus
    AddType image/bmp                                   bmp
    AddType image/svg+xml                               svg svgz
    AddType image/webp                                  webp
    AddType video/mp4                                   f4v f4p m4v mp4
    AddType video/ogg                                   ogv
    AddType video/webm                                  webm
    AddType video/x-flv                                 flv

    AddType image/x-icon                                cur ico


  ######  WebAssembly

    AddType application/wasm                            wasm


  ######  Web fonts

    AddType font/woff                                   woff
    AddType font/woff2                                  woff2
    AddType application/vnd.ms-fontobject               eot
    AddType font/ttf                                    ttf
    AddType font/collection                             ttc
    AddType font/otf                                    otf


  ######  Other

    AddType application/octet-stream                    safariextz
    AddType application/x-bb-appworld                   bbaw
    AddType application/x-chrome-extension              crx
    AddType application/x-opera-extension               oex
    AddType application/x-xpinstall                     xpi
    AddType text/calendar                               ics
    AddType text/markdown                               markdown md
    AddType text/vcard                                  vcard vcf
    AddType text/vnd.rim.location.xloc                  xloc
    AddType text/vtt                                    vtt
    AddType text/x-component                            htc

</IfModule>

######  ----------------------------------------------------------------------
######  | Character encodings                                                |
######  ----------------------------------------------------------------------

AddDefaultCharset utf-8
<IfModule mod_mime.c>
    AddCharset utf-8 .appcache \
                     .bbaw \
                     .css \
                     .htc \
                     .ics \
                     .js \
                     .json \
                     .manifest \
                     .map \
                     .markdown \
                     .md \
                     .mjs \
                     .topojson \
                     .vtt \
                     .vcard \
                     .vcf \
                     .webmanifest \
                     .xloc
</IfModule>

######  ----------------------------------------------------------------------
######  | Rewrite engine                                                     |
######  ----------------------------------------------------------------------

<IfModule mod_rewrite.c>

    ######  (1)

    RewriteEngine On

    ######  (2)

    Options +FollowSymlinks

    ######  (3)
    
    ######  Options +SymLinksIfOwnerMatch

    ######  (4)
    ######  RewriteBase /

    ######  (5)
    ######  RewriteOptions <options>

</IfModule>

<IfModule mod_rewrite.c>

    RewriteEngine On

    ######  (1)
    RewriteCond %{HTTPS} =on
    RewriteRule ^ - [E=PROTO:https]
    RewriteCond %{HTTPS} !=on
    RewriteRule ^ - [E=PROTO:http]

    ######  (2)
    ######  RewriteCond %{HTTPS} !=on

    RewriteCond %{HTTP_HOST} ^www\.(.+)$ [NC]
    RewriteRule ^ %{ENV:PROTO}://%1%{REQUEST_URI} [R=301,L]

</IfModule> 

######  ----------------------------------------------------------------------
######  | File access                                                        |
######  ----------------------------------------------------------------------

<IfModule mod_autoindex.c>
    Options -Indexes
</IfModule>

<IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteCond %{REQUEST_URI} "!(^|/)\.well-known/([^./]+./?)+$" [NC]
    RewriteCond %{SCRIPT_FILENAME} -d [OR]
    RewriteCond %{SCRIPT_FILENAME} -f
    RewriteRule "(^|/)\." - [F]
</IfModule>

<IfModule mod_authz_core.c>
    <FilesMatch "(^#.*#|\.(bak|conf|dist|fla|in[ci]|log|orig|psd|sh|sql|sw[op])|~)$">
        Require all denied
    </FilesMatch>
</IfModule>

<IfModule mod_headers.c>
    Header always set X-Content-Type-Options "nosniff"
</IfModule>

######  ----------------------------------------------------------------------
######  | Cross-Site Scripting (XSS) Protection                              |
######  ----------------------------------------------------------------------
<IfModule mod_headers.c>
    Header unset X-Powered-By
    Header always unset X-Powered-By
</IfModule>

ServerSignature Off

######  ----------------------------------------------------------------------
######  | Compression                                                        |
######  ----------------------------------------------------------------------

<IfModule mod_deflate.c>

   <IfModule mod_setenvif.c>
        <IfModule mod_headers.c>
            SetEnvIfNoCase ^(Accept-EncodXng|X-cept-Encoding|X{15}|~{15}|-{15})$ ^((gzip|deflate)\s*,?\s*)+|[X~-]{4,13}$ HAVE_Accept-Encoding
            RequestHeader append Accept-Encoding "gzip,deflate" env=HAVE_Accept-Encoding
        </IfModule>
    </IfModule>
        <IfModule mod_mime.c>
        AddEncoding gzip              svgz
    </IfModule>

</IfModule>

######  ----------------------------------------------------------------------
######  | Cache expiration                                                   |
######  ----------------------------------------------------------------------

######  Serve resources with a far-future expiration date.

######  (!) If you don't control versioning with filename-based cache busting, you
######  should consider lowering the cache times to something like one week.

######  https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control
######  https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Expires
######  https://httpd.apache.org/docs/current/mod/mod_expires.html

<IfModule mod_expires.c>

    ExpiresActive on
    ExpiresDefault                                      "access plus 1 month"

  ######  CSS

    ExpiresByType text/css                              "access plus 1 year"


  ######  Data interchange

    ExpiresByType application/atom+xml                  "access plus 1 hour"
    ExpiresByType application/rdf+xml                   "access plus 1 hour"
    ExpiresByType application/rss+xml                   "access plus 1 hour"

    ExpiresByType application/json                      "access plus 0 seconds"
    ExpiresByType application/ld+json                   "access plus 0 seconds"
    ExpiresByType application/schema+json               "access plus 0 seconds"
    ExpiresByType application/geo+json                  "access plus 0 seconds"
    ExpiresByType application/xml                       "access plus 0 seconds"
    ExpiresByType text/calendar                         "access plus 0 seconds"
    ExpiresByType text/xml                              "access plus 0 seconds"


  ######  Favicon (cannot be renamed!) and cursor images

    ExpiresByType image/vnd.microsoft.icon              "access plus 1 week"
    ExpiresByType image/x-icon                          "access plus 1 week"

  ######  HTML

    ExpiresByType text/html                             "access plus 0 seconds"


  ######  JavaScript

    ExpiresByType application/javascript                "access plus 1 year"
    ExpiresByType application/x-javascript              "access plus 1 year"
    ExpiresByType text/javascript                       "access plus 1 year"


  ######  Manifest files

    ExpiresByType application/manifest+json             "access plus 1 week"
    ExpiresByType application/x-web-app-manifest+json   "access plus 0 seconds"
    ExpiresByType text/cache-manifest                   "access plus 0 seconds"


  ######  Markdown

    ExpiresByType text/markdown                         "access plus 0 seconds"


  ######  Media files

    ExpiresByType audio/ogg                             "access plus 1 month"
    ExpiresByType image/apng                            "access plus 1 month"
    ExpiresByType image/bmp                             "access plus 1 month"
    ExpiresByType image/gif                             "access plus 1 month"
    ExpiresByType image/jpeg                            "access plus 1 month"
    ExpiresByType image/png                             "access plus 1 month"
    ExpiresByType image/svg+xml                         "access plus 1 month"
    ExpiresByType image/webp                            "access plus 1 month"
    ExpiresByType video/mp4                             "access plus 1 month"
    ExpiresByType video/ogg                             "access plus 1 month"
    ExpiresByType video/webm                            "access plus 1 month"


  ######  WebAssembly

    ExpiresByType application/wasm                      "access plus 1 year"


  ######  Web fonts

    ######  Collection
    ExpiresByType font/collection                       "access plus 1 month"

    ######  Embedded OpenType (EOT)
    ExpiresByType application/vnd.ms-fontobject         "access plus 1 month"
    ExpiresByType font/eot                              "access plus 1 month"

    ######  OpenType
    ExpiresByType font/opentype                         "access plus 1 month"
    ExpiresByType font/otf                              "access plus 1 month"

    ######  TrueType
    ExpiresByType application/x-font-ttf                "access plus 1 month"
    ExpiresByType font/ttf                              "access plus 1 month"

    ######  Web Open Font Format (WOFF) 1.0
    ExpiresByType application/font-woff                 "access plus 1 month"
    ExpiresByType application/x-font-woff               "access plus 1 month"
    ExpiresByType font/woff                             "access plus 1 month"

    ######  Web Open Font Format (WOFF) 2.0
    ExpiresByType application/font-woff2                "access plus 1 month"
    ExpiresByType font/woff2                            "access plus 1 month"


  ######  Other

    ExpiresByType text/x-cross-domain-policy            "access plus 1 week"

</IfModule>
<IfModule mod_rewrite.c>
RewriteEngine on 
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME}\.php -f
RewriteRule ^(.*)$ $1.php [NC,L]

RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME}\.html -f
RewriteRule ^(.*)$ $1.html [NC,L]

RewriteCond %{HTTPS} off
RewriteCond %{HTTP:X-Forwarded-SSL} !on
RewriteCond %{HTTP_HOST} ^YourWebDomain\.com$ [OR]
RewriteCond %{HTTP_HOST} ^www\.YourWebDomain\.com$
RewriteRule ^/?$ "https\:\/\/YourWebDomain\.com\/" [R=301,L]
</IfModule>













