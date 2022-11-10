# UST-loss-calc-cex
Goal of the system:  To calculate UST losses with the least amount of effort from the victims of UST and the person who is running the caculator (the admin).

# Current status:
Tested Working for: Binance, OkCoin, KuCoin, and Several Defi contracts
Tested Doesn't work for: Coinbase, Kraken, okx
All Other Exchanges have not been tested yet

# How it works
The victims of UST gather read only API keys from the centeralized exchanges they used and create dust transactions on the terra wallets they used with the memo "collect my info urg".  The read only API keys are given to the admin then puts all the keys into a file with a user ID / name attached to each key.  The admin then runs the script and gets back a summary of UST losses.  

## More details on how it works
The script gets all the trade information from each centeral exchange and all terra wallets from where they deposited / withdrew from.  A snapshot of all the victims UST is gathered at the snapshot block / time provided.  The script then figures out where all the UST went to, if any UST was bought after the hault time or if there was any UST from another source that the victim forgot about.


# Client Usage
The client creates read only API keys from all the Centeralized exchanges (usually takes less than 10 minutes).  The client then goes to each terra address they own and send any amount (preferablly a fraction of a cent to reduce costs) to the same wallet they are sending from with the memo: "collect my info urg".  

The Client then gives teh API keys to the admin.


# Admin Usage
##Install Python3

In your MacBook, go to Applications -> Utilities -> Terminal (you can drag this to the bottom bar for quick access)

Type in 
'''
python3 --version
'''

You should see something like 
'''
Python 3.9.6
'''

Python version 3 should come with an updated OS of MacBook

If you don’t see that, go to this website and download python3
https://www.python.org/downloads/


Copy and paste this into your terminal window

'''
# Go to your desktop to make it easier to interact with files / folder
cd ~/Desktop/

#Install Pip (a python package manager)
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python3 get-pip.py

#Install CCXT
pip install ccxt

#Download the UST loss calculator script onto your MacBook
git clone https://github.com/Anon9001/UST-loss-calc-cex.git
cd UST-loss-calc-cex
'''

## Add UST victim data to the input file
Open your browser go to this URL:
https://docs.google.com/spreadsheets/u/0/?tgif=d
Click on the + button to create a new sheet
Import the input.csv file in the folder UST-loss-calc-cex located on your desktop

Enter in all the API keys for the clients
If a client has more than one API key, make sure the API keys have the same client id / name otherwise the program won’t combine output data for that client

Save the file back into the folder UST-loss-calc-cex as input.csv

## Running the script
Run the script by typing the following into your terminal
python3 run.python &lt;pre depeg block height of when to snapshot user's holdings&gt; &lt;depeg timestamp - timestamp of the depeg block&gt; &lt;timestamp in miliseconds of when purchases of UST are no longer promised as 1 ust to 1 usd&gt; &lt;aUST to UST value at block height of snapshot&gt; 

Example: python3 run.python 7544910 1651935577000 1652407129000 1.263

7544910 is the block that DK chose as when ust depegged from usd, 1651935577000 is the timestamp for the depeg block 7544910, 1652407129000 is the time at which the chain halted, 1.263 is the conversion rate when anchor stopped producing interest

## Viewing results of the script
After the script is done running, Open google spreed sheet with output.csv
Open your browser and go to this URL:
https://docs.google.com/spreadsheets/u/0/?tgif=d
Click on the + button to create a new sheet
Import the output.csv file in the folder UST-loss-calc-cex located on your desktop


# More information about the script arguments

ClientID - This id is created by you.  It can be the user's name, or a client ID, etc.  If a client has multiple CEX like binance and kraken and you have the same ClientID, the program will combine data from both CEX in the output file for one client ID.  For example a user sells 100 UST on binance and sells 200 UST on kraken, the output will have the client sales recorded as 300 UST

exchange id	- The Exchange IDs can be found in the column IDs in the readme contained here: https://github.com/ccxt/ccxt#install 

api key	- Always given by the Exchange when the read only token / api key is created to view transactions / deposits / withdrawals

secret key	- Always given by the Exchange when the read only token / api key is created to view transactions / deposits / withdrawals

id  - This is rarely given out by an exchange but most of the time is not.  When given out, make sure to fill this in.  

password  - This is rarely set when an exchange creates an token / API key


