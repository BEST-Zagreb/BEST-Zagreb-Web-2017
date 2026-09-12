# BEST Zagreb website, 2017 edition (retired)

Static archive of best.hr as it ran from August 2017 to spring 2018: WordPress 4.9 with the Avada theme and Polylang, 8 pages in Croatian, 5 in English (under `en/`) and 11 news posts (mostly partner presentations), the last of them from 2018-05-16. In April 2018 a fresh Avada install replaced it; that later site is archived as [BEST-Zagreb-Web-2021](https://github.com/BEST-Zagreb/BEST-Zagreb-Web-2021) and the current site as [BEST-Zagreb-Web](https://github.com/BEST-Zagreb/BEST-Zagreb-Web). It was rebuilt from the backup a former maintainer left on the server in July 2018 (a MySQL data directory and the web root, found during the 2026 server retirement), not from a live site, and it is complete: every page the database listed as published is here except the two member-list pages left out on purpose (see below). Every page is plain HTML; there is no database, no PHP and nothing to keep patched.

Home: **https://2017.best.hr/** (the site ran at **www.best.hr**)

- 24 published pages, 464 files, 35.1 MB
- Verified: every page and asset requested over HTTP, 351 URLs, **0 failures**, at the root and under a sub-path
- Verified: every page rendered in a browser, 1 broken image (see below)
- Verified: after the deliberate changes below, the visible text and image list of every page match the 2018 install running in a container

## Looking at it locally

    python3 -m http.server 8000

Then open <http://127.0.0.1:8000/>. Any static file server works.

## How it was made

The 2018 database was started in a MySQL 5.7 container and the 2018 web root in a WordPress 4.9 container with PHP 7.2, the site's address rewritten to the container. The page list came from the database, not from what a crawler happened to find; the site was mirrored with `wget`, every page refetched raw, relinked to relative paths, and compared page by page with the container. Everything that would ask a server for something was stripped: feed, oEmbed, REST, RSD, shortlink and manifest links, the embed and comment-reply scripts, the comment forms. Google Analytics, Google Fonts, YouTube embeds and the other third-party loads the original pages made are kept. The tooling and the logs live in the migration notes alongside this archive.

## What deliberately differs from the 2018 pages

### Personal contact details

On the contact pages, 6 named people's e-mail addresses (12 occurrences) were replaced with **board@best.hr** and every phone number was removed (25 occurrences, including the office landline). Names stay. This archive is public and outlives the students named in it.

### Repairs and limits

Four things were changed in the database copy before crawling, none of them in the backup itself:

- The install used query-string addresses (`?p=123`), which cannot exist as static files, so the standard `/%postname%/` permalink structure was switched on; Polylang then serves the English pages under `en/`.
- The "Članovi" and "Members" pages (a list of member names) were left out.
- The 12 lorem-ipsum FAQ and portfolio rows of the 2012 Avada demo import were left out; nothing linked to them. Three posts dated 2012 under demo slugs (`class-aptent-...`, `donec-at-mauris-...`, `praesent-et-urna-...`) carry real 2017 texts (Boršč, Zoo Zagreb, winter seminar applications) and are kept.
- The theme printed a PHP 7 `count()` warning above every menu; PHP display of errors was switched off, which is how the 2018 server ran.

Eight related-post thumbnails (500x383) were zero-byte files in the backup, so the 2018 pages showed them broken; they were regenerated from the original logos. The "Projekti" page links to project pages of the pre-2017 best.hr (`dani-inzenjera/2006`, `summer-course/2003` and so on); those pages were already gone in 2018 and the links still point at best.hr, where they answer 404. One image on that page (`page_attachments/0000/0331/BCD-hallway_small.jpg`) is from the same era and is missing. The search form points at this archive's own root; a static copy cannot search. Avada is a paid theme; its files are included only so the archive renders and should not be reused elsewhere.

## Editions

best.hr editions on the web: 2017 (this repository), [2021.best.hr](https://2021.best.hr/) ([BEST-Zagreb-Web-2021](https://github.com/BEST-Zagreb/BEST-Zagreb-Web-2021)), the current site at [best.hr](https://best.hr/) ([BEST-Zagreb-Web](https://github.com/BEST-Zagreb/BEST-Zagreb-Web)). Earlier eras (2003 to mid 2017) exist only in the Wayback Machine.

## Hosting

Live at <https://2017.best.hr/>, served by Cloudflare Workers as static files straight from this repository. Every push to `main` is deployed by Workers Builds within a minute or two. Every page carries an archive notice and a `noindex` header, added at the edge by `banner.js`, so search engines keep sending people to the current site; the archived files themselves are untouched.

## Wayback Machine

This edition ran at <http://www.best.hr/>; the Internet Archive's calendar for it is <https://web.archive.org/web/*/www.best.hr*>, with captures from the period of this edition where the crawler reached them. This repository is the complete copy; the archive is a partial, independent second copy.

## Licence

The content, images and copy belong to BEST Zagreb. Third-party theme and plugin assets under `wp-content/` remain under their own licences and are included only because the pages need them to render as they originally did.
