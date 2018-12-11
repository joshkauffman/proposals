# How To Create An Internal Msig That Will Satisfy An External Msig

**Example problem:** There is an msig proposal put forth to all active Block Producers. 
Since the `eoscanadacom` active permissions requires a weight of 4, derived from multiple 
signers within EOS Canada, an internal msig needs to be crafted.

## Steps

1. Create the transaction JSON file
  ```
eosc multisig approve [proposer] [proposal_name] eoscanadacom@active --expiration 3600 --skip-sign --write-transaction [file_name].json
```
Use the `expiration` field to ensure you'll have enough time to gather the required threshold.

2. To verify that you have the required authorizations in place, run:
```
eosc tx unpack [file_name].json
```
You should have a print out like this:
```
{
  "expiration": "2018-12-10T21:12:40",
  "ref_block_num": 25106,
  "ref_block_prefix": 3701366316,
  "max_net_usage_words": 0,
  "max_cpu_usage_ms": 0,
  "delay_sec": 0,
  "context_free_actions": [],
  "actions": [
    {
      "account": "eosio.msig",
      "name": "approve",
      "authorization": [
        {
          "actor": "eoscanadacom",
          "permission": "active"
        }
      ],
      "data": {
        "level": {
          "actor": "eoscanadacom",
          "permission": "active"
        },
        "proposal_name": [proposal_name],
        "proposer": [proposer]
      }
    }
  ],
  "transaction_extensions": [],
  "signatures": [],
  "context_free_data": []
}
```

3. To create the internal msig, run:
```
eosc multisig propose [your_account_name] [second_proposal_name] [file_name].json --requested-permissions eoscanadacom@active --with-subaccounts
```
Using the `--with-subaccounts` flag will automatically fill in all of the account names associated to that permission.

4. Pass along
```
eosc multisig review [your_account_name] [second_proposal_name]
```
And now you pester everyone on Slack :)





