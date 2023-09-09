# distributeBalanceForRocketpool
A guide on how to distribute a Rocketpool minipool balance after withdrawing your Minipool

Special thanks to @P-tches in the Rocketpool Discord for providing the basic steps.


This guide is meant for someone who needs to use Etherscan to distribute the balance of their minipool back to their withdrawal address.
This guide assumes you have already performed a voluntary exit of your validators.

Here is an overview of what you will need to do. First, you will need to create an Etherscan account if you don't already have one. Then
you will go to your custom ABI page and set up a custom ABI for the Rocketpool delegate contract. Tnen you will call the delegate contract's
`distributeBalance` function on the delegate contract from your minipool addresses.

# Step 1: 
