## BitShares Core

This sectopn purpose: Lest Available Operations and Definitions.

### graphene::chain::base_operation


This section purpose: Lest Available Operations and Definitions.


- account_create_operation
- account_transfer_operation
- account_update_operation
- account_upgrade_operation
- account_whitelist_operation
- asset_operation
- asset_clain_fees_operation
- asset_claim_pool_operation
- zsset_create_operation
- asset_fund_fee_pool_operation
- asset_global_settle_operation
- asset_issue_operation
- asset_publish_feed_operation
- asset_reserve_operation
- asset_settle_cancel_operation
- asset_settle_operation
- asset_update_bitasset_operation
- asset_update_feed_producers_operation
- asset_update_issuer_operation
- asset_update_operation
- balance_claim_operation
- bit_collateral_operation
- blind_transfer_operation
- call_order_update_operation
- committee_member_create_operation
- committee_member_update_global_parameters_operation
- committee_member_update_operation
- custom_operation
- execute_bit_operation
- fba_distribute_operation
- fill_order_operation
- limit_order_cancel_operation
- limit_orders_create_operation
- override_transfer_operation
- proposal_create_operation
- proposal_delete_operation
- proposal_update_operation
- transfer_from_blind_operation
- transfer_operation
- transfer_to blind_operation
- vesting_balance_create_operation
- vesting_balance_withdraw_operation
- withdraw_permission_claim_operation
- withdraw_permission_create_operation
- withdraw_permission_delete_operation
- withdraw_permission_update_operation
- witness_create_operation
- witness_update_operation
- worker_create_operation


***

### Definitions


#### account_create_operation


#### account_transfer_operation
- Transfers the account to another account while clearing the white list. 
- In theory an account can be transferred by simply updating the authorities, but that kind of transfer lacks semantic meaning and is more often done to rotate keys without transferring ownership. This operation is used to indicate the legal transfer of title to this account and a break in the operation history. 
- The account_id's owner/active/voting/memo authority should be set to new_owner
- This operation is used to indicate the legal transfer of title to this account and a break in the operation history.
- This operation will clear the account's whitelist statuses, but not the blacklist statuses. 

#### account_update_operation
- Update an existing account.
- This operation is used to update an existing account. It can be used to update the authorities, or adjust the options on the account. See `account_object::options_type` for the options which may be updated. 

#### account_upgrade_operation
- Manage an account's membership status
- This operation is used to upgrade an account to a member, or renew its subscription. If an account which is an unexpired annual subscription member publishes this operation with `upgrade_to_lifetime_member` set to false, the account's membership expiration date will be pushed backward one year. If a basic account publishes it with `upgrade_to_lifetime_member` set to false, the account will be upgraded to a subscription member with an expiration date one year after the processing time of this operation.
- Any account may use this operation to become a lifetime member by setting `upgrade_to_lifetime_member` to true. Once an account has become a lifetime member, it may not use this operation anymore. 

#### account_whitelist_operation
- This operation is used to whitelist and blacklist accounts, primarily for transacting in whitelisted assets.
- Accounts can freely specify opinions about other accounts, in the form of either whitelisting or blacklisting them. This information is used in chain validation only to determine whether an account is authorized to transact in an asset type which enforces a whitelist, but third parties can use this information for other uses as well, as long as it does not conflict with the use of whitelisted assets.
- An asset which enforces a whitelist specifies a list of accounts to maintain its whitelist, and a list of accounts to maintain its blacklist. In order for a given account A to hold and transact in a whitelisted asset S, A must be whitelisted by at least one of S's whitelist_authorities and blacklisted by none of S's blacklist_authorities. If A receives a balance of S, and is later removed from the whitelist(s) which allowed it to hold S, or added to any blacklist S specifies as authoritative, A's balance of S will be frozen until A's authorization is reinstated.
- This operation requires authorizing_account's signature, but not account_to_list's. The fee is paid by authorizing_account

#### asset_operation
- assert that some conditions are true.
- This operation performs no changes to the database state, but can used to verify pre or post conditions for other operations. 

#### asset_claim_fees_operation
- used to transfer accumulated fees back to the issuer's balance. 

#### asset_claim_pool_operation
- Transfers BTS from the fee pool of a specified asset back to the issuer's balance. 

		Parameters
		
		- `fee`  Payment for the operation execution
		- `issuer`  Account which will be used for transfering BTS
		- `asset_id`  Id of the asset whose fee pool is going to be drained
		- `amount_to_claim`  Amount of BTS to claim from the fee pool
		- `extensions`  Field for future expansion

		Precondition
		
		- `fee` must be paid in the asset other than the one whose pool is being drained 
		- `amount_to_claim` should be specified in the core asset 
		- `amount_to_claim` should be nonnegative 

#### asset_create_operation
 
	  struct asset_create_operation : public base_operation
	  {
	  struct fee_parameters_type { 
	  uint64_t symbol3 = 500000 * GRAPHENE_BLOCKCHAIN_PRECISION;
	  uint64_t symbol4 = 300000 * GRAPHENE_BLOCKCHAIN_PRECISION;
	  uint64_t long_symbol = 5000 * GRAPHENE_BLOCKCHAIN_PRECISION;
	  uint32_t price_per_kbyte = 10; 
	  };
	  
#### asset_fund_fee_pool_operation

	  struct asset_fund_fee_pool_operation : public base_operation
	  {
	  struct fee_parameters_type { uint64_t fee = GRAPHENE_BLOCKCHAIN_PRECISION; };
	 
	  asset fee; 
	  account_id_type from_account;
	  asset_id_type asset_id;
	  share_type amount; 
	  extensions_type extensions;
	 
	  account_id_type fee_payer()const { return from_account; }
	  void validate()const;
	  };
  
#### asset_global_settle_operation
- Allows global settling of bitassets (black swan or prediction markets)
- In order to use this operation, `asset_to_settle` must have the global_settle flag set
- When this operation is executed all balances are converted into the backing asset at the settle_price and all open margin positions are called at the settle price. If this asset is used as backing for other bitassets, those bitassets will be force settled at their current feed price. 


#### asset_issue_operation

	  struct asset_issue_operation : public base_operation
	  {
	  struct fee_parameters_type { 
	  uint64_t fee = 20 * GRAPHENE_BLOCKCHAIN_PRECISION; 
	  uint32_t price_per_kbyte = GRAPHENE_BLOCKCHAIN_PRECISION;
	  };
	  
#### asset_publish_feed_operation


#### asset_reserve_operation


#### asset_settle_cancel_operation


#### asset_settle_operation


#### asset_update_bitasset_operation


#### asset_update_feed_producers_operation


#### asset_update_issuer_operation


#### asset_update_operation


#### balance_claim_operation


#### bit_collateral_operation


#### blind_transfer_operation


#### call_order_update_operation


#### committee_member_create_operation


#### committee_member_update_global_parameters_operation


#### committee_member_update_operation


#### custom_operation


#### execute_bit_operation


#### fba_distribute_operation


#### fill_order_operation


#### limit_order_cancel_operation


#### limit_orders_create_operation


#### override_transfer_operation


#### proposal_create_operation


#### proposal_delete_operation


#### proposal_update_operation


#### transfer_from_blind_operation


#### transfer_operation


#### transfer_to blind_operation


#### vesting_balance_create_operation


#### vesting_balance_withdraw_operation


#### withdraw_permission_claim_operation


#### withdraw_permission_create_operation


#### withdraw_permission_delete_operation


#### withdraw_permission_update_operation


#### witness_create_operation


#### witness_update_operation


#### worker_create_operation



***




