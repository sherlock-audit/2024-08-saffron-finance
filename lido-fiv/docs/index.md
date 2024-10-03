# Solidity API

## LidoVault

### id

```solidity
uint256 id
```

Vault ID set by the factory

### duration

```solidity
uint256 duration
```

Length of the earning period of the vault in seconds

### startTime

```solidity
uint256 startTime
```

Start of vault

_Calculated when vault starts via block.timestamp_

### endTime

```solidity
uint256 endTime
```

End of duration

_Calculated when vault starts via (block.timestamp + duration)_

### fixedSideCapacity

```solidity
uint256 fixedSideCapacity
```

Total capacity of the fixed side

### variableSideCapacity

```solidity
uint256 variableSideCapacity
```

Total capacity of the variable side

### protocolFeeBps

```solidity
uint256 protocolFeeBps
```

Saffron protocol fee in basis points

### appliedProtocolFee

```solidity
uint256 appliedProtocolFee
```

ETH amount that tracks the Saffron protocol fee applied to withdrawn Lido staking earnings. It is reset when the fee reciever withdraws

### totalProtocolFee

```solidity
uint256 totalProtocolFee
```

ETH amount that tracks the total Saffron protocol fee from variable withdrawal staking earnings while the vault is still ongoing

### protocolFeeReceiver

```solidity
address protocolFeeReceiver
```

Address that collects the Saffron protocol fee

### earlyExitFeeBps

```solidity
uint256 earlyExitFeeBps
```

Penalty fee in basis points for fixed side early withdrawals that is quadratically scaled based off of the amount of time that has elapsed since the vault started

### fixedSidestETHOnStartCapacity

```solidity
uint256 fixedSidestETHOnStartCapacity
```

Total stETH capacity of the fixed side on vault start

### minimumDepositAmount

```solidity
uint256 minimumDepositAmount
```

Minimum amount of ETH that can be deposited for variable or fixed side users

### minimumFixedDepositBps

```solidity
uint256 minimumFixedDepositBps
```

Minimum amount of the fixed capacity that can be deposited for fixed side users on a single deposit in basis points

### fixedClaimToken

```solidity
mapping(address => uint256) fixedClaimToken
```

Mock ERC20 bearer token that entitles owner to a portion of the fixed side bearer tokens and the variable side premium payment
It represents the amount of StETH shares generated from Lido staking submit on fixed side deposits

_If the vault hasn't started, this is used to return the fixed side deposit_

### fixedClaimTokenTotalSupply

```solidity
uint256 fixedClaimTokenTotalSupply
```

### fixedBearerToken

```solidity
mapping(address => uint256) fixedBearerToken
```

Mock ERC20 bearer token that entitles owner to a portion of the fixed side deposits after the vault has ended and the ETH has been unstaked from Lido

### fixedBearerTokenTotalSupply

```solidity
uint256 fixedBearerTokenTotalSupply
```

### fixedIntialTokenTotalSupply

```solidity
uint256 fixedIntialTokenTotalSupply
```

Mock ERC20 bearer token that entitles owner to a portion of the fixed side bearer tokens and the variable side premium payment
It represents total amount of StETH shares generated from Lido staking submit on fixed side deposits

### fixedETHDepositToken

```solidity
mapping(address => uint256) fixedETHDepositToken
```

Mock ERC20 bearer token that tracks fixed user's ETH deposits in order to determine when the fixed capacity is reached

### fixedETHDepositTokenTotalSupply

```solidity
uint256 fixedETHDepositTokenTotalSupply
```

### variableBearerToken

```solidity
mapping(address => uint256) variableBearerToken
```

Mock ERC20 bearer token that entitles owner to a portion of the vault earnings

### variableBearerTokenTotalSupply

```solidity
uint256 variableBearerTokenTotalSupply
```

### feeEarnings

```solidity
uint256 feeEarnings
```

Amount of earnings from fixed side early exit fees

### withdrawnFeeEarnings

```solidity
uint256 withdrawnFeeEarnings
```

Fee earnings that have been withdrawn from the variable side

### withdrawnStakingEarningsInStakes

```solidity
uint256 withdrawnStakingEarningsInStakes
```

Amount of earnings from Lido Staking in lido stakes already withdrawn by variable depositors

### withdrawnStakingEarnings

```solidity
uint256 withdrawnStakingEarnings
```

Amount of earnings from Lido Staking in ETH already withdrawn by variable depositors

### vaultEndedWithdrawalRequestIds

```solidity
uint256[] vaultEndedWithdrawalRequestIds
```

Lido withdraw request ids for after the vault has ended

### vaultEndedWithdrawalsFinalized

```solidity
bool vaultEndedWithdrawalsFinalized
```

The vault ended Lido withdrawal requests have been claimed and all the staked Lido ETH has been withdrawn

_True if the remaining Lido ETH funds have been withdrawn from Lido_

### vaultEndedStakingEarnings

```solidity
uint256 vaultEndedStakingEarnings
```

Amount of earnings in ETH from Lido Staking after the vault has ended

### vaultEndingStakesAmount

```solidity
uint256 vaultEndingStakesAmount
```

Amount of lido stETH stakes in Lido Vault at the moment of vault has ending

### vaultEndingETHBalance

```solidity
uint256 vaultEndingETHBalance
```

Balance of Lido Vault in ETH at the moment of vault has ending

### vaultEndedFixedDepositsFunds

```solidity
uint256 vaultEndedFixedDepositsFunds
```

Amount of ETH used to cover the returning of fixed user's initial principal

### userToFixedUpfrontPremium

```solidity
mapping(address => uint256) userToFixedUpfrontPremium
```

Mapping from user addresses to the upfront premium a fixed depositor received from the variable side

### fixedToVaultNotStartedWithdrawalRequestIds

```solidity
mapping(address => uint256[]) fixedToVaultNotStartedWithdrawalRequestIds
```

Mapping from user addresses to their withdrawal request ids before the vault has started

### WithdrawalRequest

```solidity
struct WithdrawalRequest {
  uint256 timestamp;
  uint256[] requestIds;
}
```

### fixedToVaultOngoingWithdrawalRequestIds

```solidity
mapping(address => struct LidoVault.WithdrawalRequest) fixedToVaultOngoingWithdrawalRequestIds
```

Mapping from fixed side user addresses to their withdrawal request ids after the vault has started but before the vault has ended

### getFixedOngoingWithdrawalRequestTimestamp

```solidity
function getFixedOngoingWithdrawalRequestTimestamp(address user) public view returns (uint256)
```

Add getter functions for each field in the struct b/c the compiler doesn't know how to construct the "free" getter that usually comes with public

### getFixedOngoingWithdrawalRequestIds

```solidity
function getFixedOngoingWithdrawalRequestIds(address user) public view returns (uint256[])
```

### getFixedToVaultNotStartedWithdrawalRequestIds

```solidity
function getFixedToVaultNotStartedWithdrawalRequestIds(address user) public view returns (uint256[])
```

### getVariableToVaultOngoingWithdrawalRequestIds

```solidity
function getVariableToVaultOngoingWithdrawalRequestIds(address user) public view returns (uint256[])
```

### fixedOngoingWithdrawalUsers

```solidity
address[] fixedOngoingWithdrawalUsers
```

Store array of all fixed users with pending ongoing withdrawals to iterate through fixedToVaultOngoingWithdrawalRequestIds mapping if the vault ends

### fixedToPendingWithdrawalAmount

```solidity
mapping(address => uint256) fixedToPendingWithdrawalAmount
```

When the vault ends ongoing fixed withdrawals may be claimed by another user
this stores the amount they should be given when the user eventually withdraws

### variableToPendingWithdrawalAmount

```solidity
mapping(address => uint256) variableToPendingWithdrawalAmount
```

Mapping from variable side user addresses to their withdrawal amount after the vault has started
this stores the amount they should be given when the user eventually withdraws

### variableToVaultOngoingWithdrawalRequestIds

```solidity
mapping(address => uint256[]) variableToVaultOngoingWithdrawalRequestIds
```

Mapping from variable side user addresses to their withdrawal request ids after the vault has started but before the vault has ended

### variableToWithdrawnStakingEarnings

```solidity
mapping(address => uint256) variableToWithdrawnStakingEarnings
```

Mapping from variable side user addresses to their total withdrawn staking earnings amount right after their Lido withdrawal request is submitted

### variableToWithdrawnStakingEarningsInShares

```solidity
mapping(address => uint256) variableToWithdrawnStakingEarningsInShares
```

Mapping from variable side user addresses to their total withdrawn staking earnings amount in lido shares right after their Lido withdrawal request is submitted

### variableToWithdrawnProtocolFee

```solidity
mapping(address => uint256) variableToWithdrawnProtocolFee
```

Mapping from variable side user addresses to their total payed protocol fee amount right after their Lido withdrawal request is submitted

### variableToWithdrawnFees

```solidity
mapping(address => uint256) variableToWithdrawnFees
```

Mapping from variable side user addresses to their total withdrawn fees amount right after their Lido withdrawal request is claimed

### VaultInitialized

```solidity
event VaultInitialized(uint256 vaultId, uint256 duration, uint256 variableSideCapacity, uint256 fixedSideCapacity, uint256 earlyExitFeeBps, uint256 protocolFeeBps, address protocolFeeReceiver)
```

Emitted when a new vault is initialized

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| vaultId | uint256 | ID of vault |
| duration | uint256 | How long the vault will be locked once started, in seconds |
| variableSideCapacity | uint256 | Maximum capacity of variable side |
| fixedSideCapacity | uint256 | Maximum capacity of fixed side |
| earlyExitFeeBps | uint256 | Fixed depositor early exit fee in basis points |
| protocolFeeBps | uint256 | Protocol fee in basis points |
| protocolFeeReceiver | address | Address that collects protocol fee |

### VariableFundsDeposited

```solidity
event VariableFundsDeposited(uint256 amount, address user)
```

Emitted when variable funds are deposited into the vault

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amount | uint256 | ETH amount deposited |
| user | address | Address of user |

### FixedFundsDeposited

```solidity
event FixedFundsDeposited(uint256 amount, uint256 shares, address user)
```

Emitted when fixed funds are deposited into the vault

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amount | uint256 | ETH amount deposited |
| shares | uint256 | stETH shares issued for Lido submit |
| user | address | Address of user |

### FixedPremiumClaimed

```solidity
event FixedPremiumClaimed(uint256 premium, uint256 shares, address user)
```

Emitted when a fixed user claims their upfront premium

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| premium | uint256 | Fixed upfront premium transferred to the fixed user |
| shares | uint256 | stETH shares claimed |
| user | address | Address of user |

### VariableFundsWithdrawn

```solidity
event VariableFundsWithdrawn(uint256 amount, address user, bool isStarted, bool isEnded)
```

Emitted when variable funds are withdrawn from the vault

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amount | uint256 | Amount withdrawn |
| user | address | Address of user |
| isStarted | bool | Indicates whether the vault has started when the funds were withdrawn |
| isEnded | bool | Indicates whether the vault has ended when the funds were withdrawn |

### FixedFundsWithdrawn

```solidity
event FixedFundsWithdrawn(uint256 amount, address user, bool isStarted, bool isEnded)
```

Emitted when fixed funds are withdrawn from the vault

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amount | uint256 | Amount withdrawn |
| user | address | Address of user |
| isStarted | bool | Indicates whether the vault has started when the funds were withdrawn |
| isEnded | bool | Indicates whether the vault has ended when the funds were withdrawn |

### VaultStarted

```solidity
event VaultStarted(uint256 timeStarted, address user)
```

Emitted when the vault capacities have been met and the vault has been moved into the started phase

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| timeStarted | uint256 | Time the vault started |
| user | address | Address of user that triggered the start of the vault |

### VaultEnded

```solidity
event VaultEnded(uint256 timeEnded, address user)
```

Emitted when the vault has passed its end time and moved into the ended phase

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| timeEnded | uint256 | Time the vault ended |
| user | address | Address of user that triggered the end of the vault |

### LidoWithdrawalRequested

```solidity
event LidoWithdrawalRequested(address user, uint256[] requestIds, uint256 side, bool isStarted, bool isEnded)
```

Emitted when stakings funds are requested to be withdrawn from Lido

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| user | address | Address of user |
| requestIds | uint256[] | Request ids of the Lido withdrawal requests |
| side | uint256 | Indicates fixed or variable side requested |
| isStarted | bool | Indicates whether the vault has started when the funds were requested to be withdrawn |
| isEnded | bool | Indicates whether the vault has ended when the funds were requested to be withdrawn |

### LidoWithdrawalFinalized

```solidity
event LidoWithdrawalFinalized(address user, uint256[] requestIds, uint256 side, bool isStarted, bool isEnded)
```

Emitted when a Lido withdrawal is claimed and the ETH is transferred to the adapter contract

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| user | address | Address of user |
| requestIds | uint256[] | Request ids of the Lido withdrawal requests |
| side | uint256 | Indicates fixed or variable side requested |
| isStarted | bool | Indicates whether the vault has started when the funds were requested to be withdrawn |
| isEnded | bool | Indicates whether the vault has ended when the funds were submitted for withdrawal |

### constructor

```solidity
constructor(bool _initialize) public
```

### initialize

```solidity
function initialize(struct ILidoVaultInitializer.InitializationParams params) external
```

Initializes the vault

_make sure this is only callable by the contract creator aka the vault factory_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | struct ILidoVaultInitializer.InitializationParams | Initialization parameters |

### receive

```solidity
receive() external payable
```

Function to receive Ether. msg.data must be empty

### isStarted

```solidity
function isStarted() public view returns (bool)
```

True if the vault has started

### isEnded

```solidity
function isEnded() public view returns (bool)
```

True if the vault has ended

### deposit

```solidity
function deposit(uint256 side) external payable
```

Deposit ETH into the vault

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| side | uint256 | ID of side to deposit into |

### claimFixedPremium

```solidity
function claimFixedPremium() external
```

Claim fixed side bearer tokens with fixed side claim tokens
and transfer to the user their upfront premium from variable deposits

### withdraw

```solidity
function withdraw(uint256 side) external
```

Withdraw from the vault

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| side | uint256 | ID of side to withdraw from |

### finalizeVaultNotStartedFixedWithdrawals

```solidity
function finalizeVaultNotStartedFixedWithdrawals() external
```

Finalize a fixed withdrawal that was requested before the vault started

### finalizeVaultOngoingFixedWithdrawals

```solidity
function finalizeVaultOngoingFixedWithdrawals() external
```

Finalize a fixed withdrawal that was requested after the vault has started

### finalizeVaultOngoingVariableWithdrawals

```solidity
function finalizeVaultOngoingVariableWithdrawals() external
```

Finalize a variable withdrawal that was requested after the vault has started

### feeReceiverFinalizeVaultOngoingVariableWithdrawals

```solidity
function feeReceiverFinalizeVaultOngoingVariableWithdrawals(address user) external
```

Protocol Fee Reciever only Finalize a variable withdrawal that was requested after the vault has started

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| user | address | for whom the reward amount is due |

### withdrawAmountVariablePending

```solidity
function withdrawAmountVariablePending() public
```

withdrawal of funds for Variable side

### finalizeVaultEndedWithdrawals

```solidity
function finalizeVaultEndedWithdrawals(uint256 side) external
```

Finalize the vault ended withdrawals

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| side | uint256 | ID of side |

### claimOngoingFixedWithdrawals

```solidity
function claimOngoingFixedWithdrawals() internal
```

### applyProtocolFee

```solidity
function applyProtocolFee(uint256 stakingEarnings) internal returns (uint256)
```

Helper function to apply Saffron's protocol fee to Lido staking earnings

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| stakingEarnings | uint256 | the amount of ETH staking earnings on Lido |

### vaultEndedWithdraw

```solidity
function vaultEndedWithdraw(uint256 side) internal
```

Helper function to do the accounting for a withdraw after the vault has ended

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| side | uint256 | ID of side |

### fixedLidoSharesTotalSupply

```solidity
function fixedLidoSharesTotalSupply() internal view returns (uint256)
```

Returns all fixed side Lido shares - claimed or unclaimed

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | totalSupply Total supply of the fixed bearer and claim tokens |

### claimFixedVaultOngoingWithdrawal

```solidity
function claimFixedVaultOngoingWithdrawal(address user) internal returns (uint256)
```

Helper function to claim a Lido fixed withdrawal that was requested after the vault has started

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| user | address | User that requested the withdrawal |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | amount Amount of ETH withdrawn from Lido after the withdraw has been claimed minus the early exit fees |

### protocolFeeReceiverWithdraw

```solidity
function protocolFeeReceiverWithdraw() internal
```

Helper function to withdraw any accrued protocol fees

### calculateVariableWithdrawState

```solidity
function calculateVariableWithdrawState(uint256 totalEarnings, uint256 previousWithdrawnAmount) internal view returns (uint256, uint256)
```

Helper function to calculate the ongoing variable withdraw state
The vault must track a variable user's withdrawals during the duration of the vault since withdrawals can be executed at any time

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| totalEarnings | uint256 | Amount of staking or fee earnings |
| previousWithdrawnAmount | uint256 | The total amount of earnings already withdrawn |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | (currentState, amountOwed) The new total amount of earnings withdrawn, the amount to withdraw |
| [1] | uint256 |  |

### getCalculateVariableWithdrawStateWithStakingBalance

```solidity
function getCalculateVariableWithdrawStateWithStakingBalance(address user) public view returns (uint256)
```

Helper function to calculate the ongoing variable withdraw state
The vault must track a variable user's withdrawals during the duration of the vault since withdrawals can be executed at any time

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| user | address | for whom the withdrawal variable amount is calculated |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | (ethAmountOwed) The amount to withdraw |

### calculateVariableWithdrawStateWithUser

```solidity
function calculateVariableWithdrawStateWithUser(uint256 totalEarnings, uint256 previousWithdrawnAmount, address user) internal view returns (uint256, uint256)
```

Helper function to calculate the ongoing variable withdraw state for user
The vault must track a variable user's withdrawals during the duration of the vault since withdrawals can be executed at any time

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| totalEarnings | uint256 | Amount of staking or fee earnings |
| previousWithdrawnAmount | uint256 | The total amount of earnings already withdrawn |
| user | address | for whom the calculation |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | (currentState, amountOwed) The new total amount of earnings withdrawn, the amount to withdraw |
| [1] | uint256 |  |

### getCalculateVariableFeeEarningsShareWithUser

```solidity
function getCalculateVariableFeeEarningsShareWithUser(address user) public view returns (uint256, uint256)
```

Helper function to calculate a variable user's proportional amount of fees that they are owed

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| user | address | for which the variable amount of the user proportional to the commission due to him is calculated |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | (currentState, feeEarningsShare) The new total amount of earnings withdrawn, the amount to fee share |
| [1] | uint256 |  |

### calculateVariableFeeEarningsShare

```solidity
function calculateVariableFeeEarningsShare() internal returns (uint256)
```

Helper function to calculate a variable user's proportional amount of fees that they are owed

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | amount The amount to give the user |

### calculateVariableFeeEarningsShareWithUser

```solidity
function calculateVariableFeeEarningsShareWithUser(address user) internal returns (uint256)
```

A helper function to calculate the proportional amount of the reward due to the user that is passed in the variable

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| user | address | to whom the reward amount is due |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | amount The amount to give the user |

### calculateFixedEarlyExitFees

```solidity
function calculateFixedEarlyExitFees(uint256 upfrontPremium, uint256 timestampRequested) internal view returns (uint256)
```

Helper function to calculate the total fees to apply to a fixed user's principal that they are requesting to withdraw
The earlier in the vault duration the withdraw request is made the higher the fee
The user must also pay back their upfront premium

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| upfrontPremium | uint256 | Upfront premium the fixed user received |
| timestampRequested | uint256 | When the withdraw was requested |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | earlyExitFee The total amount of early exit fees to apply |

### lido

```solidity
contract ILido lido
```

Lido contract

### lidoWithdrawalQueue

```solidity
contract ILidoWithdrawalQueueERC721 lidoWithdrawalQueue
```

Lido withdrawal queue contract

### LIDO_ERROR_TOLERANCE_ETH

```solidity
uint256 LIDO_ERROR_TOLERANCE_ETH
```

ETH diff tolerance either for the expected deposit or withdraw from Lido - some rounding errors of a few wei seem to occur

### VaultSet

```solidity
event VaultSet(address vault, address setter)
```

Emitted when the vault contract address is updated

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| vault | address | New vault address |
| setter | address | Address of setter |

### FundsStaked

```solidity
event FundsStaked(uint256 amount, uint256 shares, address user)
```

Emitted when ETH is submitted to the Lido platform for staking

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amount | uint256 | ETH amount staked |
| shares | uint256 | Amount of shares received for the ETH staked |
| user | address | User address |

### FundsTransferred

```solidity
event FundsTransferred(uint256 amount, address recipient)
```

Emitted when withdrawn funds are transferred out of this contract

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amount | uint256 | ETH amount transferred |
| recipient | address | Address of receiver of the funds |

### TransferredStETH

```solidity
event TransferredStETH(uint256 amount, address recipient)
```

Emitted when stETH funds are transferred out of this contract

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amount | uint256 | ETH amount transferred |
| recipient | address | Address of receiver of the stETH |

### TransferredWithdrawalERC721

```solidity
event TransferredWithdrawalERC721(uint256 requestId, address recipient)
```

Emitted when a Lido withdrawal request ERC721 is transferred out of this contract

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| requestId | uint256 | Request id of the Lido withdrawal request |
| recipient | address | Address of receiver of the ERC721 |

### WithdrawalRequested

```solidity
event WithdrawalRequested(uint256 amount, uint256[] requestIds, address user)
```

Emitted when stakings funds are requested to be withdrawn from Lido

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amount | uint256 | ETH amount requested to be withdrawn |
| requestIds | uint256[] | Request ids of the Lido withdrawal requests |
| user | address | User address |

### WithdrawalClaimed

```solidity
event WithdrawalClaimed(uint256 amount, uint256[] requestIds, address user)
```

Emitted when a Lido fixed withdrawal is claimed and the ETH is transferred to this contract

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amount | uint256 | ETH amount withdrawn |
| requestIds | uint256[] | Request ids of the Lido withdrawal requests |
| user | address | User address |

### minStETHWithdrawalAmount

```solidity
function minStETHWithdrawalAmount() public pure returns (uint256)
```

The minimum amount of stETH that can be withdrawn from Lido

### maxStETHWithdrawalAmount

```solidity
function maxStETHWithdrawalAmount() external pure returns (uint256)
```

The maximum amount of stETH that can be withdrawn from Lido in a single request
If desired amount to withdraw is greater than the value it has to be broken up into multiple requests

### stakingBalance

```solidity
function stakingBalance() public view returns (uint256)
```

Balance of stETH tokens, which is dynamic based off of staking rewards https://docs.lido.fi/contracts/lido#rebase

### thisBalance

```solidity
function thisBalance() public view returns (uint256)
```

### stakingShares

```solidity
function stakingShares() public view returns (uint256)
```

Balance of Lido stakes

### transferWithdrawnFunds

```solidity
function transferWithdrawnFunds(address recipient, uint256 amount) internal
```

Transfers ETH unstaked from Lido

_Make sure this is only callable by the vault_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| recipient | address | Address to transfer to |
| amount | uint256 | Amount of ETH |

### requestWithdrawViaShares

```solidity
function requestWithdrawViaShares(address user, uint256 shares) internal returns (uint256[])
```

Request a withdrawal on Lido to exchange stETH for ETH via shares amount

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| user | address | Address of the user that is requesting the withdraw |
| shares | uint256 | Amount of staking shares to withdraw. Will be used to calculate the actual stETH amount to withdraw |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256[] | requestIds Ids of the withdrawal requests |

### requestEntireBalanceWithdraw

```solidity
function requestEntireBalanceWithdraw(address user) internal returns (uint256[])
```

Request a withdrawal of the entire stETH balance of the contract

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| user | address | Address of the user that is requesting the withdraw |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256[] | requestIds Ids of the withdrawal requests |

### requestWithdrawViaETH

```solidity
function requestWithdrawViaETH(address user, uint256 stETHAmount) internal returns (uint256[])
```

Request a withdrawal on Lido to exchange stETH for ETH via stETH amount

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| user | address | Address of the user that is requesting the withdraw |
| stETHAmount | uint256 | Amount of stETH to withdraw |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256[] | requestIds Ids of the withdrawal requests |

### _requestWithdraw

```solidity
function _requestWithdraw(address user, uint256 stETHAmount) internal returns (uint256[])
```

Request a withdrawal on Lido to exchange stETH for ETH

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| user | address |  |
| stETHAmount | uint256 | amount of stETH to withdraw |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256[] | requestIds Ids of the withdrawal requests |

### claimWithdrawals

```solidity
function claimWithdrawals(address user, uint256[] requestIds) internal returns (uint256)
```

Claim a withdrawal request on Lido once it has been finalized. This will transfer ETH to the contract if successful

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| user | address | Address of the user that is claiming the withdraw |
| requestIds | uint256[] | Withdrawal request ids to claim |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | amount of ETH withdrawn |

### _claimWithdrawals

```solidity
function _claimWithdrawals(address user, uint256[] requestIds) internal returns (uint256)
```

Claim a withdrawal request on Lido once it has been finalized

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| user | address |  |
| requestIds | uint256[] | Ids of the withdrawal requests |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | amount of ETH withdrawn |

### calculateWithdrawals

```solidity
function calculateWithdrawals(uint256 stETHAmount) internal pure returns (uint256[])
```

Helper function to calculate how many requests will be needed to unstake from Lido due to the maximum withdrawal amount per request

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| stETHAmount | uint256 | stETH amount requested to be withdrawn |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256[] | withdrawalAmounts an array of the amounts to withdraw in each withdrawal request to Lido |

## ILido

### submit

```solidity
function submit(address _referral) external payable returns (uint256)
```

Send funds to the pool with optional _referral parameter

_This function is alternative way to submit funds. Supports optional referral address._

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | Amount of StETH shares generated |

### transfer

```solidity
function transfer(address _recipient, uint256 _amount) external returns (bool)
```

Moves `_amount` tokens from the caller's account to the `_recipient` account.

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | bool | a boolean value indicating whether the operation succeeded. |

### approve

```solidity
function approve(address spender, uint256 amount) external returns (bool)
```

Sets amount as the allowance of spender over the caller’s StETH tokens.

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | bool | bool indicating whether the operation succeeded |

### getPooledEthByShares

```solidity
function getPooledEthByShares(uint256 _sharesAmount) external view returns (uint256)
```

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | uint256 Returns the amount of ether that corresponds to _sharesAmount token shares. |

### getSharesByPooledEth

```solidity
function getSharesByPooledEth(uint256 _ethAmount) external view returns (uint256)
```

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | the amount of shares that corresponds to `_ethAmount` protocol-controlled Ether. |

### balanceOf

```solidity
function balanceOf(address account) external view returns (uint256)
```

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | uint256 Returns stETH balance of the account |

### sharesOf

```solidity
function sharesOf(address _account) external view returns (uint256)
```

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | uint256 Returns amount of shares owned by account. |

## ILidoVault

### initialize

```solidity
function initialize(struct ILidoVaultInitializer.InitializationParams params) external
```

Initializes the vault

_make sure this is only callable by the contract creator aka the vault factory_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| params | struct ILidoVaultInitializer.InitializationParams | Initialization parameters |

## ILidoVaultInitializer

Defines the parameter struct used during vault initialization

### InitializationParams

```solidity
struct InitializationParams {
  uint256 vaultId;
  uint256 duration;
  uint256 fixedSideCapacity;
  uint256 variableSideCapacity;
  uint256 earlyExitFeeBps;
  uint256 protocolFeeBps;
  address protocolFeeReceiver;
}
```

## ILidoWithdrawalQueueERC721

### WithdrawalRequestStatus

```solidity
struct WithdrawalRequestStatus {
  uint256 amountOfStETH;
  uint256 amountOfShares;
  address owner;
  uint256 timestamp;
  bool isFinalized;
  bool isClaimed;
}
```

### requestWithdrawals

```solidity
function requestWithdrawals(uint256[] _amounts, address _owner) external returns (uint256[] requestIds)
```

Batch request the _amounts of stETH for withdrawal to the _owner address. For each request, the respective amount of stETH is transferred to this contract address, and an unstETH NFT is minted to the _owner address.

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| requestIds | uint256[] | Returns the array of ids for each created request |

### safeTransferFrom

```solidity
function safeTransferFrom(address _from, address _to, uint256 _requestId) external
```

_See {IERC721-safeTransferFrom}._

### claimWithdrawal

```solidity
function claimWithdrawal(uint256 _requestId) external
```

Claims the _requestId withdrawal request, sending ether to msg.sender address.

### getWithdrawalStatus

```solidity
function getWithdrawalStatus(uint256[] _requestIds) external view returns (struct ILidoWithdrawalQueueERC721.WithdrawalRequestStatus[] statuses)
```

## VaultFactory

Configure and deploy vaults

### vaultContract

```solidity
address vaultContract
```

Master vault contract to clone from

### nextVaultId

```solidity
uint256 nextVaultId
```

Incrementing vault ID

### protocolFeeBps

```solidity
uint256 protocolFeeBps
```

Protocol fee taken from earnings in basis points (one basis point = 1/100 of 1%)

### protocolFeeReceiver

```solidity
address protocolFeeReceiver
```

Address that collects protocol fees

### earlyExitFeeBps

```solidity
uint256 earlyExitFeeBps
```

Fixed income early exit fee in basis points (one basis point = 1/100 of 1%) that is quadratically scaled based off of early exit time

### VaultInfo

```solidity
struct VaultInfo {
  address creator;
  address addr;
}
```

### vaultInfo

```solidity
mapping(uint256 => struct VaultFactory.VaultInfo) vaultInfo
```

Info about vault, mapped by vault ID

### vaultAddrToId

```solidity
mapping(address => uint256) vaultAddrToId
```

ID of vault, mapped by vault address

### VaultCodeSet

```solidity
event VaultCodeSet(address creator)
```

Emitted when the vault bytecode is set

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| creator | address | Address of creator |

### VaultCreated

```solidity
event VaultCreated(uint256 vaultId, uint256 duration, uint256 fixedSideCapacity, uint256 variableSideCapacity, uint256 earlyExitFeeBps, uint256 protocolFeeBps, address protocolFeeReceiver, address creator, address vault)
```

Emitted when a new vault is deployed

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| vaultId | uint256 | ID of vault |
| duration | uint256 | How long the vault will be locked once started, in seconds |
| fixedSideCapacity | uint256 | Maximum capacity of fixed side |
| variableSideCapacity | uint256 | Maximum capacity of variable side |
| earlyExitFeeBps | uint256 | Fixed depositor early exit fee in basis points |
| protocolFeeBps | uint256 | Protocol fee in basis points |
| protocolFeeReceiver | address | Address that collects protocol fee |
| creator | address | Address of vault creator |
| vault | address | Address of vault |

### SetEarlyExitFeeBps

```solidity
event SetEarlyExitFeeBps(uint256 earlyExitFeeBps)
```

Emitted when the Factory owner changes earlyExitFeeBps

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| earlyExitFeeBps | uint256 | Fixed income early exit fee in basis points (one basis point = 1/100 of 1%) that is quadratically scaled based off of early exit time |

### SetProtocolFeeReceiver

```solidity
event SetProtocolFeeReceiver(address protocolFeeReceiver)
```

Emitted when the Factory owner changes protocolFeeReceiver

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| protocolFeeReceiver | address | Address that collects protocol fees |

### SetProtocolFeeBps

```solidity
event SetProtocolFeeBps(uint256 protocolFeeBps)
```

Emitted when the Factory owner changes protocolFeeBps

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| protocolFeeBps | uint256 | Protocol fee taken from earnings in basis points |

### constructor

```solidity
constructor(uint256 _protocolFeeBps, uint256 _earlyExitFeeBps) public
```

### setProtocolFeeBps

```solidity
function setProtocolFeeBps(uint256 _protocolFeeBps) external
```

### setProtocolFeeReceiver

```solidity
function setProtocolFeeReceiver(address _protocolFeeReceiver) external
```

### setEarlyExitFeeBps

```solidity
function setEarlyExitFeeBps(uint256 _earlyExitFeeBps) external
```

### createVault

```solidity
function createVault(uint256 _fixedSideCapacity, uint256 _duration, uint256 _variableSideCapacity) public virtual
```

Deploys a new vault

### wasDeployedByFactory

```solidity
function wasDeployedByFactory(address addr) external view returns (bool)
```

Check to see if a given vault was deployed by this factory

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | bool | True if address matches a vault deployed by this factory |

