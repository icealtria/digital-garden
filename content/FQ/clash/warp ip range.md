`whois -h whois.radb.net -- '-i origin AS13335' | grep -Eo "([0-9.]+){4}/[0-9]+" > cloudflare_ranges.txt`
