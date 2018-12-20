eosc transfer accounting11 accounting22 2.2222 --memo "walkthru of msig" --skip-sign --expiration 3600 --write-transaction walkthru.json --vault-file kylin.json -u https://kylin.eoscanada.com
what is the tx we want to happen

eosc multisig propose accounting11 doesitwork walkthru.json --requested-permissions accounting11@active,accounting22@active --vault-file kylin.json -u https://kylin.eoscanada.com
wrap that tx into an msig, with the requested signers

eosc multisig review accounting11 doesitwork -u https://kylin.eoscanada.com
to double check it's on the chain

eosc multisig approve accounting11 doesitwork accounting11 --vault-file kylin.json -u https://kylin.eoscanada.com
signing it with first account

eosc multisig approve accounting11 doesitwork accounting22 --vault-file kylin.json -u https://kylin.eoscanada.com
signing it with second account

eosc multisig status accounting11 doesitwork -u https://kylin.eoscanada.com
ensure that we have all the required signatures

eosc multisig exec accounting11 doesitwork accounting22 --vault-file kylin.json -u https://kylin.eoscanada.com
exec the msig
