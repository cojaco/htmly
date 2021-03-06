HTMLy
=====

HTMLy is an open source databaseless, blogging platform that prioritizes simplicity and speed (Flat-File Blog). HTMLy can be referred to as a Flat-File CMS, since it will also manage your content.

You do not need to use a VPS to run HTMLy, shared hosting or even free hosting should work as long as the host supports at least PHP 5.3.

Features
---------
- Admin Panel
- Markdown editor with live preview
- Categorization with tags (multiple tagging support)
- Static Pages (e.g. Contact Page, About Page)
- Meta canonical, description, and rich snippets for SEO
- Pagination
- Author Page
- Multi author support
- Social Links
- Disqus Comments (optional)
- Facebook Comments (optional)
- Google Analytics
- Built-in Search
- Related Posts
- Per Post Navigation (previous and next post)
- Body class for easy theming
- Breadcrumb
- Archive page (by year, year-month, or year-month-day)
- JSON API
- OPML
- RSS Feed
- RSS 2.0 Importer (basic)
- Sitemap.xml
- Archive and Tag Cloud Widget
- SEO Friendly URLs
- Teaser thumbnail for images and Youtube videos
- Responsive Design
- Lightbox
- User Roles
- Online Backup
- File Caching
- Auto Update

Requirements
------------
HTMLy requires PHP 5.3 or greater.

Installations
-------------
If you have OpenSSL on your server, use the [installer](https://github.com/Kanti/htmly-installer/releases/latest) and read the following [instructions](https://github.com/Kanti/htmly-installer/blob/master/README.md#htmly-installerphp) to get started.
If you don't have OpenSSL, please download the latest version, extract it, then upload the extracted files to your server. Also, make sure the installation folder is writeable by your server.

Configurations
--------------
Rename `config.ini.example` inside the `config` folder to `config.ini` (or you can create a new `config/config.ini` file) then change the site settings there.

Create `YourUsername.ini` inside the `config/users` folder or simply rename the `username.ini.example` file and write down your password there:

````cfg
password = YourPassword
````

In addition, HTMLy support admin user role. To do so, simply add the following line to your choosen user:

````cfg
role = admin
````

Users assigned with the admin role can edit/delete all users' posts.

To access the admin panel, add `/login` to the end of your site's URL.
e.g. `www.yoursite.com/login`

### Lighttpd
The following is an example configuration for lighttpd:

````php
$HTTP["url"] =~ "^/config" {
  url.access-deny = ( "" )
}
$HTTP["url"] =~ "^/system/includes" {
  url.access-deny = ( "" )
}
$HTTP["url"] =~ "^/system/admin/views" {
  url.access-deny = ( "" )
}

url.rewrite-once = (
  "^/(themes|system|vendor)/(.*)" => "$0",
  "^/(.*\.php)" => "$0",

  # Everything else is handles by htmly
  "^/(.*)$" => "/index.php/$1"
)
````

### Nginx
The following is a basic configuration for Nginx:

````nginx
server {
  listen 80;

  server_name example.com www.example.com;
  root /usr/share/nginx/html;

  access_log /var/log/nginx/access.log;
  error_log /var/log/nginx/error.log error;

  index index.php;

  location ~ /config/ {
     deny all;
  }

  location / {
    try_files $uri $uri/ /index.php?$args;
  }

  location ~ \.php$ {
        fastcgi_pass   127.0.0.1:9000;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME   $document_root$fastcgi_script_name;
        include        fastcgi_params;
  }
}
````

Both Online or Offline
----------------------
The built-in editor found in the admin panel, also provides you the ability to write to Markdown files offline by uploading them (see naming convention below) into the `content/username/blog` folder (the `username` must match `YourUsername.ini` above). 

For static pages you can upload it to the `content/static` folder.

File Naming Convention
----------------------
When you write a blog post and save it via the admin panel, HTMLy automatically create a .md file extension with the following name, example:

````
2014-01-31-12-56-40_tag1,tag2,tag3_databaseless-blogging-platform-flat-file-blog.md
````

Here's the explanation (separated by an underscore):

- `2014-01-31-12-56-40` is the published date. The date format is `yyyy-mm-dd-hh-mm-ss`
- `tag1,tag2,tag3` are the tags, separated by commas
- `databaseless-blogging-platform-flat-file-blog` is the URL
	
For static pages, use the following format:

````
content/static/about.md
````

In the example above, the `/about.md` creates the URL:  
`www.yourblog.com/about`

Thus, if you write/create files offline, you must name the .md file in the format above.

For static subpages, use the following format:

````
content/static/about/me.md
````

This will create the URL:  
`www.yourblog.com/about/me`

Content Title
-------------
If you are writing offline, to create a title for your post, wrap the title with an HTML comment and a `t` on both side.

```html
<!--t Title t-->
````  

Example of how your post would look like:
```html
<!--t Here is the post title t-->

Paragraph 1

Paragraph 2 etc.
```


Demo
----
Visit [HTMLy Demo](http://demo.htmly.com).

Credit
------
People who give references and inspiration for HTMLy:
* [Martin Angelov](http://tutorialzine.com)

Contribute
----------
1. Fork and edit
2. Submit pull request for consideration

Contributors
----------
- [danpros](https://github.com/danpros) - [Weblog](http://www.danpros.com)
- [Kanti](https://github.com/Kanti) - [Weblog](https://kanti.de)
- [fahmi182](https://github.com/fahmi182) - [Weblog](http://ifahmi.com)
- [fanningert](https://github.com/fanningert) - [Weblog](http://thomas.fanninger.at)
- [BlackCodec](https://github.com/BlackCodec)
- [mlncn](https://github.com/mlncn)

Copyright / License
-------------------
For copyright notice please read [COPYRIGHT.txt](https://github.com/danpros/htmly/blob/master/COPYRIGHT.txt). HTMLy is licensed under the GNU General Public License Version 2.0 (or later).
