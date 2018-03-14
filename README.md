# diskover - File system crawler, storage search engine and analytics powered by Elasticsearch

[![License](https://img.shields.io/github/license/shirosaidev/diskover.svg?label=License&maxAge=86400)](./LICENSE)
[![Release](https://img.shields.io/github/release/shirosaidev/diskover.svg?label=Release&maxAge=60)](https://github.com/shirosaidev/diskover/releases/latest)
[![Donate Patreon](https://img.shields.io/badge/Donate%20%24-Patreon-brightgreen.svg)](https://www.patreon.com/diskover)
[![Donate PayPal](https://img.shields.io/badge/Donate%20%24-PayPal-brightgreen.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=CLF223XAS4W72)

<img align="left" width="249" height="189" src="docs/diskover.png?raw=true" hspace="5" vspace="5" alt="diskover">

diskover is an open source file system crawler and disk usage software that uses [Elasticsearch](https://www.elastic.co) to index and manage data across heterogeneous storage systems. Using diskover, you are able to more effectively search and organize files and system administrators are able to manage storage infrastructure, efficiently provision storage, monitor and report on storage use, and effectively make decisions about new infrastructure purchases.

As the amount of file data generated by business' continues to expand, the stress on expensive storage infrastructure, users and system administrators, and IT budgets continues to grow.

Using diskover, users can identify old and unused files and give better insights into data change, file duplication and wasted space.

diskover is written and maintained by Chris Park (shirosai) and runs on Linux and OS X/macOS using Python 2/3.

<div align="center"><img src="https://github.com/shirosaidev/diskover/blob/master/docs/diskover-diagram1.png?raw=true" alt="diskover diagram" width="800" height="525"/></div>

## Screenshots

[diskover-web](https://github.com/shirosaidev/diskover-web) (diskover's web file manager, analytics app, file system search engine, rest-api)<br>
<img align="left" width="400" src="https://github.com/shirosaidev/diskover-web/raw/master/docs/diskover-web-dashboard-screenshot.png?raw=true" alt="diskover-web dashboard">
<img align="left" width="400" src="https://github.com/shirosaidev/diskover-web/raw/master/docs/diskover-web-filetree-screenshot.png?raw=true" alt="diskover-web file tree">
<img align="left" width="400" src="https://github.com/shirosaidev/diskover-web/raw/master/docs/diskover-web-advancedsearch-screenshot.png?raw=true" alt="diskover-web advanced search">
<img width="400" src="https://github.com/shirosaidev/diskover-web/raw/master/docs/diskover-web-tags-screenshot.png?raw=true" alt="diskover-web tags"><br>
Kibana dashboards/saved searches/visualizations and support for Gource<br>
<img align="left" width="400" src="docs/kibana-dashboarddark2-screenshot.png?raw=true" alt="kibana-screenshot">
<img width="400" src="docs/diskover-gource1-screenshot.png?raw=true" alt="diskover-gource">

### diskover Gource videos

<a href="https://youtu.be/InlfK8GQ-kM"><img align="left" width="400" src="https://img.youtube.com/vi/InlfK8GQ-kM/0.jpg" alt="gource video"></a>
<a href="https://youtu.be/qKLJjZ0TMqA"><img width="400" src="https://img.youtube.com/vi/qKLJjZ0TMqA/0.jpg" alt="gource video"></a>

## Installation Guide

### Requirements

* `Linux or OS X/macOS` (tested on OS X 10.11.6, Ubuntu 16.04)
* `Python 2.7. or Python 3.5.` (tested on Python 2.7.14, 3.5.3)
* `Python elasticsearch client module`
* `Python requests module`
* `Python scandir module`
* `Python progressbar2 module`
* `Python blessings module`
* `Elasticsearch 5` (local or [AWS ES Service](https://aws.amazon.com/elasticsearch-service/), tested on Elasticsearch 5.4.2, 5.6.4) Elasticsearch 6 is not supported yet.
Install the above Python modules using pip.

### Optional Installs

* [diskover-web](https://github.com/shirosaidev/diskover-web) (diskover's web file manager and analytics app)
* [sharesniffer](https://github.com/shirosaidev/sharesniffer) (for scanning your network for file shares and auto-mounting for crawls)
* [GNU parallel](https://www.gnu.org/software/parallel/) (for running parallel diskover crawls using diskover-mp.sh)
* [Kibana](https://www.elastic.co/products/kibana) (for visualizing Elasticsearch data, tested on Kibana 5.4.2, 5.6.4)
* [X-Pack](https://www.elastic.co/downloads/x-pack) (Kibana plugin for graphs, reports, monitoring and http auth)
* [Gource](http://gource.io) (for Gource visualizations of diskover Elasticsearch data, see videos above)

### Download

```sh
$ git clone https://github.com/shirosaidev/diskover.git
$ cd diskover
```

[Download latest version](https://github.com/shirosaidev/diskover/releases/latest)

### Requirements

You need to have at least **Python 2.7. or Python 3.5.** and have installed required Python dependencies using `pip`.

```sh
$ pip install -r requirements.txt
```

## Getting Started

Start diskover with:

```sh
$ cd /path/you/want/to/crawl
$ python /path/to/diskover.py
```

**Defaults for crawl with no flags is to index from . (current directory) and files >0 Bytes and 0 days modified time. Empty files and directores are skipped (unless you use -s 0 and -e flags). Use -h to see cli options.**

A successfull crawl should look like this:

```
   ___       ___       ___       ___       ___       ___       ___       ___
  /\  \     /\  \     /\  \     /\__\     /\  \     /\__\     /\  \     /\  \
 /::\  \   _\:\  \   /::\  \   /:/ _/_   /::\  \   /:/ _/_   /::\  \   /::\  \
/:/\:\__\ /\/::\__\ /\:\:\__\ /::-"\__\ /:/\:\__\ |::L/\__\ /::\:\__\ /::\:\__\
\:\/:/  / \::/\/__/ \:\:\/__/ \;:;-",-" \:\/:/  / |::::/  / \:\:\/  / \;:::/  /
 \::/  /   \:\__\    \::/  /   |:|  |    \::/  /   L;;/__/   \:\/  /   |:\/__/
  \/__/     \/__/     \/__/     \|__|     \/__/    v1.4.1     \/__/     \|__|
                                      https://shirosaidev.github.io/diskover
                                      Bringing light to the darkness.
                                      Support diskover on Patreon :)

    
2017-12-20 15:08:41,664 [INFO][diskover] Connecting to Elasticsearch
2017-12-20 15:08:41,676 [INFO][diskover] Checking ES index: diskover-index
2017-12-20 15:08:41,680 [WARNING][diskover] ES index exists, deleting
2017-12-20 15:08:41,968 [INFO][diskover] Creating ES index
2017-12-20 15:08:42,192 [INFO][diskover] Adding disk space info to ES index
2017-12-20 15:08:42,197 [INFO][diskover] Starting crawl using 20 threads
Crawling: 100%|████████████████████| 10147/10147 [0h:00m:00s, 322.7 dir/s]
2017-12-20 15:09:13,107 [INFO][diskover] Finished crawling

********************************* CRAWL STATS *********************************
 Directories: 10147 / Skipped: 92
 Files: 64267 (54.01 GB) / Skipped: 1211 (46.21 GB)
 Elapsed time: 0h:00m:31s
*******************************************************************************
```

## User Guide

[Read the wiki](https://github.com/shirosaidev/diskover/wiki) for more documentation on how to use diskover.

## Discussions/Questions

For discussions or questions about diskover, please ask on [Google Group](https://groups.google.com/forum/?hl=en#!forum/diskover).

## Bugs

For bugs about diskover, please use the [issues page](https://github.com/shirosaidev/diskover/issues).

## Donations

To continue developing diskover and keep making it better, please consider supporting my work on [Patreon](https://www.patreon.com/diskover) or [PayPal](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=CLF223XAS4W72). Thank you so much to all the users and supporters.

## License

See the [license file](https://github.com/shirosaidev/diskover/blob/master/LICENSE).
