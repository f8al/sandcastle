# Change Log
All notable changes to the Sandcastle script will be documented in this file.

## 1.2.0 – 2017-04-09
- Sandcastle now supports the `-f` argument (text file)
	* The script defaults to `bucket-names.txt` if one is not given
- Sandcastle now presents a line count for the specified text file
- Adjusted ASCII header art and script wording

## 1.1.0 – 2017-04-09
- Sandcastle now distinguishes between bucket status codes
	* Buckets returning 404 are hidden by default
	* Other status codes are displayed as potential "matches"
- Sandcastle script and documentation improvements
- Established `CHANGELOG.md` for update tracking

## 1.0.0 – 2017-04-08
- Initial public release of the optimised bucketCrawler script
- Initial `README.md` documentation and bucket permutations