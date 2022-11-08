# UST-loss-calc-cex
UST loss calculator for centralized exchanges and the terra wallets connected to them by withdraw or deposit.

Note: Does not work with coinbase or kraken.  Coinbase uses Eth wrapped UST and more code is needed.  Kraken pumps out empty sets when requesting withdrawal / deposit history


## Reqired: For every terra wallet connected to the exchange keys, make sure you send a dust transaction from yourself to yourself with the memo "collect my info urg".  Otherwise the program will not count the wallets as the clients wallet.  The reason for this is if a client uses an exchange wallet to deposit UST into another exchange before they sell or if they bought it from another person to deposit it to their exchange months after the depeg.


## Required: Create CEX read only tokens or get them from clients.  Add them in input.csv in the following format
ClientId, exchange id, api key,secret key, id, password / pass phrase

ClientID - This id is created by you.  It can be the user's name, or a client ID, etc.  If a client has multiple CEX like binance and kraken and you have the same ClientID, the program will combine data from both CEX in the output file for one client ID.  For example a user sells 100 UST on binance and sells 200 UST on kraken, the output will have the client sales recorded as 300 UST

exchange id	- The Exchange IDs can be found in the column IDs in the readme contained here: https://github.com/ccxt/ccxt#install 

api key	- Always given by the Exchange when the read only token / api key is created to view transactions / deposits / withdrawals

secret key	- Always given by the Exchange when the read only token / api key is created to view transactions / deposits / withdrawals

id  - This is rarely given out by an exchange but most of the time is not.  When given out, make sure to fill this in.  

password  - This is rarely set when an exchange creates an token / API key


## USAGE with arguments to run the program
USAGE: python3 run.python &lt;pre depeg block height of when to snapshot user's holdings&gt; &lt;depeg timestamp - timestamp of the depeg block&gt; &lt;timestamp in miliseconds of when purchases of UST are no longer promised as 1 ust to 1 usd&gt; &lt;aUST to UST value at block height of snapshot&gt; 

Example: python3 run.python 7544910 1651935577000 1652407129000 1.263

7544910 is the block that DK chose as when ust depegged from usd, 1651935577000 is the timestamp for the depeg block 7544910, 1652407129000 is the time at which the chain halted, 1.263 is the conversion rate when anchor stopped producing interest
