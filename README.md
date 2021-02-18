# Ethers Typed Data (Legacy)

Signs typed data as per legacy version of [EIP 712](https://eips.ethereum.org/EIPS/eip-712). \
It's a copy of [ethers-typed-data](https://www.npmjs.com/package/ethers-typed-data) package that doesn't set the `salt` parameter in the `domain` description. \
Useful when working with the legacy implementation contracts like [DAI](https://etherscan.io/address/0x6b175474e89094c44da98b954eedeac495271d0f). 

## Installation

```
npm install ethers-typed-data-legacy --save
```

## Usage

```typescript
import { buildTypedData, hashTypedData } from 'ethers-typed-data-legacy';

const typedData = buildTypedData(
  {
    name: 'test',
  },
  'Bid',
  {
    Identity: [
      { type: 'uint256', name: 'userId' },
      { type: 'address', name: 'wallet' },
    ],
    Bid: [
      { type: 'uint256', name: 'amount' },
      { type: 'Identity', name: 'bidder' },
    ],
  },
  {
    amount: 100,
    bidder: {
      userId: 10,
      wallet: '0xEEb4801FBc9781EEF20801853C1Cb25faB8A7a3b',
    },
  },
);

console.log('typed data:', typedData);

const hash = hashTypedData(typedData);

console.log('typed data hash:', hash);
```

## License

MIT License.
