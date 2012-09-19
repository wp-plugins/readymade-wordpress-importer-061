=== Plugin Name ===
Contributors: readymadeweb
Donate link: 
Tags: importer, wordpress, typepad, movabletype, attachments, import, uploads, transfer
Requires at least: 3.0
Tested up to: 3.4
Stable tag: 0.6

Import posts, pages, comments, custom fields, categories, tags and more from a WordPress export file.

== Description ==

The ReadyMade WordPress Importer is a branch of the default WordPress importer. This version modifies the default in two ways:

1. If there is an attachment in the WXR and the importer is not able to determine the file type from the file name (ie missing extension), the patched version will make a light (body-less) request to the web server where the file is hosted for information we can use about the file. The things we're interested in are file type, size, and filename.
1. If the importer is processing an attachment under the above situation, and it is able to determine the file type, then it will rewrite the local version of the file to have the appropriate file extension.

ReadyMadeWeb developed this plugin in the process of creating a service to convert TypePad data to WXR formatted files.  During this process we've encountered some unique problems with TypePad data. Namely, many TypePad files, particularly images, are saved without file extensions. This prevents the default WordPress importer from importing those files into the wp-content/uploads folder. By adding a MIME type detection as a fallback, we prevent many files from being excluded from the import process.

== Installation ==

The quickest method for installing the importer is:

1. Upload the `readymade-wordpress-importer` folder to the `/wp-content/plugins/` directory
1. Activate the plugin through the 'Plugins' menu in WordPress
1. Go to the Tools -> Import screen, click on 'ReadyMade WordPress Importer'

== Changelog ==

= 0.6.2 =
* Reads MIME Type for files without proper file extensions


== Upgrade Notice ==

= 0.6.2
* Reads MIME Type for files without proper file extensions

== Frequently Asked Questions ==

= Help! I'm getting out of memory errors or a blank screen. =
If your exported file is very large, the import script may run into your host's configured memory limit for PHP.

A message like "Fatal error: Allowed memory size of 8388608 bytes exhausted" indicates that the script can't successfully import your XML file under the current PHP memory limit. If you have access to the php.ini file, you can manually increase the limit; if you do not (your WordPress installation is hosted on a shared server, for instance), you might have to break your exported XML file into several smaller pieces and run the import script one at a time.

For those with shared hosting, the best alternative may be to consult hosting support to determine the safest approach for running the import. A host may be willing to temporarily lift the memory limit and/or run the process directly from their end.

-- [WordPress Codex: Importing Content](http://codex.wordpress.org/Importing_Content#Before_Importing)

== Filters ==

Like the WordPress importer, ReadyMade WordPress Importer has filters that allow you to completely enable/block certain features:

* `import_allow_create_users`: return false if you only want to allow mapping to existing users
* `import_allow_fetch_attachments`: return false if you do not wish to allow importing and downloading of attachments
* `import_attachment_size_limit`: return an integer value for the maximum file size in bytes to save (default is 0, which is unlimited)

There are also a few actions available to hook into:

* `import_start`: occurs after the export file has been uploaded and author import settings have been chosen
* `import_end`: called after the last output from the importer
