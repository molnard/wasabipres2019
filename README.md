# wasabipres2019

![alt text](https://wasabiwallet.io/images/wasabi_wallet_logo_2-1.png)

Hi everyone! My name is David Molnar and I would like invite you for a coffee. A virtual coffee of course because no way I have as much coffee as I would require to invite you all.

So there we are in the coffee shop and we are paying with bitcoin as a result we get back our drink. Meanwhile you are drinking your coffee which is tasty and hot as it meant to be, let's have a conversation about what happened in the point of privacy view during the transaction.

# Wallet
To pay you are using some kind of wallet for the transaction maybe a webwallet or a lightwallet. The problem is that
__Web wallets__ Everyt actions you take are forwarded to a server. Thin client like wallets are the same they are just providing a user interface but transaction related operations are running on the servers which can easily spy on you. In the privacy point of view this is the worst you can do. Use wallets which are not tied to server connection.
__Key storage__ To sign the transaction for that coffee you have to own a private key. It must be stored on your device, meaning that you have the full control over your bitcoins no third party can freeze or lose your funds. If you control the keys it is your bitcoin if you don't control the keys it is not your bitcoin.
__Encrypted secret__ If the key is stored locally then the Wallet file should be stored safely. Wasabi is encrypt the file in a way that if someone manages to get it still useless without your password. What is more safer than that is to use a hardware wallet so your private keys never leave embedded system. 
__Address reuse__ Address reuse can be dangerous too. It harms the privacy of not only yourself, but also others - including many not related to the transaction. When addresses are re-used, they allow others to much more easily and reliably determine that the address being reused is yours. Wasabi is a deterministic wallet so it is generating new addresses for every transaction.
__Input joining__ In many wallets you are only seeing the total balance of your wallet. In reality your balance is fragmented to many UTXO-s with this kind of wallets you are not able to choose which coin goes where it is selected automatically. Why it is important? You should be aware the history of the coins which will be used for that transaction where did it came from. With coincontrol you can see every coins you have, you can select which will be used, eventhou you can add labels to coins when you are sending or receiving and  Wasabi will automatically append the labels according to the path of that coin.
__Trust developers__ Let's say we have found a wallet is fulfilling the mentioned critereas. How can you verify that? Check on the website? Trust in the creator of the wallet? In the world of bitcoin we have a good saying for that: "don't trust, verify". The mechanism of a software is fully determined by the source code. If you are compiling your own wallet from that you can be sure it will work accordingly. Even if you are not a programmer so you have to trust in someone at least the trust is distributed among the programmers of the world like in any open-source projects.
__Company behind__ It is also good if there is a legal entity behind the software. Wasabi has zkSNACKs. 

These were the main privacy problems with wallets. Next session is the bitcoin network especially nodes.

# Nodes

__Supernodes__
There are supernodes in the network which are collecting metadata about the origin of any network traffic. If you are lucky you didn't bump into any network analysis server, but you likely will in the future. When you are broadcasting a transaction the originating IP, your IP goes with it. To solve this you can use VPN or any anonimity network. Wasabi is using TOR and random node selection to address this problem. 
__P2P Transaction propagation__
In the future transaction propagation could be made more private with the technology called dandelion where path and the propagation as known as diffusion is obfuscated with some random behaviour.
__Special nodes__
There are also some special nodes, servers which are dedicated for a certain lightwallet, a third-party server which can easily spy on you.

__Get balance requests SPV filtering__
Another huge problem is how the wallets are requesting your total UTXO. A wallet like this is requesting every UTXO related to the wallet are exposed. Bloom filtering is not helping on this because the filters are on server side. You should run a full node OR    
there is another option. A new proposal BIP158 which is in the process of getting finalized. It is apparently in discussion. What it does is that you are not downloading the whole blockchain but filters. The filters are contructed in a way that your wallet can determine which blocks are related. This is happening on client side. So instead of requesting transactions it is requesting blocks even more it is requesting every block from random nodes. So basically no on can figure out which transactions you are interested in.

With wasabi you have a constant set of filters you get it from some source additionally it is using Tor and changing Tor circuits on every request. So this is the first light wallet architecture thats truly a light wallet that does not ruin your privacy. Because bitcoin core nodes does not support it yet we have to implement it on our backend that sends the filters to the clients and thats how it works. Another option is to use a fullnode Wasabi is also capable to use that.

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




