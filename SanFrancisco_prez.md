Hi everyone! My name is David Molnar and I am one of the software artists of the Wasabi Wallet team.

Wasabi is an open-source, non-custodial, privacy focused Bitcoin wallet, that implements trustless coin shuffling with mathematically provable anonymity: Schnorrian CoinJoin and it is the first of its kind.

Wasabi's prime directive is: privacy. Every aspects of the wallet is built around this. 

# Why do we care about privacy?

- For the first glance the answer is that you don't want another ppl knowing your business. 
How much money do you have? 
How much is your salary?
How much do you pay for your employees?

You can be an individual or you can be a business both need privacy for their payments so it is certainly not only matter to criminals. 

I lyed. It is very important to them to not have privacy.

Last time when I was abroad I had to pay with a 500 euro banknote. I was literally trying to hide during the payment because that amount of money can trigger someone. With bitcoin the amount and the number of prying eyes are much higher. 
Privacy means that you can voluntairly share information but only if you want to! Privacy is the act of choosing what to reveal to the world.

# But there is another greate benefit, a great glory behind,
What if It told you: if you impove privacy than you will impove bitcoin as a money itself.

Well if it would be an excange rate calculator it wouldn't be so useful. But now that has deeper meaning. 
Money has some axiomatic properties describes what is a good money: Acceptability, Portability, Durability, Divisibility, Fungiblitiy and so on.
Fungibility is the interchangablity of money. 1 EUR = 1 EUR. It does't matter where it came from. It does't matter if two ppl before you it was stolen. It is a euro. That euro is the same as every other euro. No one can say: I take that euro but I won't take that other one. Money is the one type of property that it cannot be stolen and recovered by the original owner. If you got robbed you can't say that is my money and give back two people later. You can say to the person who stole it from you but you can't just walk into a shop and say I am gonna sue you because you have the money that was stolen from me. The reason that we have fungiblity is very simple: otherwise money won"t work. Imagine that every time you receive a euro you have to check a centralized list if it is dirty, that's not working - it won't scale. In bitcoin we can see some companies trying to destroy fungiblity and that is a real problem. 

1 - Trying to sell clean coins for more. for example Coinbase coins.
2 - Many coins may be called ”dirty” in some way or another. These coins worth less than others or banned.


We are building money with bitcoin so we need fungibility too, otherwise bitcoin will fail as a money and it will be useless.

If we can provide easy (I mean cheap and fast) methods to impove fungibility we improve bitcoin as a money and we impove the privacy of ours!

# How to be more fungible and more private in practice?

Adam Gibson who is working on cryptography, bitcoin privacy, fungibility technology from the beginning, and most known as a developer of JoinMarket with Chris Belcher.
Set up a list with 7 points. 7 most important rules to follow:

So here is the list, I will give you couple of seconds to read through it.

# 1 Address reuse

Major privacy leak, known since whitepaper. Bitcoin is often described as an anonymous cryptocurrency, but this is incorrect. Bitcoin is actually pseudonymous. The distinction is crucial: under a cryptographic pseudonym, your behavior can still be tracked. 
It is like a masquarade party. If you are using the same mask on every party sooner or later you will be compromised and with the global ledger all the things you did in the past immediately connected to you.
Bitcoin addresses are pseudonyms you should throw it away after you used it.
It a very common mistake as far as I know 30% of all transactions involve an address which is used before.
Wasabi automatically removes used addresses.

# 2 Separate profile

For example you can have a work and a home profile, some wallet calls it accounts (based on BIP32). It is useful because you don't want mix your businesses, you want to handle them separately and keep them clean. A lot of wallet just showing your total balance which contains your salary, your donations, lambo rentals. So when you are paying for the coffee you might end up paying that with your total salary because your wallet automatically selects the input coins and you have absolutely no control over that. Usually you even cannot see that you have coins. You don't know which mask will be selected for the party. Bitcoin is not working like a bank account where you have a specific amount of money, bitcoin wallet has coins in it.

There is a metric called wallet clustering where you find bitcoin addresses and certain evidence that the addresses owned by the same person. You use a bunch of assumptions and heuristic but in the end you will have a set of addresses which is called a wallet cluster.
Jonas Nick said: give me one of your SPV wallet address and I give back 70 percent of your wallet addresses. That means that every person who has at least one your addresses can estimate 70% of your total money, which is pretty scary.

For example one powerful huristic is the Common-owner-input heuristic. Look at the following transaction, the most probable case is that someone want to buy something for 10 BTC. The heuristic says(szez) that A B C inputs belongs to the same person. If you compromised with address lets say C then A and B also connected to you. ABC now became the saem wallet cluster. So be careful how you consolidate / join together your coins!

Wasabi does't have profiles instead it has coincontrol feature. Every coin you have is visble sparately. When you are sending bitcoin you can decide which coin will be the most apropriate regarding and the amount and the source of that coin! Labeling system is very useful here basically it is your own wallet cluster metric.

# 3 P2P trade

Let's say your are about to make a transaction with your wallet. I put 3 different situations there.
The first one is when your wallet just communicating with a central server and basically the server will do the job. It has all the information required and all the control. There were a lot of cases when these server got hacked and users lost a lot of money. There were more cases when the user was locked out from his wallet. 
The second one when not the server but the protocol used being hacked. The wallet using their own protocol which can be defective. So there can be a middle man attack. 
The 3rd problem is when there is no third party involved which is much better basically that is the P2P communication, but still the Node can spy on you.

Here is what Wasabi do. First try to connect to a local node on your computer automatically. If it is not possible then select a random peer, connect it through Tor and broadcast the transaction. If it is still not possible for some reason then try to connect to Wasabi backend sent the transaction and let the backend broadcast it.

# 4 Use your own full node or at least use Tor.

If you are using your own full node, most of the privacy leak by network analysis are solved and Wasabi will automatically detect it and use it without a single click. You will have every information locally which is the best from privacy perspective but is has a cost it is very resource intense. 
So if you cannot do that you will have to ask nodes. We know that there are supernodes logging all information about requests. So for example to establish you total balance you have to ask the node for specific transactions related to your wallet. If it is spying on you it can start building your wallet cluster. That is why most of the light wallets are volnurable against network analysis.

Wasabi using Client side filtering means that your client has a filter set locally. With there filters your client will know which block will contains a specific transaction so instead of asking transactions from the nodes you are asking blocks. Even if the node is spying it will only know which block contains the related transaction. It is not so useful because there are a few thousand transaction in a block.

# 5 Use CoinJoin.

We got privacy on the network level but we still don't have privacy on blockchain level. The transaction chain is our enemy.
Here is Alice she has a potentially tainted coin. For example it is shes salary and she has a feeling that her boss is watching the emloyees addresses. 
Alice wants to break the chain of transactions and get rid of every heuristic. Now doing something 'celever' can be enough but who knows when there will be a heuristic that will find connection. SharedCoin failed like this, they did a lot of CoinJoin and later something called CoinJoin Sudoku partially or totally deanonimized all. So we need something which is provable. The base idea is: if the outputs are equal than amount analysis won't work. So we set up a minumum denomination 1 BTC. Every participants generate output addresses. 

# 6 Avoid servers.

This is not a trivial problem to solve this in a trustless way. There were attemts to create centralized mixers but a lot became a scam. There is 3 main problems: they can steal your money, the can collect information and create wallet clusters, the last one they know the links in the CoinJoin so they can deanomize you later.
Wasabi also has a centralized backend but it is contructed in a way that even we cannot deanonimize you. 

Wasabi using the Zerolink protocol by Ádám Ficsór. Basically it is a protocol collecting solutions for every privacy leak there can be while using a bitcoin wallet and CoinJoin.

Here is a simple block diagram how it is work technically.

# 7 Start using lighning network. 

At this point, it is too early to start leveraging LN in a privacy oriented wallet.
However, if Bitcoin is successful in the future, there will be a need to think about these questions, since blockchains don't scale.

What we are proud of:

Got the coinJoin bounty established by Gregory Maxwell in 2013
JoinMarket and WasabiWallet 10-10 BTC 


# LEGAL ASPECTS

## Wasabi Wallet fit into U.S. regulatory

Wasabi always plays by the rules. It has a company called zkSNACKs behind it, it has Terms and Conditions, Privacy Policy and Legal Issues all the documents to operate legally. However there are inconsistencies regarding the regulations among countries especially on the area of mixing and anonimity providers. For Wasabi even term was missing as it is not only a non-custodial wallet it has a unique coinjoin procedure. Now this changed on the ninth of May FinCEN published a guidance.
FinCEN is a bureau of the U.S. Department of the Treasury. Collect all rules together and give a guidance. Define terms, rules and gives some restrictions. For example Bestmixer.io which closed recently was an anonymity service provider so they should use KYC. If the platform simply facilitates the matching of crypto buyers/sellers, and the actual transactions take place off the platform, then it is not a money transmitter. However if the service acts as an intermediary to the transaction and settles trades, then it is a money transmitter subject to the BSA.
Wasabi:
- Non custodial wallet so called unhosted
- zkSNACKs not holding any BTC just coordinates the users to create the CoinJoin
- The ownership of the coins does not change. The users send their bitcoin to their own addresses.
Wasabi is an Anonymizing software provider as describe in 4.5.1(b) so it is not a money transmitter we are not under the Funds Travel Rule, basically we can continue to operate like now without KYC. 



There were some regulations before but they were inconsistent among countries. 

US treasury agains cyber criminal. Collect all rules together and give a guidance. About the actors of the system who is a miner who is and excange who is who. 
BSA: Who is money transmitter they have to identify their customer. 
custodial: hosted wallet -> money transmitter
unhosted wallet -> not financial service 
Bestmixer.io anonimity service provider, they receive the btc so they like hosted wallet they have to KYC their clients
Wasabi: non custodial, unhosted wallet - who only give an interface to construct the transaction but does not receive the btc like us. 
Anonimity service and anomity software
service: they accept the money and they transmit
our case: the mix come back to the same user you pay for yourself, so money do not change owner. 

Fincen:
FIN-2019-G001 
May 9, 2019
FINCEN GUIDANCE
Funds Travel Rule. Under this rule, if a crypto exchange is sending funds on behalf of one of its users, to another exchange, then they may need to record who the sending and receiving account holders are, and share this information with the receiving exchange.

4.5.1(b) Anonymizing software provider

Tom Robinson
- What do you think about coinjoin?
- Exchanges ask them to check the transaction or vica-versa? It is a two edged sword they can stole data like at conbase?
- The future of this? Privacy coins allowed? 
- 7000 BTC start mixing in wasabi. If we receive some official requiest we can block some inputs.

DOJO section



