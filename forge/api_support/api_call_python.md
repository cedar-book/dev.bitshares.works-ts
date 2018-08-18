## BitShares Python API Call - examples

#### Table of Contents:
-
-
-
-

***

### API

#### /account

~~~
curl -X GET --header 'Accept: application/json' 'http://185.208.208.184:5000/account?account_id=1.2.4'
~~~

Response Body

~~~
[
  {
    "active": {
      "account_auths": [],
      "address_auths": [],
      "key_auths": [],
      "weight_threshold": 0
    },
    "active_special_authority": [
      0,
      {}
    ],
    "blacklisted_accounts": [],
    "blacklisting_accounts": [],
    "id": "1.2.4",
    "lifetime_referrer": "1.2.4",
    "lifetime_referrer_fee_percentage": 8000,
    "membership_expiration_date": "1969-12-31T23:59:59",
    "name": "temp-account",
    "network_fee_percentage": 2000,
    "options": {
      "extensions": [],
      "memo_key": "BTS1111111111111111111111111111111114T1Anm",
      "num_committee": 0,
      "num_witness": 0,
      "votes": [],
      "voting_account": "1.2.5"
    },
    "owner": {
      "account_auths": [],
      "address_auths": [],
      "key_auths": [],
      "weight_threshold": 0
    },
    "owner_special_authority": [
      0,
      {}
    ],
    "referrer": "1.2.4",
    "referrer_rewards_percentage": 0,
    "registrar": "1.2.4",
    "statistics": "2.6.4",
    "top_n_control_flags": 0,
    "whitelisted_accounts": [],
    "whitelisting_accounts": []
  }
]
~~~

#### /account_id

~~~
curl -X GET --header 'Accept: application/json' 'http://185.208.208.184:5000/account_id?account_name=committee-account'
~~~

Response Body

~~~
"1.2.0"
~~~

Response Headers

~~~
{
  "access-control-allow-origin": "*",
  "connection": "keep-alive",
  "content-length": "8",
  "content-type": "application/json",
  "date": "Sat, 18 Aug 2018 04:29:04 GMT",
  "server": "nginx/1.6.2"
}
~~~

#### /acount_name

~~~
curl -X GET --header 'Accept: application/json' 'http://185.208.208.184:5000/account_name?account_id=1.2.0'
~~~

Response Body

~~~
"committee-account"
~~~

#### /accounts
(*Get an account list of the most 100 rich CORE holders.*)

~~~
curl -X GET --header 'Accept: application/json' 'http://185.208.208.184:5000/accounts'
~~~

Response Body

~~~
[
  {
    "account_id": "1.2.20067",
    "amount": "19019320146385",
    "name": "poloniexwallet"
  },
  {
    "account_id": "1.2.809079",
    "amount": "16119240552757",
    "name": "bitkkchubei002"
  },
  {
    "account_id": "1.2.479516",
    "amount": "11478766398323",
    "name": "binance-cold-1"
  },
  ...
 ]
~~~  
  
  
  



