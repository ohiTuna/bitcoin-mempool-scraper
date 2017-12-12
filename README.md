>**windows binary now available**
I've built a windows binary for users without Go installed. I've only tested it on my system so **I would greatly appreciate users without go installed letting me know if it worked.** It should simply run, exit, and have a .csv file created in the same dir as where your .exe is located        


## Tradeblock mempool scraper

Gets the last week of Bitcoin's mempool data, giving snapshots at 10 min intervals(code can be modified to do 1 min intervals if desired). Data is spit out into 9 columns and (typically) just under 1,000 rows.
##### Data includes: 
- date/time (unix epoch)
- tx bytes added to mempool since last block found
- tx bytes in mempool since BEFORE last block
- txs added to MP since last block
- txs in MP since BEFORE last block
- fees added to MP since last block found
- fees added to MP since BEFORE last block
- tx per min
- timestamp (excel format)
So if you divide the 'fees added to MP since last block found' by the 'tx bytes added to MP since last block found' you can get the fee per byte for all txs in MP that have been sent AFTER the last block was found. If you add columns for fees before/after last and add tx bytes before/after then divide sum fees by sum tx bytes the result is the fee per byte for all txs in the mempool at that moment. 
Basicaly this scraper is the data that is visualized here: https://tradeblock.com/bitcoin/. It can easily be modified to run API queries at weekly intervals if you want to just let it run in the background, just add a ticker channel via a for loop before the httpGet. 
### Two points of caution: 
**one**, there are sometimes gaps in the data and the time will jump from 8/30 12:10 to 8/30 12:40 (or similar), it is rare but it does happen.
**Two**, remember that Tradeblock is like any other node and will 'count' thier mempool differently. Some nodes will hold on to txs for 72 hours with no min fee, others will only count txs as in the mempool fo 48 hours and only if the fee is >X sat/byte. 

## updates
**version 0.30**    
- windows binary exe now available (needs user testing)    


**version 0.20**   
- now includes excel formatted timestamp at end
- column headers
- various code changes (uses go's endcode/csv pkg instead of fmt.Fprintf(), other minor stuff)


## Usage    
**Windows users:**(needs tested to ensure no dependencies are needed)          
simply run the .exe and the .csv will be outputted to the same dir as .exe     

**Users with Go installed:**
$ go run $GOPATH/bitcoin-mempool-scraper/tbkmempool.go           
program will run, write, and close automatically---i.e. requires no user input.           
