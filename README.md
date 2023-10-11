# distributeBalanceForRocketpool
A layman's guide on how to distribute a Rocketpool minipool balance after withdrawing your Minipool

Special thanks to @P-tches in the Rocketpool Discord for providing the basic steps.


This guide is meant for someone who needs to use Etherscan to distribute the balance of their minipool back to their withdrawal address.
This guide assumes you have already performed a voluntary exit of your validators.[^1]

Here are the steps:
✅ Create an Etherscan account if you don't already have one
✅ Set up a custom ABI for the Rocketpool delegate contract
✅ Call the delegate contract's `distributeBalance` function from your minipool addresses.

# Step 0: Create an Etherscan account.
Go to Etherscan.io and create an account. Make sure you are logged in.

# Step 1: Determine which delegate contract your minipool is connected to. Add the ABI of the Delegate contract
A quick explainer from the [Rocketpool docs](https://docs.rocketpool.net/guides/node/minipools/delegates.html#upgrading-your-delegate) on what the Delegate contract is:
> The minipool delegate contract is a special contract that contains the bulk of the logic required by minipools - things like fairly distributing the balance between you and the pool stakers, for example. Unlike minipools, where each minipool is a unique contract, the delegate is a single contract that many minipools can "forward" requests to.
>
> Occasionally, the Rocket Pool development team will publish a new minipool delegate that adds new functionality. For example, in the Atlas update, we introduced a new delegate that had support for distributing skimmed rewards without needing to close the minipool.

To see which delegate contract you need to use, go to your minipool address on Etherscan, click Contract, "Read Contract", then `getDelegate`
![Screen Shot 2023-10-10 at 1 50 18 PM](https://github.com/lieberscott/distributeBalanceForRocketpool/assets/26235414/aa8338a8-df73-4898-ab8f-5174e82b946e)

> If you need to find your minipool address, follow the directions below.<br/>
> .<br/>
> a. Keep in mind, you have three main addresses for the purpose of tracking down your minipool address: Your originating wallet addresss, your node address, and your minipool address. <br/>
> b. Go to Etherscan.io and enter the address for your original wallet address from which you originally sent your 8ETH or 16ETH.<br/>
> c. Find the transaction from which you sent your 8TH or 16ETH (or more, if setting up multiple minipools) to the node. Click the receiving address. This is your node address.<br/>
> .<br/>
> ![Finding Node 1](https://github.com/lieberscott/distributeBalanceForRocketpool/assets/26235414/4806c4d7-3ba3-460a-9dce-5a3dbb259eb0)
> .<br/>
> d. Click the receiving address. This is your node address.<br/>
> e. Find the transaction where your node received the 8ETH or 16ETH from your original wallet. Right afterward, should be a "Stake" transaction. The receiver of this transaction is your minipool.<br/>
> .<br/>
> ![Finding Node 2](https://github.com/lieberscott/distributeBalanceForRocketpool/assets/26235414/41973233-1284-4ba9-8a1f-e6e4bd6bb884)

# Step 2. Go to your minipool address on Etherscan, click Contract, click "more options", then "Is this a proxy?"
![Contract 2](https://github.com/lieberscott/distributeBalanceForRocketpool/assets/26235414/97723dc0-b56d-4b55-ae28-b12c8f2d27c7)

# Step 3. Then complete the verification that the contract is a proxy contract, and click save.
![Proxy Contract 1](https://github.com/lieberscott/distributeBalanceForRocketpool/assets/26235414/b9c30d5e-c5b6-4d64-b310-5addaf668773)


# Step 4. Go back to the minipool address, click on the Contract tab, refresh the page, and "Write as proxy" should be visible.
![Distribute Balance 1](https://github.com/lieberscott/distributeBalanceForRocketpool/assets/26235414/f7c94cd2-b13f-4b7b-b28e-bd00c09934f0)

# Step 5. Write `distributeBalance` and enter `false` as the parameter
As of this writing it is the fifth function down. Write "false" as a parameter

# Step 6. Withdraw RPL stake
**NOTE: You can only withdraw your RPL stake by calling the `withdrawRPL` function with your node address. It will be withdrawn to your withdrawal address (if set, otherwise to node address).**

**Also, you must wait at least 28 days from your last stake (or re-stake) or the transaction will fail**


a. Sign in to Metamask or another Web3 wallet using your node credentials.
b. Go to the most recent RPL deployer contract on Etherscan. As of this writing, it is (v3)[https://etherscan.io/address/0x0d8d8f8541b12a0e1194b7cc4b6d954b90ab82ec#code].
c. Go to the Contract tab, Read Contract, then `getNodeRPLStake`. Input your validator address.
![Screen Shot 2023-10-10 at 2 08 12 PM](https://github.com/lieberscott/distributeBalanceForRocketpool/assets/26235414/04468c65-6016-44fa-974c-4ef9853e0397)
d. Copy the result. It will look like a very big number. This is your RPL stake (in wei).
e. Go to the Write Contract tab. Connect your node address to Etherscan using a Web3 wallet.
f. Click `withdrawRPL`, enter the number you just copied and write.
![Screen Shot 2023-10-10 at 2 15 04 PM](https://github.com/lieberscott/distributeBalanceForRocketpool/assets/26235414/6506d879-76d3-4b6d-8cdf-6d850e2f379c)

[^1]If you need to do that step, this (video is very helpful)[https://www.youtube.com/watch?v=KoBAacMWA_k].
