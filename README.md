# UST-loss-calc-cex
UST loss calculator for centralized exchanges


## Reqired: Get a snapshot using the snapshot tool.  

The snapshot tool is located here: https://urg-snapshot-tool.s3.us-east-1.amazonaws.com/index.html. Use terra1hzh9vpxhsk8253se0vv5jj6etdvxu3nv8z07zu as the CW20/CW721 token address.  The code for this tool is located here: https://github.com/Anon9001/token-snapshot.  Use the block height you want to use from terra finder (I.E https://finder.terra.money/classic/blocks/7544910).  Please Note the timestamp and convert to Timestamp in milliseconds from a converter (I.E https://www.epochconverter.com/)

NOTE: snapshot tool takes a while to run, like 6 hours.  I've posted an example snapshot in this repo

## Required: Create CEX read only tokens or get them from clients.  Add them in input.csv in the following format
ClientId, exchange id, api key,secret key, id, password / pass phrase

ClientID - This id is created by you.  It can be the user's name, or a client ID, etc.  If a client has multiple CEX like binance and kraken and you have the same ClientID, the program will combine data from both CEX in the output file for one client ID.  For example a user sells 100 UST on binance and sells 200 UST on kraken, the output will have the client sales recorded as 300 UST

exchange id	- The Exchange IDs can be found in the column IDs in the readme contained here: https://github.com/ccxt/ccxt#install 

api key	- Always given by the Exchange when the read only token / api key is created to view transactions / deposits / withdrawals

secret key	- Always given by the Exchange when the read only token / api key is created to view transactions / deposits / withdrawals

id  - This is rarely given out by an exchange but most of the time is not.  When given out, make sure to fill this in.  

password  - This is rarely set when an exchange creates an token / API key


## USAGE with arguments to run the program
USAGE: python3 run.python &lt;snapshot file name&gt; &lt;block height of snapshot&gt; &lt;timestamp of blockheight in miliseconds&gt; &lt;aUST to UST value at block height of snapshot&gt;

Example: python3 run.python terra1hzh9vpxhsk8253se0vv5jj6etdvxu3nv8z07zu.csv 7607789 1652407129000 1.263

&lt;snapshot file name&gt; - This is the file that was created with the snapshot tool

&lt;block height of snapshot&gt; - This is the block height you used when creating the snapshot file with the snapshot tool

&lt;timestamp of blockheight in miliseconds&gt;  - This is the timestamp in miliseconds that the block was at at the block height used in the snapshot tool

&lt;aUST to UST value at block height of snapshot&gt; - This is the value of aUST.  When you convert 1aUST to UST, it is multiplied by this.  When anchor stopped running, the conversion rate was 1.263
