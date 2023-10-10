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
> The minipool delegate contract is a special contract that contains the bulk of the logic required by minipools - things like fairly distributing the balance between you and the pool stakers, for example. Unlike minipools, where each minipool is a unique contract, the delegate is a single contract that many minipools can "forward" requests to.
>
> Occasionally, the Rocket Pool development team will publish a new minipool delegate that adds new functionality. For example, in the Atlas update, we introduced a new delegate that had support for distributing skimmed rewards without needing to close the minipool.

To see which delegate contract you need to use, go to your 


# Step 2. Go to your minipool address on Etherscan, click Contract, click "more options", then "Is this a proxy?"
![Contract 2](https://github.com/lieberscott/distributeBalanceForRocketpool/assets/26235414/97723dc0-b56d-4b55-ae28-b12c8f2d27c7)
> If you need to find your minipool address, follow the directions below.<br/>
>
> a. Keep in mind, you have three main addresses for the purpose of tracking down your minipool address: Your originating wallet addresss, your node address, and your minipool address. <br/>
> b. Go to Etherscan.io and enter the address for your original wallet address from which you originally sent your 8ETH or 16ETH.<br/>
> c. Find the transaction from which you sent your 8TH or 16ETH (or more, if setting up multiple minipools) to the node. Click the receiving address. This is your node address.<br/>
>
> ![Finding Node 1](https://github.com/lieberscott/distributeBalanceForRocketpool/assets/26235414/4806c4d7-3ba3-460a-9dce-5a3dbb259eb0)
>
> d. Click the receiving address. This is your node address.<br/>
> e. Find the transaction where your node received the 8ETH or 16ETH from your original wallet. Right afterward, should be a "Stake" transaction. The receiver of this transaction is your minipool.<br/>
>
> ![Finding Node 2](https://github.com/lieberscott/distributeBalanceForRocketpool/assets/26235414/41973233-1284-4ba9-8a1f-e6e4bd6bb884)


# Step 3. Then complete the verification that the contract is a proxy contract, and click save.
![Proxy Contract 1](https://github.com/lieberscott/distributeBalanceForRocketpool/assets/26235414/b9c30d5e-c5b6-4d64-b310-5addaf668773)


# Step 4. Go back to the minipool address, click on the Contract tab, refresh the page, and "Write as proxy" should be visible.
![Distribute Balance 1](https://github.com/lieberscott/distributeBalanceForRocketpool/assets/26235414/f7c94cd2-b13f-4b7b-b28e-bd00c09934f0)

# Step 5. Write `distributeBalance` and enter `false` as the parameter
As of this writing it is the fifth function down. Write "false" as a parameter

# Step 6. Withdraw RPL stake
