### Console API

$ quorum.nodeInfo returns the quorum capabilities of this node.
Example output for a node that is configured as block maker and voter:
> quorum.nodeInfo
{
  blockMakerAccount: "0x7bd175a388c7a5f33fb81bbb3b7e97cbfabb3600",
  blockmakestrategy: {
    maxblocktime: 6,
    minblocktime: 3,
    status: "active",
    type: "deadline"
  },
  canCreateBlocks: true,
  canVote: true,
  voteAccount: "0x7bd175a388c7a5f33fb81bbb3b7e97cbfabb3600"
}

$ quorum.vote accepts a block hash and votes for this hash to be the canonical head on the current height. It returns the tx hash.
> quorum.vote(eth.getBlock("latest").hash)
"0x16c69b9bdf9f10c64e65dbfe50bc997d2bc1ed321c6041db602908b7f6cab2a9"

$ quorum.canonicalHash accepts a block height and returns the canonical hash for that height (+1 will return the hash where the current pending block will be based on top of),
> quorum.canonicalHash(eth.blockNumber+1)
"0xf2c8a36d0c54c7013246fddebfc29bc881f6f10f74f761d511b5ebfaa103adfa"

$ quorum.isVoter accepts an address and returns an indication if the given address is allowed to vote for new blocks
> quorum.isVoter("0x7bd175a388c7a5f33fb81bbb3b7e97cbfabb3600")
true

$ quorum.isBlockMaker accepts an address and returns an indication if the given address is allowed to make blocks
> quorum.isBlockMaker("0x7bd175a388c7a5f33fb81bbb3b7e97cbfabb3600")
true

$ quorum.makeBlock() orders the node to create a block bypassing block maker strategy.
> quorum.makeBlock()
"0x3a07e82a48ab3c19a3d09d247e189e3a3041d1d9eafd2e1515b4ddd5b016bfd9"

$ quorum.pauseBlockMaker (temporary) orders the node to stop creating blocks
> quorum.pauseBlockMaker()
null
> quorum.nodeInfo
{
  blockMakerAccount: "0x7bd175a388c7a5f33fb81bbb3b7e97cbfabb3600",
  blockmakestrategy: {
    maxblocktime: 6,
    minblocktime: 3,
    status: "paused",
    type: "deadline"
  },
  canCreateBlocks: true,
  canVote: true,
  voteAccount: "0x7bd175a388c7a5f33fb81bbb3b7e97cbfabb3600"
}

$ quorum.resumeBlockMaker instructs the node to begin creating blocks again when its paused.
> quorum.resumeBlockMaker()
null
> quorum.nodeInfo
{
  blockMakerAccount: "0x7bd175a388c7a5f33fb81bbb3b7e97cbfabb3600",
  blockmakestrategy: {
    maxblocktime: 6,
    minblocktime: 3,
    status: "active",
    type: "deadline"
  },
  canCreateBlocks: true,
  canVote: true,
  voteAccount: "0x7bd175a388c7a5f33fb81bbb3b7e97cbfabb3600"
}

### Command line flags
QUORUM OPTIONS:
  --voteaccount value		Address that is used to vote for blocks
  --votepassword value		Password to unlock the voting address
  --blockmakeraccount value	Address that is used to create blocks
  --blockmakerpassword value	Password to unlock the block maker address
  --singleblockmaker		Indicate this node is the only node that can create blocks
  --minblocktime value		Set minimum block time (default: 3)
  --maxblocktime value		Set max block time (default: 10)
