# wasabipres2019

![alt text](https://wasabiwallet.io/images/wasabi_wallet_logo_2-1.png)

Hi everyone! My name is David Molnar and I am one of the software developers we could say software artist of the Wasabi Wallet team. 

Wasabi is an open-source, non-custodial, privacy focused Bitcoin wallet, that implements trustless coin shuffling with mathematically provable anonymity: Chaumian CoinJoin, it is the first of its kind.

But before we go into the details. To wake you and me up let's go buy a cup of coffee.

## Coffee Shop

So there we are in the coffee shop and we are paying with bitcoin as a result we get back our drink. Meanwhile we are drinking our coffee which is tasty and hot as it meant to be, let's have a conversation about what happened in the point of privacy / security view during the transaction.

# Customer service
What is pretty obvious you have exposed your personal identiy to the cashier. The situation is pretty the same If you are doing it online bacause of the Know you customer policy as know as KYC policy where you have to identify yourself for example with a photo if your ID card. So the transaction can be connected to you. If you are using your wallet in the same way you are using your credit card you might have exposed you total balance or some part of it to the cashier. That is not only an uncofortable feeling but also dangerous. With your input address she could follow back past transactions and with change output address she could trace your future transactions. 

# Wallet
To pay with bitcoin you have to use a wallet maybe a webwallet or a lightwallet. Most of these wallets directly tied to a 3rd party server.

__Light wallets__ Everyt actions you take are forwarded to them if they decide they can easily spy on you. Most of the cases they are holding your private keys too, it is called custodial key management.
In the privacy point of view this is the worst you can do.

__Key storage__ Private key should be stored on your side, meaning that you have the full control over your bitcoins no third party can freeze or lose your funds. Last time and that was the last time that I used my coinbase wallet because suddenly I was required to upload an image of my passport until that my wallet was freezed. They can lock you out until you deannonimize yourself. 
If you control the keys it is your bitcoin if you don't control the keys it is not your bitcoin.
 
__Input joining__ In many wallets you only see the total balance of your wallet. In reality your balance is fragmented to many coins. With this kind of wallets you are not able to choose which coin goes where it is selected automatically. Why it is a problem? You should be aware the history of the coin which will be used for a transaction, where did it come from. With coincontrol you can see every coins you have, you can select which will be used, eventhou you can add labels to coins when you are sending or receiving and Wasabi will automatically append the labels according to the path of that coin. Basically it is building the history of a particular coin. For example in that way you can avoid to pay with your full salary for that coffee and expose it to the cashier. 

__Trust developers__ Let's say we have found a wallet which is fulfilling the mentioned critereas. How can you verify that? 

Wasabi is 100% open-source sotfware so you don't have to trust in the developers you can verify it by compiling from the source code. 

Your wallet have to communicate to send and receive requests with bitcoin nodes. 

# Nodes

__Supernodes__
There are supernodes in the network which collect metadata about the origin of any network traffic. If you are lucky you didn't bump into any network analysis server, but you likely will in the future.

There is no light wallet that would not fail on the privacy level against network analysis. With most light wallet, easy to see because mostly it is just querying a web API. For example to determine the total balance you have in your wallet, addresses are queried in the same time from the same source and just connected together.

Jonas Nick has deanonimyzed a lot of SPV wallets and he said that give me one of your bitcoin address (SPV wallet) and I give back 70 percent of your wallett addresses using heuristic and cluster analysis. That is pretty scary. 

These kind of problems can be solved by runnig a full node I would recommend that. But if you cannot do that because it is resource intensive. 

Another solution is in the process of getting finalized BIP158. It is apparently in discussion. 
The idea is instead of requesting addresses you are requesting blocks. In that way an observer cannot tell which addresses are we interested in.
With wasabi you have a constant set of filters you get it from some source. The filters are contructed in a way that your wallet can determine which blocks are related. So this is the first light wallet architecture thats truly a light wallet that does not ruin your privacy. Because bitcoin core nodes does not support it yet we have to implement it on our backend that sends the filters to the clients and thats how it works.

Another interesting technology will be dandelion where the where propagation as known as diffusion of a transaction is obfuscated with some random behaviour.

# BlockChain and transaction graph

Bitcoin is often described as an anonymous cryptocurrency, but this is incorrect. Bitcoin is actually pseudonymous(no p in the beginning). The distinction is crucial: under a cryptographic pseudonym, your behavior can still be tracked. 

## CoinJoin

At this point we have covered many issues. However one of the most trivial problem is remained, that transaction chain is still there and is it traceable. So we have to obfuscate the transaction chain. Let's try to do some Mixing.

_mixers_
Can you obfuscate the ledger on your own? Well the answer is not really. The problem is that even if you are generating a lot of transactions with varying inputs and outputs the begin and the end transaction could be identified. For example if coins come from the same wallet it can be connected together with the help of breadth-first search on the transaction graph. In additon transaction generation could be expensive. The more users there are, the better your privacy.

In the past, traditional bitcoin mixers provide centralized way to obfuscate the ledger. The problem is that you have to send your coins into the mixer and they will send back the mixed bitcoin for you if they will... For example: Bitcoin fog worked for years without an issue had a good feedback but later it became a selective scam. You send the money it mixes but if you send a larger amount then it will take it. Also it can decide to deanonimize you. Trusted 3rd parties are privacy and security holes. Wasabi has a trustless solution for this but before that

Why coinjoin is good for privacy? Because from the CoinJoin you cannot tell which output correspons to an input.
Let's look at following CoinJoin transaction. 
For the first look it is hard to say which output connected to which input. Who knows the game named sodoku? Imagine that a CoinJoin transaction is written in a format of a Sodoku game, the rows are the inputs, the columns are the outputs. Analyzing the amounts and filling the sodoku can reveal the relationship between inputs and outputs in that way deanonymize the participants. Let's play a game. Try to deanonimize the users. Output with 1 BTC belongs to Alice because she cannot get back more than she gave. Output with 8 BTC can only can only be owned by Eszter bacause of the same reason. Bob's outputs can only be 2 and 4 not other combination gives 6 bitcoins. And so on... The more users are denonimized the easier to do the rest. If we need mathematically proven anonimity we need to have equal outputs regarding the amounts.

If there is 4 paticipants in the coinjoin then you have a quater probability to tell who is the original owner of that coin. In this case we are saying that the anonimity set is four. In the reality nobody will register with the exact amount of the denomination so beside the mixed coin you will get back a change which is unmixed. With that amount you can participate in another round meaning that with this particular example if you have 8 bitcoins than you will have 8 rounds to anonymize you total amount.

How to generate this coinjoin transaction? Something like a coordinator is required which establish the connection between the paticipants.

With this your privacy on the blockchain is increased. Are we in safe now? Unfortunately not because if the coordinator is spying on you it will know a lot to deanonimize you. This coordinator have to contructed in way that it cannot deanonymize the participants.
Let's see how it is done by Wasabi.

So the first phase is when the coordinator waits and collects the users. For example the anonymity set is fifty so it will wait until 50 users are there. Let's have a closer look how can a user can register.

The user would like to gain privacy on one of her coins this will be the input. Also she have to give the output where the mixed coin will arrive and also a change output. Now if she gives output in a plain format the coordinator easily interconnect the input the output so deanonimize the user. The trick is to blind the output. With this the coordinator cannot see the output address but can sign it and later verify that signiture if the output was registered or just an attacker tries to provide some fake outputs. So it signs it blindly and send it back. 

In that phase we are checking if the users are still there and do some verification. If all of the clients are there we move to the next phase. 

The client sends the unblinded output. Here we have to stop for a while. The communication between the client and the coordinator made through the internet. I have already mentioned that wasabi is using TOR anonimity network to increase privacy. On client side we are not only defend ourself from an external observer but from the Coordinator itself. If we would use the same Tor channel as we used to send the input the coordinator can interconnect that. So to send the output we are using a different Tor channel and authorize ourself wtih the unblinded output signatures.

So now we have all inputs, all outputs only the signatures are missing. 

In signing phase we let the clients verify the constructed coinjoin. They are verifying if the transaction is valid for example it the outputs are there and the amounts are correct. So you only have to trust in yourself. If something is not correct then client can say that: I am not sign this transaction. So basically there is no way to stole from the users. if it is OK the signature is sent back and added to the transaction. 

After every user signed the transaction it is broadcasted to the nodes by the server. 

Wasabi not only protects your privacy from others but also protects from us. The only person you have to trust in, is yourself!

More details can be found on the website regarding technicals details, software, or about the team. 


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




