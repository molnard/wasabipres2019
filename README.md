# wasabipres2019

![alt text](https://wasabiwallet.io/images/wasabi_wallet_logo_2-1.png)

Greetings everyone! My name is David Molnar and I would like invite you for a coffee. A virtual coffee of course because no way I have as much coffee as I would require to invite you all.

There we are in the coffee shop and we are paying with bitcoin as a result we get back our drink. Meanwhile you are drinking your coffee which is tasty and hot as it meant to be let's think what happened in the point of privacy view. 

# Wallet
You are using some kind of wallet for the transaction. 
__Web wallets__ In the privacy point of view this is the worst you can do.  
__Key storage__ To sign the transaction for that coffee you have to have a private key. It must be stored on your device. Meaning that you have the full control over your bitcoins no third party can freeze or lose your funds. If you control the keys it is your bitcoin if you don't control the keys it is not your bitcoin.
__Encrypted secret__ the wallet file is encrypted in a way that if someone manages to get it still useless without your password. 
__Address reuse__ harms the privacy of not only yourself, but also others - including many not related to the transaction. When addresses are re-used, they allow others to much more easily and reliably determine that the address being reused is yours. Wasabi is a deterministic wallet so it generating new addresses for receviving and for change.
__Input joining__ Coin control means you are not only seeing the total balance of your wallet but the individual coins you own. Why it is important? You should be aware of that which coin or coins you will use for that transaction what was the history of that coin. You have control over that eventhou you can tag coins when sending or receiving and Wasabi will automatically build the history of that coin. But we still have a chain how to break it?

# Nodes
__Supernodes__
Lightweight wallets generally query a third-party server which can easily spy on you.

__SPV filtering__ BIP158 new proposal which is in the process of getting finalized. It is apparently in discussion. The way how it works you download filters you do not tell the nodes what to filter and than you can figure out what block are relevant to my use case to my wallet. 

You have a constant set of filters you get if from some source and from thoose filters you can figure out which block you are interested in and you get the blocks from random nodes. So basically no on can figure out which transactions you are interested in. Even the blocks because you are using Tor and changing Tor circuits it is just really hard if not impossible. So this is the first light wallet architecture thats truly a light wallet that does not ruin your privacy. Because bitcoin core nodes does not support it yet so we have our backend that sends the filters to the clients and thats how it works. 

You can run a fullnode too and configure Wasabi to use that.

# BlockChain and transaction graph

Bitcoin is often described as an anonymous cryptocurrency, but this is incorrect. Bitcoin is actually pseudonymous(no p in the beginning). The distinction is crucial: under a cryptographic pseudonym, your behavior can still be tracked. KYC exchanges collect personal information which is shared with other exchanges, Heuristics and clustering analysis to identify exchanges, mixers, supernodes connect to large swathes and correlate transaction with their originating IPs.


_Odd dollar example_
# Fungibility!
Sound familiar but what does it mean exactly?
Fungibility is a principle in economics it says a token of value such a currency coin is indistinguishable of any other coins. Either you can’t say I would accept US dollars but only if their serial number is odd, if it is even that is evil money I won't touch it. If you say that you are breaking the law. The law requires you to threat equally and the government can't say that either. So that creates fungibility. Every dollat billet is fully exchangable of any other dollat billet for equal. That principal is fundamental to currency.

If you visit the bitcoin.mit.edu website you will see the following statement. If there is no fungibility that statement would not be correct.

_Consequence_
If you destroy fungibility you destroy the means of exchange function of the currency. For example, in bitcoin you can create a blacklist or a whitelist. __What it does that it imposes a burden on everyone.__ If you receive money now, you don’t know if it is real unless you also check that against the latest version of the blacklist to see if it not one of the banned ones. You can’t do that, that does not scale. If there was a mass centralization in mining to adopt that kind of policy that would be a destructive event for bitcoin.

Is that really what we concerned about today? Do you care with fungibility? In my opinion: not really! (Of course in the long term I care) BUT for today I would like to use my bitcoins without any restrictions. You are doing nothing illegal, no darknet connections, you are clean like the brand new snow. 

When you are sending money, are you ready to share every transactions connected to it in the past?
When you are receiving money, are you ready to share every transactions connected to it in the future? 
Even if you are doing nothing illegal (as most of the bitcoin users) __even so__ I do not feel comfortable to share that information.
__Do we need fungibility? Yes but we need more. WE NEED Privacy!__
 
_Story: traceing a coin_
In the oldern days I sold bitcoins face to face. The buyer bought it and just for fun I decided to follow my coins just to see where it will land. One day I found that the final buyer has 32 BTC and sent that to BITMEX. That a lot of money.
Every buy or sell you will expose one of your addresses.

# Privacy
What can we do to keep our privacy? There is a lot to do we will see it in the next part.
https://youtu.be/XORDEX-RrAI?t=969

_Decentralized mixers_
Just to mention without going into the datails 
Thumblebit is a unidirectional payment hub something like lightning network but without the network part and it is anonymus. Joinmarket is instant Thumblebit can archive higher anonimity set. 

# Wasabi wallet

I would like to show how do we achive privacy in a wallet called Wasabi wallet. What kind of technology did we use / implement or develop for that purpose. My presentation plan is to go trough a casual day of a bitcoin user.


_coinjoin_
Let's take the previous example. You are avoiding address reuse, using the coincontrol and labeling and the history of your coins are growing. That is good but now you have to join together two or more coins to have enough money to pay for something. You will expose some part or all of your transaction history involved by your coins. Also you can expose the total amount of money you have. Instead of paying the landlord direcly with one or more of your coins you have to use some obfuscation to ensure your privacy.

_mixers_
Anonymity loves company: you cannot mix by yourself. If coins come from the same wallet it can be connected together with the help of breadth-first search on the transaction graph. We need company to make a reliable coinjoin.

Decentralized mixer: in the past, traditional bitcoin mixers provide centralized way to obfuscate the ledger. The problem is that you have to send your coins into the mixer and they will send back the mixed bitcoin for you if they will... For example: Bitcoin fog worked for years without an issue had a good feedback but later it became a selective scam. You send the money it mixes but if you are sending a larger amount then it will take it. Tricky isn't it? 

Fixed denominations: CoinJoin outputs should be equal regarding the amounts. Every attempts to change this is to risk that the CoinJoin can be deanomyzed. Imagine that a CoinJoin transaction is written in a format of a Sodoku game, the rows are the inputs, the columns are the outputs. Analyzing the amounts and filling the sodoku can reveal the relationship between inputs and outputs thus deanonymize the participants. (Sharedcoin works like this)

CoinJoin rounds: contructing the CoinJoin transaction requires an exact procedure to follow. For example the first is to collect enought participants to construct the inputs. Later we will go into the details. 

Chaumian CoinJoin: contructing the CoinJoin transaction requires some kind of coordinator which establish the connection between the paticipants. This coordinator have to contructed in way that it cannot deanonymize the participants. 



ip - tor
anynomity loves company - anonimity set



# Anonymity network

We need TOR. No TOR library for dotnet 

# Network analysis

There is no light wallet that would not fail on the privacy level against network analysis. Every light wallet is volnurable to network analysis. With most light wallet is easy to see because it is mostly just querying a web API so every bitcoin address are exposed and just connected together.

_story_
Jonas Nick has deaninimyzed a lot of SPV wallets he said that give me one of your bitcoin address (SPV wallet) and I give back 70 percent of your wallett addresses. That is pretty scary.




# About Wasabi



# Credits Sources

Haseeb Qureshi

# Possible questions

_Personal implications_
Bitcoin is often described as an anonymous cryptocurrency, but this is incorrect. Bitcoin is actually pseudonymous(no p in the beginning). The distinction is crucial: under a cryptographic pseudonym, your behavior can still be tracked. KYC exchanges collect personal information which is shared with other exchanges, Heuristics and clustering analysis to identify exchanges, mixers, supernodes connect to large swathes and correlate transaction with their originating IPs.
Companies like Chainalysis provide surveillance services to law enforcement and various three-letter agencies, reportedly earning more than about 6M dollar in 2018 via government contracts.

_Confidental transaction_
Masking the amounts in transactions. So the end result is we dont need a round however they are costy I guess 10 times more in size. So there is a trade-off in it.

_ZCash, Monero_




