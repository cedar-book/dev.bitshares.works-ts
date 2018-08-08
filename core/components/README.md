## Components Structures and Detailed Description

### Block
- [A Block Elements and Structure(PDF)](../knowledge_base/shared_files/structures/BitShares-Block-Structurev1.pdf)
- [Block Header - inheritance](README.md#block-header)


### Evaluators
- graphene::chain::account_create_evaluator 


### Operations 
- [graphene::chain::base_operation](../components/operations.md#bitshares-core---graphenechain)

### Objects
- [graphene::chain Namespace: Class - Objects](../components/objects.md#bitshares-core---graphenechain)


***



### Block Header

#### block_header

    // *Block Header Inheritance* (i.e.) 1.0.0.0 
    // graphene::chain
    
    struct block_header
    {
        digest_type digest()const;
        block_id_type previous;
        uint32_t block_num()const { return num_from_id(previous) + 1; }
        fc::time_point_sec timestamp;
        witness_id_type witness;
        checksum_type transaction_merkle_root;
        extensions_type extensions;

        static uint32_t num_from_id(const block_id_type& id);
    };

 
#### signed_block_header
 
    // *Block Header Inheritance* (i.e.) 1.1.0.0
    // graphene::chain
        
    struct signed_block_header : public block_header
    {
        block_id_type id()const;
        fc::ecc::public_key signee()const;
        void sign( const fc::ecc::private_key& signer );
        bool validate_signee( const fc::ecc::public_key& expected_signee )const;

        signature_type witness_signature;
    };
 
#### signed_block
 
    // *Block Header Inheritance* (i.e.) 1.1.1.0
    // graphene::chain
        
    struct signed_block : public signed_block_header
    {
        checksum_type calculate_merkle_root()const;
        vector<processed_transaction> transactions;
    };

 
#### signed_block
  
    // *Block Header Inheritance* (i.e.) 1.1.1.1
    // graphene::wallet
    
    struct signed_block_with_info : public signed_block
    {
        signed_block_with_info( const signed_block& block );
        signed_block_with_info( const signed_block_with_info& block ) = default;

        block_id_type block_id;
        public_key_type signing_key;
        vector< transaction_id_type > transaction_ids;
    };
 
 ***
 

 ### Message Header
 Defines an 8 byte header that is always present because the minimum encrypted packet, size is 8 bytes (blowfish).  The maximum message size is defined in config.hpp. The channel, and message type is also included because almost every channel will have a message type field and we might as well include it in the 8 byte header to save space.
 
 #### message_header
 
      // *message Header Inheritance* (i.e.) 1.0.0.0 
      // graphene::net

       struct message_header
      {
         uint32_t  size;   // number of bytes in message, capped at MAX_MESSAGE_SIZE
         uint32_t  msg_type;  // every channel gets a 16 bit message type specifier
      };

      typedef fc::uint160_t message_hash_type;

#### message
Abstracts the process of packing/unpacking a message for a particular channel.
   
      struct message : public message_header
      {
         std::vector<char> data;

         message(){}

         message( message&& m )
         :message_header(m),data( std::move(m.data) ){}

         message( const message& m )
         :message_header(m),data( m.data ){}

         /**
          *  Assumes that T::type specifies the message type
          */
         template<typename T>
         message( const T& m ) 
         {
            msg_type = T::type;
            data     = fc::raw::pack(m);
            size     = (uint32_t)data.size();
         }

         fc::uint160_t id()const
         {
            return fc::ripemd160::hash( data.data(), (uint32_t)data.size() );
         }

         /**
          *  Automatically checks the type and deserializes T in the
          *  opposite process from the constructor.
          */
         template<typename T>
         T as()const 
         {
             try {
              FC_ASSERT( msg_type == T::type );
              T tmp;
              if( data.size() )
              {
                 fc::datastream<const char*> ds( data.data(), data.size() );
                 fc::raw::unpack( ds, tmp );
              }
              else
              {
                 // just to make sure that tmp shouldn't have any data
                 fc::datastream<const char*> ds( nullptr, 0 );
                 fc::raw::unpack( ds, tmp );
              }
              return tmp;
             } FC_RETHROW_EXCEPTIONS( warn, 
                  "error unpacking network message as a '${type}'  ${x} !=? ${msg_type}", 
                  ("type", fc::get_typename<T>::name() )
                  ("x", T::type)
                  ("msg_type", msg_type)
                  );
         }
      };


