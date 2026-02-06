# SUT Token Integration Tutorial

Complete guide to integrating SUT (SuperTrust) token payments into your application.

## What is SUT?

SUT (SuperTrust) is a utility token on the Polygon network used for AI services.

| Property | Value |
|----------|-------|
| Network | Polygon |
| Contract | `0x98965474EcBeC2F532F1f780ee37b0b05F77Ca55` |
| Decimals | 18 |

## Quick Links

- 🤖 [Live Bot Demo](https://t.me/sutisbest_bot)
- 📊 [Price Chart](https://dexscreener.com/polygon/0x98965474EcBeC2F532F1f780ee37b0b05F77Ca55)
- 💱 [Buy on QuickSwap](https://quickswap.exchange/#/swap?outputCurrency=0x98965474EcBeC2F532F1f780ee37b0b05F77Ca55)
- 📦 [Payment SDK](https://github.com/cryptoaibot1738728800/sut-pay)

## Installation

```bash
npm install ethers
```

## Verify Payment

```typescript
import { ethers } from "ethers";

const SUT_CONTRACT = "0x98965474EcBeC2F532F1f780ee37b0b05F77Ca55";

async function verifySUTPayment(txHash: string, wallet: string): Promise<number> {
  const provider = new ethers.JsonRpcProvider("https://polygon-rpc.com");
  const receipt = await provider.getTransactionReceipt(txHash);
  
  if (!receipt) return 0;
  
  const transferTopic = ethers.id("Transfer(address,address,uint256)");
  
  for (const log of receipt.logs) {
    if (log.address.toLowerCase() === SUT_CONTRACT.toLowerCase() &&
        log.topics[0] === transferTopic) {
      const to = ethers.getAddress("0x" + log.topics[2].slice(26));
      if (to.toLowerCase() === wallet.toLowerCase()) {
        return Number(ethers.formatUnits(log.data, 18));
      }
    }
  }
  return 0;
}
```

## Use Cases

1. **AI Services** - Pay for code review, content writing, analysis
2. **API Access** - Metered API usage with SUT
3. **Subscriptions** - Recurring payments in crypto
4. **Micropayments** - Low-fee small transactions

## Resources

- [SDK Repository](https://github.com/cryptoaibot1738728800/sut-pay)
- [Payment Demo](https://github.com/cryptoaibot1738728800/sut-payment-demo)
- [Telegram Bot](https://t.me/sutisbest_bot)

## License

MIT
