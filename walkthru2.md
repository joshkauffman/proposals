Walkthru of having an account with an msig structure on it execute an msig

What is being done: accounting33 sends 1.5 EOS to accounting11. The permission structure of accounting33
is that both accounting11 and accounting22 need to sign.

Craft the transaction that sends 1.5 EOS from accounting33 to accounting11
```
eosc transfer accounting33 accounting11 1.5 --skip-sign --expiration 3500 --write-transaction 33.json --vault-file kylin.json -u https://kylin.eoscanada.com
```
Things to note: --skip-sign to not create the transaction, --expiration to allow a longer expiration time, 
`--write-transaction` to craft the json file, `--vault-file` just becuz i keep my kylin keys separate for testing, `-u https://kylin.eoscanada.com`
because we're on Kylin.

Create the msig to collect the signatures from both accounting11 and accounting22
```
eosc multisig propose accounting33 33to11 --requested-permissions accounting33 33.json --with-subaccounts --vault-file kylin.json -u https://kylin.eoscanada.com
```
Things to note: `--requested-permissions accounting33` means that it is looking to get the signatures that would 
satisfy the active permission of accounting33, `--with-subaccounts` automatically scrapes the permission structure of accounting33
to include the needed accounts/keys

Verify that everything looks like it should
```
eosc multisig review accounting33 33to11 --vault-file kylin.json -u https://kylin.eoscanada.com
```

Now we can start signing
```
eosc multisig approve accounting33 33to11 accounting11 --vault-file kylin.json -u https://kylin.eoscanada.com
eosc multisig approve accounting33 33to11 accounting22 --vault-file kylin.json -u https://kylin.eoscanada.com
```

Now we exec
```
eosc multisig exec accounting33 33to11 accounting33 --vault-file kylin.json -u https://kylin.eoscanada.com
```
