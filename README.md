# UST-loss-calc-cex
Goal of the system:  To calculate UST losses with the least amount of effort from the victims of UST and the person who is running the caculator (the admin).

# Current status:
Tested Working for: Coinbase, Kraken, Binance, OkCoin, KuCoin, and Several Defi contracts
All Other Exchanges have not been tested yet

# How it works
The victims of UST gather read only API keys from the centeralized exchanges they used and create dust transactions on the terra wallets they used with the memo "collect my info urg".  The read only API keys and terra wallet addresses are given to the admin then puts all the keys into a file with a user ID / name attached to each key.  The admin then runs the script and gets back a summary of UST losses.  

## More details on how it works
All buy and sell trasnactions from the wallets and the exchanges are gathered by user and then divided up by the timestamps given.  Then an output file is created


# Client Usage
The client creates read only API keys from all the Centeralized exchanges (usually takes less than 10 minutes).  The client then goes to each terra address they own and send any amount (preferablly a fraction of a cent to reduce costs) to the same wallet they are sending from with the memo: "collect my info urg".  

The Client then gives the API keys and the terra wallet addresses to the admin.


# Admin Usage
## Install Python3

In your MacBook, go to Applications -> Utilities -> Terminal (you can drag this to the bottom bar for quick access)

Type in 
```
python3 --version
```

You should see something like 
```
Python 3.9.6
```

Python version 3 should come with an updated OS of MacBook

If you don’t see that, go to this website and download python3
https://www.python.org/downloads/


Copy and paste this into your terminal window

```
# Go to your desktop to make it easier to interact with files / folder
cd ~/Desktop/

# Install Pip (a python package manager)
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python3 get-pip.py

# Install CCXT
pip install ccxt

# Download the UST loss calculator script onto your MacBook
git clone https://github.com/Anon9001/UST-loss-calc-cex.git
cd UST-loss-calc-cex
```

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
python3 run.python &lt;As many optional timestamps to divide up totals&gt;

Example:python3 run.python 1651935577000 1652407129000

1651935577000 is the timestamp of when Do Kwon says the depeg occured, 1652407129000 is the time at which the chain halted.  This will divide up buys/sells into 3 different categories.  All buys and sells before 1651935577000, all buys and sells between timestamps 1651935577000 and 1652407129000 and all buys/sells after 1652407129000.  


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


