# wasabipres2019

![alt text](https://wasabiwallet.io/images/wasabi_wallet_logo_2-1.png)

Hi everyone! My name is David Molnar and I would like invite you for a coffee. A virtual coffee of course because no way I have as much coffee as I would require to invite you all.

## Coffee Shop

So there we are in the coffee shop and we are paying with bitcoin as a result we get back our drink. Meanwhile you are drinking your coffee which is tasty and hot as it meant to be, let's have a conversation about what happened in the point of privacy view during the transaction.

# Customer service
If you are buying/selling with bitcoin you are exposing your identity which could be connected to your wallet. If you are doing it "offline" you are exposing your identity to the 

# Wallet
To pay you are using some kind of wallet for the transaction maybe a webwallet or a lightwallet. The problem is that
__Light wallets__ Everyt actions you take are forwarded to a server. Thin client like wallets are the same they are just providing a user interface but transaction related operations are running on the servers which can easily spy on you. 
In the privacy point of view this is the worst you can do. Use wallets which are not tied to a dedicated server.
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
There is no light wallet that would not fail on the privacy level against network analysis. Every light wallet is volnurable to network analysis. With most light wallet is easy to see because it is mostly just querying a web API so every bitcoin address are exposed and just connected together. For example to determine the total UTXO you have in the wallet addresses are queried in the same time from the same source. Bloom filtering is not helping on this because the filters are on server side so you still exposing your addresses.

Jonas Nick has deanonimyzed a lot of SPV wallets and he said that give me one of your bitcoin address (SPV wallet) and I give back 70 percent of your wallett addresses. That is pretty scary. To prevent that you should run a full node which is costly OR    
there is another option. A new proposal BIP158 which is in the process of getting finalized. It is apparently in discussion. What it does is that you are not downloading the whole blockchain but filters. The filters are contructed in a way that your wallet can determine which blocks are related. This is happening on client side. So instead of requesting transactions it is requesting blocks even more it is requesting every block from random nodes. So basically no on can figure out which transactions you are interested in.

With wasabi you have a constant set of filters you get it from some source additionally it is using Tor and changing Tor circuits on every request. So this is the first light wallet architecture thats truly a light wallet that does not ruin your privacy. Because bitcoin core nodes does not support it yet we have to implement it on our backend that sends the filters to the clients and thats how it works. Another option is to use a fullnode. Wasabi is also capable for that.

# BlockChain and transaction graph

Bitcoin is often described as an anonymous cryptocurrency, but this is incorrect. Bitcoin is actually pseudonymous(no p in the beginning). The distinction is crucial: under a cryptographic pseudonym, your behavior can still be tracked. KYC exchanges collect personal information which is shared with other exchanges, Heuristics and clustering analysis to identify exchanges, mixers, supernodes connect to large swithes and correlate transaction with their originating IPs. 

## CoinJoin

Ok so at this point most of the privacy problems are solved on an acceptable level by using existing technologies like TOR and following clever protocols. We handled Wallet leakage, networks and part of blockchain analysis but one more thing is remained, transaction chain is still there and is it traceable. So we have to obfuscate the transaction graph. 

_mixers_
Can someone do this alone? Well not really. The problem is that even if you are generating a lot of transaction with varying inputs and outputs the begin and the end transaction could be identified. For example if coins come from the same wallet it can be connected together with the help of breadth-first search on the transaction graph. By the way transaction generation could be expensive. Anonymity loves company: you cannot mix by yourself.

In the past, traditional bitcoin mixers provide centralized way to obfuscate the ledger. The problem is that you have to send your coins into the mixer and they will send back the mixed bitcoin for you if they will... For example: Bitcoin fog worked for years without an issue had a good feedback but later it became a selective scam. You send the money it mixes but if you are sending a larger amount then it will take it. Decentralized coinjoin is the solution for that.

CoinJoin outputs should be equal regarding the amounts. Every attempts to change this is to risk that the CoinJoin can be deanomyzed. Imagine that a CoinJoin transaction is written in a format of a Sodoku game, the rows are the inputs, the columns are the outputs. Analyzing the amounts and filling the sodoku can reveal the relationship between inputs and outputs thus deanonymize the participants. (Sharedcoin works like this) we need fixed denominations.

Basically it works as follows. Wait enought participants to register into the coinjoin. They are just sending confirmed utxos as the inputs. If there is enought participants move forward construct the coinjoin transaction. Inputs and outputs are ready but the signatures are missing so send this partially constructed transaction back to the users let them verify it - for example if they are gettign back enough bitcoins. If it is OK they sign their inputs send it back to the coordinator where the transaction will be propagated to the network. Roughly speaking this is how it works.

Why coinjoin is good for privacy?
Because from the equal outputs of the CoinJoin you cannot tell which input correspons to that for sure. If there is 4 paticipants in the coinjoin then you have a quater probability to tell that. In this case we are saying that the anonimity set is four. In the reality nobody will register with the exact amount of the denomination so beside the coinjoined coin you will get back a change which is unmixed. With that amount you can participate in another round meaning that with this particular example if you have 8 bitcoins than you will have 8 rounds to anonymize you total amount. You can also do that with CoinJoined coins to increase the privacy of a coin. 
Later wasabi added a feature called: "unequal amount mixing" which basically meaning that the coordinator is trying to mix the remaining amounts if there is enough to do that. In that case the anonimity set will be lower but it will be faster and we are getting more anonymity for a slightly more fee in generally it is cheaper.

With this your privacy on the blockchain is increased. Are we in safe now? Unfortunately not because if the coordinator is spying on you it will know a lot to deanonimize you. Somehow the participants have to keep their outputs in a secret during the coinjoin. How to construct the CoinJoin if we don't know the outputs? The answer is blind signitures!

Schnorrian CoinJoin: contructing the CoinJoin transaction requires some kind of coordinator which establish the connection between the paticipants. This coordinator have to contructed in way that it cannot deanonymize the participants.

Mainly there are two actors here on the left side the user with wasabiwallet and the coordinator on the right side. Our main goal is to construct the coinjoin transaction in a way that even the coordinator itself could not deanonymize the users meaning that it cannot figure out which outputs corresponds to an input AND maintain protection against DOS attacks. 
So the first phase is the registration phase. The user would like to gain privacy on one of her UTXOs this will be the input. Also she have to give the outputs where the private coins will arrive. Now if she is giving outputs in a plain format the coordinator easily interconnect inputs and outputs so the trick is to blind the outputs. With this the trick is that the coordinator cannot see the output address but can sign it and later verify that signiture. So it signs it blindly and send it back. Also the input is added to the coinjoin transaction but it is not signed yet so nobody can spend it! In every phase you will see uniqueId-s and hashes like roundhash, basically the function of that is to prevent a hacker joining into coinjoin progress skipping the input registration phase. 
If the anonimity set is fifty than the coordinator will wait for fifty clients to register. This is the longest phase depends of the user activity can take a few minutes to hours. After we got enough users we move forward to the next step. 
In that phase we are checking if the users are still there and send them back the roundhash. As we got all the input addresses on coordinator site generate a hash from that and send it to the client. In that way later the clients can verify if the coordinator has messed something with the inputs. 


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
 
_coinjoin_
Let's take the previous example. You are avoiding address reuse, using the coincontrol and labeling and the history of your coins are growing. That is good but now you have to join together two or more coins to have enough money to pay for something. You will expose some part or all of your transaction history involved by your coins. Also you can expose the total amount of money you have. Instead of paying the landlord direcly with one or more of your coins you have to use some obfuscation to ensure your privacy.





ip - tor
anynomity loves company - anonimity set



# Anonymity network

We need TOR. No TOR library for dotnet 

# Network analysis

_story_





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




