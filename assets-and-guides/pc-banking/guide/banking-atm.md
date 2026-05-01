# ATMs

## Using an ATM

Walk up to any ATM prop in the world and interact. The ATM screen lets you deposit cash, withdraw cash, and check balance without going inside a branch.

- Branded ATMs (Fleeca, Maze, Pacific) belong to a single bank.
- Generic ATMs route to the nearest branch automatically.
- You can use someone else's card from your inventory if PIN is correct (configurable). Wrong PIN attempts are alerted to the card owner after 3 tries.

![ATM screen](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/BankingGuide/images/ATM/1.png)

## Fees and Limits

Each account gets a number of free ATM withdrawals per cycle. After that, a per-withdrawal fee applies. Fleeca = 3 free, Pacific = unlimited.

If you use a card from one bank at another bank's ATM, an inter-bank fee is charged. Server owners can configure a custom fee matrix per bank pair, or waive fees between specific partner banks.

## Credit Card Cash Advance

Credit cards can pull cash from an ATM as a cash advance - the amount is added to your card debt instead of being deducted from a checking balance. This is configurable and can be disabled server-wide.

