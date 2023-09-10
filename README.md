# distributeBalanceForRocketpool
A layman's guide on how to distribute a Rocketpool minipool balance after withdrawing your Minipool

Special thanks to @P-tches in the Rocketpool Discord for providing the basic steps.


This guide is meant for someone who needs to use Etherscan to distribute the balance of their minipool back to their withdrawal address.
This guide assumes you have already performed a voluntary exit of your validators.

Here is an overview of what you will need to do. First, you will need to create an Etherscan account if you don't already have one. Then
you will go to your custom ABI page and set up a custom ABI for the Rocketpool delegate contract. Tnen you will call the delegate contract's
`distributeBalance` function on the delegate contract from your minipool addresses.

# Step 0: Create an Etherscan account.
Go to Etherscan.io and create an account. Make sure you are logged in.

# Step 1: Determine which delegate contract your minipool is connected to. Add the ABI of the Delegate contract
A quick explainer from the [Rocketpool docs](https://docs.rocketpool.net/guides/node/minipools/delegates.html#upgrading-your-delegate) on what the Delegate contract is:
> Every validator you run has a minipool contract as its "owner" so-to-speak. The minipool is a unique contract specifically assigned to that validator; it acts as its withdrawal address. All reward and staking balance withdrawals from the Beacon Chain will be sent to the minipool contract.
> 
> Each minipool is unique to ensure that you (the node operator) have ultimate control over it. Nobody else controls it, nobody else can change it; it's entirely at your command.
> 
> That being said, in order to minimize gas costs during node deposits, the minipool itself contains very little actual functionality. Almost everything it can do is deferred to a delegate contract.
> 
> The minipool delegate contract is a special contract that contains the bulk of the logic required by minipools - things like fairly distributing the balance between you and the pool stakers, for example. Unlike minipools, where each minipool is a unique contract, the delegate is a single contract that many minipools can "forward" requests to.
>
> Occasionally, the Rocket Pool development team will publish a new minipool delegate that adds new functionality. For example, in the Atlas update, we introduced a new delegate that had support for distributing skimmed rewards without needing to close the minipool.
>
> Minipool can have their delegates upgraded to take advantage of this new functionality. Delegate upgrades are opt-in, so you can decide if and when you want to use them. That being said, they are usually required in order to take advantage of new functionality that network upgrades introduce.

To see which delegate contract you need to use, go to your 


# Step 2. Go to your minipool address on Etherscan, click Contract, click "more options", then "Is this a proxy?"

# Step 3. Then complete the verification that the contract is a proxy contract, and click save.

# Step 4. Go back to the minipool address, click on the Contract tab, refresh the page, and "Write as proxy" should be visible.

# Step 5. Write `distributeBalance`
As of this writing it is the fifth function down. Write "false" as a parameter
