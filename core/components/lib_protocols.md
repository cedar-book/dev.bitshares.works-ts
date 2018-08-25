#### BitShares Core - graphene::chain
https://bitshares.org/doxygen/dir_88bb0b7a0369deae7dcd36c79a63cea0.html

# Protocols and Detailed Descriptions
*graphene::chain::*

*..\libraries\chain\include\graphene\chain\protocol*


- account 
- address 
- assert 
- asset 
- asset_ops 
- authority 
- balance 
- base 
- block 
- buyback 
- chain_parameters 
- committee_member 
- confidential 
- config 
- custom 
- ext 
- fba 
- fee_schedule 
- market 
- memo 
- operations 
- proposal 
- protocol 
- special_authority 
- transaction 
- transfer 
- types 
- vesting 
- vote 
- withdraw_permission 
- witness 
- worker 

***

- account 


- address 

namespace fc { namespace ecc {
	class public_key;
	typedef fc::array<char,33>  public_key_data;
} } // fc::ecc

namespace graphene { namespace chain {

struct public_key_type;

- A 160 bit hash of a public key
- An address can be converted to or from a base58 string with 32 bit checksum.
- An address is calculated as ripemd160( sha512( compressed_ecc_public_key ) )
- When converted to a string, checksum calculated as the first 4 bytes ripemd160( address ) is appended to the binary address before converting to base58.

class address
{
};

};

- assert 

struct account_name_eq_lit_predicate{  };
struct asset_symbol_eq_lit_predicate{  };
struct block_id_predicate{  };

   typedef static_variant<
      account_name_eq_lit_predicate,
      asset_symbol_eq_lit_predicate,
      block_id_predicate
     > predicate;

struct assert_operation : public base_operation{  };


- asset 

extern const int64_t scaled_precision_lut[];
struct price;
struct asset{  };
struct price{  };
struct price_feed{  };




   
   
- asset_ops 

bool is_valid_symbol( const string& symbol );
struct asset_options {  };
struct bitasset_options {  };
struct asset_create_operation : public base_operation {  };
struct asset_global_settle_operation : public base_operation{   };
struct asset_settle_operation : public base_operation{   };
struct asset_settle_cancel_operation : public base_operation{   };
struct asset_fund_fee_pool_operation : public base_operation{  };
struct asset_update_operation : public base_operation{  };
struct asset_update_bitasset_operation : public base_operation{  };
struct asset_update_feed_producers_operation : public base_operation{  };
struct asset_publish_feed_operation : public base_operation{  };
struct asset_issue_operation : public base_operation{  };
struct asset_reserve_operation : public base_operation{  };
struct asset_claim_fees_operation : public base_operation{  };
struct asset_update_issuer_operation : public base_operation{  };
struct asset_claim_pool_operation : public base_operation{  };



### authority 

struct authority{  };
void add_authority_accounts(
   flat_set<account_id_type>& result,
   const authority& a
   );



### balance 

struct balance_claim_operation : public base_operation{  };


### base 
struct void_result{};
typedef fc::static_variant<void_result,object_id_type,asset> operation_result;

struct base_operation{  };

typedef static_variant<void_t>      future_extensions;

typedef flat_set<future_extensions> extensions_type;


### block 
struct block_header{  };
struct signed_block_header : public block_header{  }
struct signed_block : public signed_block_header{  };



### buyback 

struct buyback_account_options
{
   /**
    * The asset to buy.
    */
   asset_id_type       asset_to_buy;

   /**
    * Issuer of the asset.  Must sign the transaction, must match issuer
    * of specified asset.
    */
   account_id_type     asset_to_buy_issuer;

   /**
    * What assets the account is willing to buy with.
    * Other assets will just sit there since the account has null authority.
    */
   flat_set< asset_id_type > markets;
};


### chain_parameters 

   typedef static_variant<>  parameter_extension; 
   struct chain_parameters
   {
      /** using a smart ref breaks the circular dependency created between operations and the fee schedule */
      smart_ref<fee_schedule> current_fees;                       ///< current schedule of fees
      uint8_t                 block_interval                      = GRAPHENE_DEFAULT_BLOCK_INTERVAL; ///< interval in seconds between blocks
      uint32_t                maintenance_interval                = GRAPHENE_DEFAULT_MAINTENANCE_INTERVAL; ///< interval in sections between blockchain maintenance events
      uint8_t                 maintenance_skip_slots              = GRAPHENE_DEFAULT_MAINTENANCE_SKIP_SLOTS; ///< number of block_intervals to skip at maintenance time
      uint32_t                committee_proposal_review_period    = GRAPHENE_DEFAULT_COMMITTEE_PROPOSAL_REVIEW_PERIOD_SEC; ///< minimum time in seconds that a proposed transaction requiring committee authority may not be signed, prior to expiration
      uint32_t                maximum_transaction_size            = GRAPHENE_DEFAULT_MAX_TRANSACTION_SIZE; ///< maximum allowable size in bytes for a transaction
      uint32_t                maximum_block_size                  = GRAPHENE_DEFAULT_MAX_BLOCK_SIZE; ///< maximum allowable size in bytes for a block
      uint32_t                maximum_time_until_expiration       = GRAPHENE_DEFAULT_MAX_TIME_UNTIL_EXPIRATION; ///< maximum lifetime in seconds for transactions to be valid, before expiring
      uint32_t                maximum_proposal_lifetime           = GRAPHENE_DEFAULT_MAX_PROPOSAL_LIFETIME_SEC; ///< maximum lifetime in seconds for proposed transactions to be kept, before expiring
      uint8_t                 maximum_asset_whitelist_authorities = GRAPHENE_DEFAULT_MAX_ASSET_WHITELIST_AUTHORITIES; ///< maximum number of accounts which an asset may list as authorities for its whitelist OR blacklist
      uint8_t                 maximum_asset_feed_publishers       = GRAPHENE_DEFAULT_MAX_ASSET_FEED_PUBLISHERS; ///< the maximum number of feed publishers for a given asset
      uint16_t                maximum_witness_count               = GRAPHENE_DEFAULT_MAX_WITNESSES; ///< maximum number of active witnesses
      uint16_t                maximum_committee_count             = GRAPHENE_DEFAULT_MAX_COMMITTEE; ///< maximum number of active committee_members
      uint16_t                maximum_authority_membership        = GRAPHENE_DEFAULT_MAX_AUTHORITY_MEMBERSHIP; ///< largest number of keys/accounts an authority can have
      uint16_t                reserve_percent_of_fee              = GRAPHENE_DEFAULT_BURN_PERCENT_OF_FEE; ///< the percentage of the network's allocation of a fee that is taken out of circulation
      uint16_t                network_percent_of_fee              = GRAPHENE_DEFAULT_NETWORK_PERCENT_OF_FEE; ///< percent of transaction fees paid to network
      uint16_t                lifetime_referrer_percent_of_fee    = GRAPHENE_DEFAULT_LIFETIME_REFERRER_PERCENT_OF_FEE; ///< percent of transaction fees paid to network
      uint32_t                cashback_vesting_period_seconds     = GRAPHENE_DEFAULT_CASHBACK_VESTING_PERIOD_SEC; ///< time after cashback rewards are accrued before they become liquid
      share_type              cashback_vesting_threshold          = GRAPHENE_DEFAULT_CASHBACK_VESTING_THRESHOLD; ///< the maximum cashback that can be received without vesting
      bool                    count_non_member_votes              = true; ///< set to false to restrict voting privlegages to member accounts
      bool                    allow_non_member_whitelists         = false; ///< true if non-member accounts may set whitelists and blacklists; false otherwise
      share_type              witness_pay_per_block               = GRAPHENE_DEFAULT_WITNESS_PAY_PER_BLOCK; ///< CORE to be allocated to witnesses (per block)
      uint32_t                witness_pay_vesting_seconds         = GRAPHENE_DEFAULT_WITNESS_PAY_VESTING_SECONDS; ///< vesting_seconds parameter for witness VBO's
      share_type              worker_budget_per_day               = GRAPHENE_DEFAULT_WORKER_BUDGET_PER_DAY; ///< CORE to be allocated to workers (per day)
      uint16_t                max_predicate_opcode                = GRAPHENE_DEFAULT_MAX_ASSERT_OPCODE; ///< predicate_opcode must be less than this number
      share_type              fee_liquidation_threshold           = GRAPHENE_DEFAULT_FEE_LIQUIDATION_THRESHOLD; ///< value in CORE at which accumulated fees in blockchain-issued market assets should be liquidated
      uint16_t                accounts_per_fee_scale              = GRAPHENE_DEFAULT_ACCOUNTS_PER_FEE_SCALE; ///< number of accounts between fee scalings
      uint8_t                 account_fee_scale_bitshifts         = GRAPHENE_DEFAULT_ACCOUNT_FEE_SCALE_BITSHIFTS; ///< number of times to left bitshift account registration fee at each scaling
      uint8_t                 max_authority_depth                 = GRAPHENE_MAX_SIG_CHECK_DEPTH;
      extensions_type         extensions;

      /** defined in fee_schedule.cpp */
      void validate()const;
   };


- committee_member 
struct committee_member_create_operation : public base_operation{  };
struct committee_member_update_operation : public base_operation{  };
struct committee_member_update_global_parameters_operation : public base_operation{  };


### confidential 

using fc::ecc::blind_factor_type;

/**
 * @defgroup stealth Stealth Transfer
 * @brief Operations related to stealth transfer of value
 *
 * Stealth Transfers enable users to maintain their finanical privacy against even
 * though all transactions are public.  Every account has three balances:
 *
 * 1. Public Balance - everyone can see the balance changes and the parties involved
 * 2. Blinded Balance - everyone can see who is transacting but not the amounts involved
 * 3. Stealth Balance - both the amounts and parties involved are obscured
 *
 * Account owners may set a flag that allows their account to receive(or not) transfers of these kinds
 * Asset issuers can enable or disable the use of each of these types of accounts.
 *
 * Using the "temp account" which has no permissions required, users can transfer a
 * stealth balance to the temp account and then use the temp account to register a new
 * account.  In this way users can use stealth funds to create anonymous accounts with which
 * they can perform other actions that are not compatible with blinded balances (such as market orders)
 *
 * @section referral_program Referral Progam
 *
 * Stealth transfers that do not specify any account id cannot pay referral fees so 100% of the
 * transaction fee is paid to the network.
 *
 * @section transaction_fees Fees
 *
 * Stealth transfers can have an arbitrarylly large size and therefore the transaction fee for
 * stealth transfers is based purley on the data size of the transaction.
 */
///@{

/**
 *  @ingroup stealth
 *  This data is encrypted and stored in the
 *  encrypted memo portion of the blind output.
 */
struct blind_memo
{
   account_id_type     from;
   share_type          amount;
   string              message;
   /** set to the first 4 bytes of the shared secret
    * used to encrypt the memo.  Used to verify that
    * decryption was successful.
    */
   uint32_t            check= 0;
};

struct blind_input{  };

struct stealth_confirmation{  };

struct blind_output{  };

struct transfer_to_blind_operation : public base_operation{  };
struct transfer_from_blind_operation : public base_operation{  };
struct blind_transfer_operation : public base_operation{  }:



### config 


### custom 

struct custom_operation : public base_operation{  };



### ext 

amespace graphene { namespace chain {

using fc::unsigned_int;

template< typename T >
struct extension
{
   extension() {}

   T value;
};

template< typename T >
struct graphene_extension_pack_count_visitor{  };

template< typename Stream, typename T >
struct graphene_extension_pack_read_visitor{  };

template< typename Stream, typename T >
struct graphene_extension_unpack_visitor{  };
}};


namespace fc {

template< typename T >
struct graphene_extension_from_variant_visitor
{


};

template< typename T >
void from_variant( const fc::variant& var, graphene::chain::extension<T>& value, uint32_t max_depth ){  };

template< typename T >
struct graphene_extension_to_variant_visitor{  };

template< typename T >
void to_variant( const graphene::chain::extension<T>& value, fc::variant& var, uint32_t max_depth ){  };

namespace raw {

template< typename Stream, typename T >
void pack( Stream& stream, const graphene::chain::extension<T>& value, uint32_t _max_depth=FC_PACK_MAX_DEPTH )
{
   FC_ASSERT( _max_depth > 0 );
   --_max_depth;
   graphene::chain::graphene_extension_pack_count_visitor<T> count_vtor( value.value );
   fc::reflector<T>::visit( count_vtor );
   fc::raw::pack( stream, unsigned_int( count_vtor.count ), _max_depth );
   graphene::chain::graphene_extension_pack_read_visitor<Stream,T> read_vtor( stream, value.value, _max_depth );
   fc::reflector<T>::visit( read_vtor );
}


template< typename Stream, typename T >
void unpack( Stream& s, graphene::chain::extension<T>& value, uint32_t _max_depth=FC_PACK_MAX_DEPTH )
{
   FC_ASSERT( _max_depth > 0 );
   --_max_depth;
   value = graphene::chain::extension<T>();
   graphene::chain::graphene_extension_unpack_visitor<Stream, T> vtor( s, value.value, _max_depth );
   fc::reflector<T>::visit( vtor );
   FC_ASSERT( vtor.count_left == 0 ); // unrecognized extension throws here
}

} // fc::raw
};


### fba 
struct fba_distribute_operation : public base_operation{  };


### fee_schedule 

..\libraries\chain\include\graphene\chain\protocol\fee_schedule.hpp

template<typename T> struct transform_to_fee_parameters;
template<typename ...T>
template<typename Operation>
typedef transform_to_fee_parameters<operation>::type fee_parameters;

struct transform_to_fee_parameters<fc::static_variant<T...>>

class fee_helper 
class fee_helper<account_create_operation> 
class fee_helper<bid_collateral_operation> {
class fee_helper<asset_update_issuer_operation>
class fee_helper<asset_claim_pool_operation> 
 
*contains all of the parameters necessary to calculate the fee for any operation*

struct fee_schedule
{
	fee_schedule();

	static fee_schedule get_default();

	/**
	*  Finds the appropriate fee parameter struct for the operation
	*  and then calculates the appropriate fee.
	*/
	asset calculate_fee( const operation& op, const price& core_exchange_rate = price::unit_price() )const;
	asset set_fee( operation& op, const price& core_exchange_rate = price::unit_price() )const;

	void zero_all_fees();

	/**
	*  Validates all of the parameters are present and accounted for.
	*/
	void validate()const;

	template<typename Operation>
	const typename Operation::fee_parameters_type& get()const
	{
	 return fee_helper<Operation>().cget(parameters);
	}
	template<typename Operation>
	typename Operation::fee_parameters_type& get()
	{
	 return fee_helper<Operation>().get(parameters);
	}

	/**
	*  @note must be sorted by fee_parameters.which() and have no duplicates
	*/
	flat_set<fee_parameters> parameters;
	uint32_t                 scale = GRAPHENE_100_PERCENT; ///< fee * scale / GRAPHENE_100_PERCENT
};

typedef fee_schedule fee_schedule_type;

  


### market 

**struct**
limit_order_create_operation
limit_order_cancel_operation
call_order_update_operation
fill_order_operation
bid_collateral_operation
execute_bid_operation



### memo 

- defines the keys used to derive the shared secret

- Because account authorities and keys can change at any time, each memo must capture the specific keys used to derive the shared secret.  In order to read the cipher message you will need one of the two private keys.

*  If @ref from == @ref to and @ref from == 0 then no encryption is used, the memo is public.
*  If @ref from == @ref to and @ref from != 0 then invalid memo data

**struct**

   struct memo_data
   {
      public_key_type from;
      public_key_type to;
      /**
       * 64 bit nonce format:
       * [  8 bits | 56 bits   ]
       * [ entropy | timestamp ]
       * Timestamp is number of microseconds since the epoch
       * Entropy is a byte taken from the hash of a new private key
       *
       * This format is not mandated or verified; it is chosen to ensure uniqueness of key-IV pairs only. This should
       * be unique with high probability as long as the generating host has a high-resolution clock OR a strong source
       * of entropy for generating private keys.
       */
      uint64_t nonce = 0;
      /**
       * This field contains the AES encrypted packed @ref memo_message
       */
      vector<char> message;

      /// @note custom_nonce is for debugging only; do not set to a nonzero value in production
      void        set_message(const fc::ecc::private_key& priv,
                              const fc::ecc::public_key& pub, const string& msg, uint64_t custom_nonce = 0);

      std::string get_message(const fc::ecc::private_key& priv,
                              const fc::ecc::public_key& pub)const;
   }
   
- defines a message and checksum to enable validation of successful decryption
- When encrypting/decrypting a checksum is required to determine whether or not decryption was successful.
 
   
   struct memo_message
   {
      memo_message(){}
      memo_message( uint32_t checksum, const std::string& text )
      :checksum(checksum),text(text){}

      uint32_t    checksum = 0;
      std::string text;

      string serialize() const;
      static memo_message deserialize(const string& serial);
   };


### operations 

-  Defines the set of valid operations as a discriminated union type.

  typedef fc::static_variant<
            transfer_operation,
            limit_order_create_operation,
            limit_order_cancel_operation,
            call_order_update_operation,
            fill_order_operation,           // VIRTUAL
            account_create_operation,
            account_update_operation,
            account_whitelist_operation,
            account_upgrade_operation,
            account_transfer_operation,
            asset_create_operation,
            asset_update_operation,
            asset_update_bitasset_operation,
            asset_update_feed_producers_operation,
            asset_issue_operation,
            asset_reserve_operation,
            asset_fund_fee_pool_operation,
            asset_settle_operation,
            asset_global_settle_operation,
            asset_publish_feed_operation,
            witness_create_operation,
            witness_update_operation,
            proposal_create_operation,
            proposal_update_operation,
            proposal_delete_operation,
            withdraw_permission_create_operation,
            withdraw_permission_update_operation,
            withdraw_permission_claim_operation,
            withdraw_permission_delete_operation,
            committee_member_create_operation,
            committee_member_update_operation,
            committee_member_update_global_parameters_operation,
            vesting_balance_create_operation,
            vesting_balance_withdraw_operation,
            worker_create_operation,
            custom_operation,
            assert_operation,
            balance_claim_operation,
            override_transfer_operation,
            transfer_to_blind_operation,
            blind_transfer_operation,
            transfer_from_blind_operation,
            asset_settle_cancel_operation,  // VIRTUAL
            asset_claim_fees_operation,
            fba_distribute_operation,       // VIRTUAL
            bid_collateral_operation,
            execute_bid_operation,          // VIRTUAL
            asset_claim_pool_operation,
            asset_update_issuer_operation
         > operation;


- Appends required authorities to the result vector.  The authorities appended are not the same as those returned by get_required_auth 
- Return a set of required authorities for @ref op.		 
		 
   void operation_get_required_authorities( const operation& op, 
                                            flat_set<account_id_type>& active,
                                            flat_set<account_id_type>& owner,
                                            vector<authority>&  other );

   void operation_validate( const operation& op );


- necessary to support nested operations inside the proposal_create_operation

	struct op_wrapper
	{
	  public:
		 op_wrapper(const operation& op = operation()):op(op){}
		 operation op;
	};


### proposal 

- proposed_transactions  The Graphene Transaction Proposal Protocol
- Graphene allows users to propose a transaction which requires approval of multiple accounts in order to execute.

- The user proposes a transaction using proposal_create_operation, then signatory accounts use proposal_update_operations to add or remove their approvals from this operation. When a sufficient number of approvals have been granted, the operations in the proposal are used to create a virtual transaction which is subsequently evaluated. Even if the transaction fails, the proposal will be kept until the expiration time, at which point, if sufficient approval is granted, the transaction will be evaluated a final time. This allows transactions which will not execute successfully until a given time to still be executed through the proposal mechanism. The first time the proposed transaction succeeds, the proposal will be regarded as resolved, and all future updates will be invalid.
-  The proposal system allows for arbitrarily complex or recursively nested authorities. If a recursive authority (i.e. an authority which requires approval of 'nested' authorities on other accounts) is required for a proposal, then a second proposal can be used to grant the nested authority's approval. That is, a second proposal can be created which, when sufficiently approved, adds the approval of a nested authority to the first proposal. This multiple-proposal scheme can be used to acquire approval for an arbitrarily deep authority tree. 
- **Note** that at any time, a proposal can be approved in a single transaction if sufficient signatures are available on the proposal_update_operation, as long as the authority tree to approve the proposal does not exceed the maximum recursion depth. In practice, however, it is easier to use proposals to acquire all approvals, as this leverages on-chain notification of all relevant parties that their approval is required. Off-chain multi-signature approval requires some off-chain mechanism for acquiring several signatures on a single transaction. This off-chain synchronization can be avoided using proposals.
  
  
* op_wrapper is used to get around the circular definition of operation and proposals that contain them.

struct op_wrapper;

- The proposal_create_operation creates a transaction proposal, for use in multi-sig scenarios
- Creates a transaction proposal. The operations which compose the transaction are listed in order in proposed_ops, and expiration_time specifies the time by which the proposal must be accepted or it will fail permanently. The expiration_time cannot be farther in the future than the maximum expiration time set in the global properties object.
	 
struct proposal_create_operation : public base_operation
struct proposal_update_operation : public base_operation
struct proposal_delete_operation : public base_operation
      
   
### protocol 


### special_authority 

struct no_special_authority {};

struct top_holders_special_authority
{
   asset_id_type asset;
   uint8_t       num_top_holders = 1;
};

typedef static_variant<
   no_special_authority,
   top_holders_special_authority
   > special_authority;

void validate_special_authority( const special_authority& auth );



### transaction 

- All transactions are sets of operations that must be applied atomically. Transactions must refer to a recent block that defines the context of the operation so that they assert a known binding to the object id's referenced in the transaction.
- Rather than specify a full block number, we only specify the lower 16 bits of the block number which means you can reference any block within the last 65,536 blocks which is 3.5 days with a 5 second block interval or 18 hours with a 1 second interval.
- All transactions must expire so that the network does not have to maintain a permanent record of all transactions ever published.  A transaction may not have an expiration date too far in the future because this would require keeping too much transaction history in memory.
-  The block prefix is the first 4 bytes of the block hash of the reference block number, which is the second 4 bytes of the @ref block_id_type (the first 4 bytes of the block ID are the block number)
- **Note**: A transaction which selects a reference block cannot be migrated between forks outside the period of ref_block_num.time to (ref_block_num.time + rel_exp * interval). This fact can be used to protect market orders which should specify a relatively short re-org window of perhaps less than 1 minute. Normal payments should probably have a longer re-org window to ensure their transaction can still go through in the event of a momentary disruption in service.
- **Note**: It is not recommended to set the @ref ref_block_num, @ref ref_block_prefix, and @ref expiration fields manually. Call the appropriate overload of @ref set_expiration instead.
   

**groups operations that should be applied atomically**

struct transaction
{
  /**
   * Least significant 16 bits from the reference block number. If @ref relative_expiration is zero, this field
   * must be zero as well.
   */
  uint16_t           ref_block_num    = 0;
  /**
   * The first non-block-number 32-bits of the reference block ID. Recall that block IDs have 32 bits of block
   * number followed by the actual block hash, so this field should be set using the second 32 bits in the
   * @ref block_id_type
   */
  uint32_t           ref_block_prefix = 0;

  /**
   * This field specifies the absolute expiration for this transaction.
   */
  fc::time_point_sec expiration;

  vector<operation>  operations;
  extensions_type    extensions;

  /// Calculate the digest for a transaction
  digest_type         digest()const;
  transaction_id_type id()const;
  void                validate() const;
  /// Calculate the digest used for signature validation
  digest_type         sig_digest( const chain_id_type& chain_id )const;

  void set_expiration( fc::time_point_sec expiration_time );
  void set_reference_block( const block_id_type& reference_block );

  /// visit all operations
  template<typename Visitor>
  vector<typename Visitor::result_type> visit( Visitor&& visitor )
  {
	 vector<typename Visitor::result_type> results;
	 for( auto& op : operations )
		results.push_back(op.visit( std::forward<Visitor>( visitor ) ));
	 return results;
  }
  template<typename Visitor>
  vector<typename Visitor::result_type> visit( Visitor&& visitor )const
  {
	 vector<typename Visitor::result_type> results;
	 for( auto& op : operations )
		results.push_back(op.visit( std::forward<Visitor>( visitor ) ));
	 return results;
  }

  void get_required_authorities( flat_set<account_id_type>& active, flat_set<account_id_type>& owner, vector<authority>& other )const;
};


**adds a signature to a transaction**

struct signed_transaction : public transaction
{
  signed_transaction( const transaction& trx = transaction() )
	 : transaction(trx){}

  /** signs and appends to signatures */
  const signature_type& sign( const private_key_type& key, const chain_id_type& chain_id );

  /** returns signature but does not append */
  signature_type sign( const private_key_type& key, const chain_id_type& chain_id )const;

  /**
   *  The purpose of this method is to identify some subset of
   *  @ref available_keys that will produce sufficient signatures
   *  for a transaction.  The result is not always a minimal set of
   *  signatures, but any non-minimal result will still pass
   *  validation.
   */
  set<public_key_type> get_required_signatures(
	 const chain_id_type& chain_id,
	 const flat_set<public_key_type>& available_keys,
	 const std::function<const authority*(account_id_type)>& get_active,
	 const std::function<const authority*(account_id_type)>& get_owner,
	 uint32_t max_recursion = GRAPHENE_MAX_SIG_CHECK_DEPTH
	 )const;

  void verify_authority(
	 const chain_id_type& chain_id,
	 const std::function<const authority*(account_id_type)>& get_active,
	 const std::function<const authority*(account_id_type)>& get_owner,
	 uint32_t max_recursion = GRAPHENE_MAX_SIG_CHECK_DEPTH )const;

  /**
   * This is a slower replacement for get_required_signatures()
   * which returns a minimal set in all cases, including
   * some cases where get_required_signatures() returns a
   * non-minimal set.
   */

  set<public_key_type> minimize_required_signatures(
	 const chain_id_type& chain_id,
	 const flat_set<public_key_type>& available_keys,
	 const std::function<const authority*(account_id_type)>& get_active,
	 const std::function<const authority*(account_id_type)>& get_owner,
	 uint32_t max_recursion = GRAPHENE_MAX_SIG_CHECK_DEPTH
	 ) const;

  flat_set<public_key_type> get_signature_keys( const chain_id_type& chain_id )const;

  vector<signature_type> signatures;

  /// Removes all operations and signatures
  void clear() { operations.clear(); signatures.clear(); }
};

void verify_authority( const vector<operation>& ops, const flat_set<public_key_type>& sigs,
					  const std::function<const authority*(account_id_type)>& get_active,
					  const std::function<const authority*(account_id_type)>& get_owner,
					  uint32_t max_recursion = GRAPHENE_MAX_SIG_CHECK_DEPTH,
					  bool allow_committe = false,
					  const flat_set<account_id_type>& active_aprovals = flat_set<account_id_type>(),
					  const flat_set<account_id_type>& owner_approvals = flat_set<account_id_type>());

- captures the result of evaluating the operations contained in the transaction
- When processing a transaction some operations generate new object IDs and these IDs cannot be known until the transaction is actually included into a block.  When a block is produced these new ids are captured and included with every transaction.  The index in operation_results should correspond to the same index in operations.
- If an operation did not create any new object IDs then 0 should be returned.

struct processed_transaction : public signed_transaction
{
  processed_transaction( const signed_transaction& trx = signed_transaction() )
	 : signed_transaction(trx){}

  vector<operation_result> operation_results;

  digest_type merkle_digest()const;
};

### transfer 

- operations

struct transfer_operation : public base_operation
struct override_transfer_operation : public base_operation  


### types 

using namespace graphene::db;

using                               std::map;
using                               std::vector;
using                               std::unordered_map;
using                               std::string;
using                               std::deque;
using                               std::shared_ptr;
using                               std::weak_ptr;
using                               std::unique_ptr;
using                               std::set;
using                               std::pair;
using                               std::enable_shared_from_this;
using                               std::tie;
using                               std::make_pair;

using                               fc::smart_ref;
using                               fc::variant_object;
using                               fc::variant;
using                               fc::enum_type;
using                               fc::optional;
using                               fc::unsigned_int;
using                               fc::signed_int;
using                               fc::time_point_sec;
using                               fc::time_point;
using                               fc::safe;
using                               fc::flat_map;
using                               fc::flat_set;
using                               fc::static_variant;
using                               fc::ecc::range_proof_type;
using                               fc::ecc::range_proof_info;
using                               fc::ecc::commitment_type;
struct void_t{};

typedef fc::ecc::private_key        private_key_type;
typedef fc::sha256 chain_id_type;

typedef boost::rational< int32_t >   ratio_type;

enum asset_issuer_permission_flags
{
  charge_market_fee    = 0x01, /**< an issuer-specified percentage of all market trades in this asset is paid to the issuer */
  white_list           = 0x02, /**< accounts must be whitelisted in order to hold this asset */
  override_authority   = 0x04, /**< issuer may transfer asset back to himself */
  transfer_restricted  = 0x08, /**< require the issuer to be one party to every transfer */
  disable_force_settle = 0x10, /**< disable force settling */
  global_settle        = 0x20, /**< allow the bitasset issuer to force a global settling -- this may be set in permissions, but not flags */
  disable_confidential = 0x40, /**< allow the asset to be used with confidential transactions */
  witness_fed_asset    = 0x80, /**< allow the asset to be fed by witnesses */
  committee_fed_asset  = 0x100 /**< allow the asset to be fed by the committee */
};
const static uint32_t ASSET_ISSUER_PERMISSION_MASK = charge_market_fee|white_list|override_authority|transfer_restricted|disable_force_settle|global_settle|disable_confidential
  |witness_fed_asset|committee_fed_asset;
const static uint32_t UIA_ASSET_ISSUER_PERMISSION_MASK = charge_market_fee|white_list|override_authority|transfer_restricted|disable_confidential;

enum reserved_spaces
{
  relative_protocol_ids = 0,
  protocol_ids          = 1,
  implementation_ids    = 2
};

inline bool is_relative( object_id_type o ){ return o.space() == 0; }

- List all object types from all namespaces here so they can be easily reflected and displayed in debug output.  If a 3rd party  wants to extend the core code then they will have to change the packed_object::type field from enum_type to uint16 to avoid warnings when converting packed_objects to/from json.

enum object_type
{
  null_object_type,
  base_object_type,
  account_object_type,
  asset_object_type,
  force_settlement_object_type,
  committee_member_object_type,
  witness_object_type,
  limit_order_object_type,
  call_order_object_type,
  custom_object_type,
  proposal_object_type,
  operation_history_object_type,
  withdraw_permission_object_type,
  vesting_balance_object_type,
  worker_object_type,
  balance_object_type,
  OBJECT_TYPE_COUNT ///< Sentry value which contains the number of different object types
};

enum impl_object_type
{
  impl_global_property_object_type,
  impl_dynamic_global_property_object_type,
  impl_reserved0_object_type,      // formerly index_meta_object_type, TODO: delete me
  impl_asset_dynamic_data_type,
  impl_asset_bitasset_data_type,
  impl_account_balance_object_type,
  impl_account_statistics_object_type,
  impl_transaction_object_type,
  impl_block_summary_object_type,
  impl_account_transaction_history_object_type,
  impl_blinded_balance_object_type,
  impl_chain_property_object_type,
  impl_witness_schedule_object_type,
  impl_budget_record_object_type,
  impl_special_authority_object_type,
  impl_buyback_object_type,
  impl_fba_accumulator_object_type,
  impl_collateral_bid_object_type
};


class account_object;
class committee_member_object;
class witness_object;
class asset_object;
class force_settlement_object;
class limit_order_object;
class call_order_object;
class custom_object;
class proposal_object;
class operation_history_object;
class withdraw_permission_object;
class vesting_balance_object;
class worker_object;
class balance_object;
class blinded_balance_object;


typedef object_id< protocol_ids, account_object_type,            account_object>               account_id_type;
typedef object_id< protocol_ids, asset_object_type,              asset_object>                 asset_id_type;
typedef object_id< protocol_ids, force_settlement_object_type,   force_settlement_object>      force_settlement_id_type;
typedef object_id< protocol_ids, committee_member_object_type,   committee_member_object>      committee_member_id_type;
typedef object_id< protocol_ids, witness_object_type,            witness_object>               witness_id_type;
typedef object_id< protocol_ids, limit_order_object_type,        limit_order_object>           limit_order_id_type;
typedef object_id< protocol_ids, call_order_object_type,         call_order_object>            call_order_id_type;
typedef object_id< protocol_ids, custom_object_type,             custom_object>                custom_id_type;
typedef object_id< protocol_ids, proposal_object_type,           proposal_object>              proposal_id_type;
typedef object_id< protocol_ids, operation_history_object_type,  operation_history_object>     operation_history_id_type;
typedef object_id< protocol_ids, withdraw_permission_object_type,withdraw_permission_object>   withdraw_permission_id_type;
typedef object_id< protocol_ids, vesting_balance_object_type,    vesting_balance_object>       vesting_balance_id_type;
typedef object_id< protocol_ids, worker_object_type,             worker_object>                worker_id_type;
typedef object_id< protocol_ids, balance_object_type,            balance_object>               balance_id_type;

// implementation types
class global_property_object;
class dynamic_global_property_object;
class asset_dynamic_data_object;
class asset_bitasset_data_object;
class account_balance_object;
class account_statistics_object;
class transaction_object;
class block_summary_object;
class account_transaction_history_object;
class chain_property_object;
class witness_schedule_object;
class budget_record_object;
class special_authority_object;
class buyback_object;
class fba_accumulator_object;
class collateral_bid_object;

typedef object_id< implementation_ids, impl_global_property_object_type,  global_property_object>                    global_property_id_type;
typedef object_id< implementation_ids, impl_dynamic_global_property_object_type,  dynamic_global_property_object>    dynamic_global_property_id_type;
typedef object_id< implementation_ids, impl_asset_dynamic_data_type,      asset_dynamic_data_object>                 asset_dynamic_data_id_type;
typedef object_id< implementation_ids, impl_asset_bitasset_data_type,     asset_bitasset_data_object>                asset_bitasset_data_id_type;
typedef object_id< implementation_ids, impl_account_balance_object_type,  account_balance_object>                    account_balance_id_type;
typedef object_id< implementation_ids, impl_account_statistics_object_type,account_statistics_object>                account_statistics_id_type;
typedef object_id< implementation_ids, impl_transaction_object_type,      transaction_object>                        transaction_obj_id_type;
typedef object_id< implementation_ids, impl_block_summary_object_type,    block_summary_object>                      block_summary_id_type;

typedef object_id< implementation_ids,
				  impl_account_transaction_history_object_type,
				  account_transaction_history_object>       account_transaction_history_id_type;
typedef object_id< implementation_ids, impl_chain_property_object_type,   chain_property_object>                     chain_property_id_type;
typedef object_id< implementation_ids, impl_witness_schedule_object_type, witness_schedule_object>                   witness_schedule_id_type;
typedef object_id< implementation_ids, impl_budget_record_object_type, budget_record_object >                        budget_record_id_type;
typedef object_id< implementation_ids, impl_blinded_balance_object_type, blinded_balance_object >                    blinded_balance_id_type;
typedef object_id< implementation_ids, impl_special_authority_object_type, special_authority_object >                special_authority_id_type;
typedef object_id< implementation_ids, impl_buyback_object_type, buyback_object >                                    buyback_id_type;
typedef object_id< implementation_ids, impl_fba_accumulator_object_type, fba_accumulator_object >                    fba_accumulator_id_type;
typedef object_id< implementation_ids, impl_collateral_bid_object_type, collateral_bid_object >                      collateral_bid_id_type;

typedef fc::array<char, GRAPHENE_MAX_ASSET_SYMBOL_LENGTH>    symbol_type;
typedef fc::ripemd160                                        block_id_type;
typedef fc::ripemd160                                        checksum_type;
typedef fc::ripemd160                                        transaction_id_type;
typedef fc::sha256                                           digest_type;
typedef fc::ecc::compact_signature                           signature_type;
typedef safe<int64_t>                                        share_type;
typedef uint16_t                                             weight_type;

struct public_key_type
{
   struct binary_key
   {
	  binary_key() {}
	  uint32_t                 check = 0;
	  fc::ecc::public_key_data data;
   };
   fc::ecc::public_key_data key_data;
   public_key_type();
   public_key_type( const fc::ecc::public_key_data& data );
   public_key_type( const fc::ecc::public_key& pubkey );
   explicit public_key_type( const std::string& base58str );
   operator fc::ecc::public_key_data() const;
   operator fc::ecc::public_key() const;
   explicit operator std::string() const;
   friend bool operator == ( const public_key_type& p1, const fc::ecc::public_key& p2);
   friend bool operator == ( const public_key_type& p1, const public_key_type& p2);
   friend bool operator != ( const public_key_type& p1, const public_key_type& p2);
};

struct extended_public_key_type
{
  struct binary_key
  {
	 binary_key() {}
	 uint32_t                   check = 0;
	 fc::ecc::extended_key_data data;
  };
  
  fc::ecc::extended_key_data key_data;
   
  extended_public_key_type();
  extended_public_key_type( const fc::ecc::extended_key_data& data );
  extended_public_key_type( const fc::ecc::extended_public_key& extpubkey );
  explicit extended_public_key_type( const std::string& base58str );
  operator fc::ecc::extended_public_key() const;
  explicit operator std::string() const;
  friend bool operator == ( const extended_public_key_type& p1, const fc::ecc::extended_public_key& p2);
  friend bool operator == ( const extended_public_key_type& p1, const extended_public_key_type& p2);
  friend bool operator != ( const extended_public_key_type& p1, const extended_public_key_type& p2);
};

struct extended_private_key_type
{
  struct binary_key
  {
	 binary_key() {}
	 uint32_t                   check = 0;
	 fc::ecc::extended_key_data data;
  };
  
  fc::ecc::extended_key_data key_data;
   
  extended_private_key_type();
  extended_private_key_type( const fc::ecc::extended_key_data& data );
  extended_private_key_type( const fc::ecc::extended_private_key& extprivkey );
  explicit extended_private_key_type( const std::string& base58str );
  operator fc::ecc::extended_private_key() const;
  explicit operator std::string() const;
  friend bool operator == ( const extended_private_key_type& p1, const fc::ecc::extended_private_key& p2);
  friend bool operator == ( const extended_private_key_type& p1, const extended_private_key_type& p2);
  friend bool operator != ( const extended_private_key_type& p1, const extended_private_key_type& p2);
};

namespace fc
{
    void to_variant( const graphene::chain::public_key_type& var,  fc::variant& vo, uint32_t max_depth = 2 );
    void from_variant( const fc::variant& var,  graphene::chain::public_key_type& vo, uint32_t max_depth = 2 );
    void to_variant( const graphene::chain::extended_public_key_type& var, fc::variant& vo, uint32_t max_depth = 2 );
    void from_variant( const fc::variant& var, graphene::chain::extended_public_key_type& vo, uint32_t max_depth = 2 );
    void to_variant( const graphene::chain::extended_private_key_type& var, fc::variant& vo, uint32_t max_depth = 2 );
    void from_variant( const fc::variant& var, graphene::chain::extended_private_key_type& vo, uint32_t max_depth = 2 );
}


### vesting 


struct linear_vesting_policy_initializer
{
  /** while vesting begins on begin_timestamp, none may be claimed before vesting_cliff_seconds have passed */
  fc::time_point_sec begin_timestamp;
  uint32_t           vesting_cliff_seconds = 0;
  uint32_t           vesting_duration_seconds = 0;
};

struct cdd_vesting_policy_initializer
{
  /** while coindays may accrue over time, none may be claimed before the start_claim time */
  fc::time_point_sec start_claim;
  uint32_t           vesting_seconds = 0;
  cdd_vesting_policy_initializer( uint32_t vest_sec = 0, fc::time_point_sec sc = fc::time_point_sec() ):start_claim(sc),vesting_seconds(vest_sec){}
};

typedef fc::static_variant<linear_vesting_policy_initializer, cdd_vesting_policy_initializer> vesting_policy_initializer;

struct vesting_balance_create_operation : public base_operation
struct vesting_balance_withdraw_operation : public base_operation



### vote 

- An ID for some votable object
- This class stores an ID for a votable object. The ID is comprised of two fields: a type, and an instance. The type field stores which kind of object is being voted on, and the instance stores which specific object of that type is being referenced by this ID.
- A value of vote_id_type is implicitly convertible to an unsigned 32-bit integer containing only the instance. It may also be implicitly assigned from a uint32_t, which will update the instance. It may not, however, be implicitly constructed from a uint32_t, as in this case, the type would be unknown.
- On the wire, a vote_id_type is represented as a 32-bit integer with the type in the lower 8 bits and the instance in the upper 24 bits. This means that types may never exceed 8 bits, and instances may never exceed 24 bits. 
- In JSON, a vote_id_type is represented as a string "type:instance", i.e. "1:5" would be type 1 and instance 5. 
- **Note**: In the Graphene protocol, vote_id_type instances are unique across types; that is to say, if an object of type 1 has instance 4, an object of type 0 may not also have instance 4. In other words, the type is not a namespace for instances; it is only an informational field.

struct vote_id_type
{
   /// Lower 8 bits are type; upper 24 bits are instance
   uint32_t content;

   friend size_t hash_value( vote_id_type v ) { return std::hash<uint32_t>()(v.content); }
   enum vote_type
   {
      committee,
      witness,
      worker,
      VOTE_TYPE_COUNT
   };

   /// Default constructor. Sets type and instance to 0
   vote_id_type():content(0){}
   /// Construct this vote_id_type with provided type and instance
   vote_id_type(vote_type type, uint32_t instance = 0)
      : content(instance<<8 | type)
   {}
   /// Construct this vote_id_type from a serial string in the form "type:instance"
   explicit vote_id_type(const std::string& serial)
   { try {
      auto colon = serial.find(':');
      FC_ASSERT( colon != std::string::npos );
      *this = vote_id_type(vote_type(std::stoul(serial.substr(0, colon))), std::stoul(serial.substr(colon+1)));
   } FC_CAPTURE_AND_RETHROW( (serial) ) }

   /// Set the type of this vote_id_type
   void set_type(vote_type type)
   {
      content &= 0xffffff00;
      content |= type & 0xff;
   }
   /// Get the type of this vote_id_type
   vote_type type()const
   {
      return vote_type(content & 0xff);
   }

   /// Set the instance of this vote_id_type
   void set_instance(uint32_t instance)
   {
      assert(instance < 0x01000000);
      content &= 0xff;
      content |= instance << 8;
   }
   /// Get the instance of this vote_id_type
   uint32_t instance()const
   {
      return content >> 8;
   }

   vote_id_type& operator =(vote_id_type other)
   {
      content = other.content;
      return *this;
   }
   /// Set the instance of this vote_id_type
   vote_id_type& operator =(uint32_t instance)
   {
      set_instance(instance);
      return *this;
   }
   /// Get the instance of this vote_id_type
   operator uint32_t()const
   {
      return instance();
   }

   /// Convert this vote_id_type to a serial string in the form "type:instance"
   explicit operator std::string()const
   {
      return std::to_string(type()) + ":" + std::to_string(instance());
   }
};

class global_property_object;

vote_id_type get_next_vote_id( global_property_object& gpo, vote_id_type::vote_type type );


namespace fc
{

class variant;

void to_variant( const graphene::chain::vote_id_type& var, fc::variant& vo, uint32_t max_depth = 1 );
void from_variant( const fc::variant& var, graphene::chain::vote_id_type& vo, uint32_t max_depth = 1 );

}


### withdraw_permission 

- Create a new withdrawal permission
- This operation creates a withdrawal permission, which allows some authorized account to withdraw from an authorizing account. This operation is primarily useful for scheduling recurring payments.
- Withdrawal permissions define withdrawal periods, which is a span of time during which the authorized account may make a withdrawal. Any number of withdrawals may be made so long as the total amount withdrawn per period does not exceed the limit for any given period.
- Withdrawal permissions authorize only a specific pairing, i.e. a permission only authorizes one specified authorized account to withdraw from one specified authorizing account. Withdrawals are limited and may not exceed he withdrawal limit. The withdrawal must be made in the same asset as the limit; attempts with withdraw any other asset type will be rejected.
- The fee for this operation is paid by withdraw_from_account, and this account is required to authorize this operation.

struct withdraw_permission_create_operation : public base_operation
struct withdraw_permission_update_operation : public base_operation
struct withdraw_permission_claim_operation : public base_operation
struct withdraw_permission_delete_operation : public base_operation

### witness 

- operations
- Create a witness object, as a bid to hold a witness position on the network.
- Accounts which wish to become witnesses may use this operation to create a witness object which stakeholders may vote on to approve its position as a witness.
	
struct witness_create_operation : public base_operation
struct witness_update_operation : public base_operation
	
	
### worker 

- operations
- workers The Blockchain Worker System
- Graphene blockchains allow the creation of special "workers" which are elected positions paid by the blockchain for services they provide. There may be several types of workers, and the semantics of how and when they are paid are defined by the @ref worker_type_enum enumeration. All workers are elected by core stakeholder approval, by voting for or against them.
- Workers are paid from the blockchain's daily budget if their total approval (votes for - votes against) is positive, ordered from most positive approval to least, until the budget is exhausted. Payments are processed at the blockchain maintenance interval. If a worker does not have positive approval during payment processing, or if the chain's budget is exhausted before the worker is paid, that worker is simply not paid at that interval.
- Payment is not prorated based on percentage of the interval the worker was approved. If the chain attempts to pay a worker, but the budget is insufficient to cover its entire pay, the worker is paid the remaining budget funds, even though this does not fulfill his total pay. The worker will not receive extra pay to make up the difference later. Worker pay is placed in a vesting balance and vests over the number of days specified at the worker's creation.
-  Once created, a worker is immutable and will be kept by the blockchain forever.


struct vesting_balance_worker_initializer
{
  vesting_balance_worker_initializer(uint16_t days=0):pay_vesting_period_days(days){}
  uint16_t pay_vesting_period_days = 0;
};

struct burn_worker_initializer
{};

struct refund_worker_initializer
{};


typedef static_variant< 
  refund_worker_initializer,
  vesting_balance_worker_initializer,
  burn_worker_initializer > worker_initializer;

struct worker_create_operation : public base_operation
{
  struct fee_parameters_type { uint64_t fee = 5000*GRAPHENE_BLOCKCHAIN_PRECISION; };

  asset                fee;
  account_id_type      owner;
  time_point_sec       work_begin_date;
  time_point_sec       work_end_date;
  share_type           daily_pay;
  string               name;
  string               url;
  /// This should be set to the initializer appropriate for the type of worker to be created.
  worker_initializer   initializer;

  account_id_type   fee_payer()const { return owner; }
  void              validate()const;
};


 
 
