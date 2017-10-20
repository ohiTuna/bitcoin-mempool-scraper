
# Tradeblock mempool scraper

Gets the last week of mempool data, giving snapshots at 10 min intervals(code can be modified to do 1 min intervals if desired). Data is spit out into 8 columns and (typically) just under 1,000 rows. Data includes: date/time (unix), tx bytes added to MP since last block found, tx bytes in MP since BEFORE last block, txs added to MP since last block, txs in MP since BEFORE last block, fees added to MP since last block found (in satoshis), fees added to MP since BEFORE last block, tx per min.     
So if you divide the sixth column (F in excel), by the second column (B in excel) you can get the fee per byte for all txs in MP that have been sent AFTER the last block was found. If you add columns F+G and B+C and do (F+G)/(B+C) the result is the fee per byte for all txs in the mempool at that moment. 
Basicaly this scraper is the data that is visualized here: https://tradeblock.com/bitcoin/. It can easily be modified to run API queries at weekly intervals if you want to just let it run in the background. 
Two points of caution: one, there are sometimes gaps in the data and the time will jump from 8/30 12:10 to 8/30 12:40 (or similar), it is rare but it does happen. Two, remember that Tradeblock is like any other node and will 'count' thier mempool differently. Some will hold on to txs for 72 hours with no min fee, others will only count txs as in the mempool fo 48 hours and only if the fee is >0. 

## updates
 version 0.20
 - now includes excel formatted timestamp at end
 - column headers
 - various code changes (uses go's endcode/csv pkg instead of fmt.Fprintf(), other minor stuff)


## Usage
$ go run $GOPATH/bitcoin-mempool-scraper/tbkmempool.go
program will run, write, and close automatically---i.e. requires no user input.

requires Go! (golang)
see: http://golang.org
