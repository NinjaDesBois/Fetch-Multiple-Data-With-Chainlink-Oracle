# Fetch-Multiple-Data-With-Chainlink-Oracle
This repo is for our hackaton's project (Chainlink) a smart contract + a job to fetch data from Snapshot and update our smart contract with new Data (Special thank to Ijonas who helps us for this repo :https://gist.github.com/ijonas) 
Here's an example of fetching votes of a Snapshot proposal.

The URL being fetched from the snapshotvotes.sol's requestVotes(url) function would be something like

https://hub.snapshot.org/graphql?operationName=Votes&query=query%20Votes%20%7B%0A%20%20proposal%20(id%3A%20%220xdc18efd665d776ef388aafa8385f3a63e6c2220641d04ec109a3c3c7d19e915d%22)%20%7B%0A%20%20%20%20scores%0A%20%20%20%20quorum%0A%20%20%7D%0A%7D%0A

The snapshotvotes.sol smartcontract sends the job request with URL to the following

oracle contract address: 0xd23cB7C9bDa53734ef4595F7a23398a85443246E
job Id: 8ebf12e2380f4a78afe3f74eac1d3f97
The getvotes.toml extracts the following 3 JSON values

yays - data,proposal,scores,0
nays - data,proposal,scores,1
abstentions - data,proposal,scores,2
and returns them to fulfillVotes(...) callback function on the smartcontract.

NOTE: After you deploy the snapshotvotes.sol smartcontract, remember to transfer testnet LINK to the smartcontract otherwise your job won't reach the Chainlink node. Each invocation costs 0.05LINK.
