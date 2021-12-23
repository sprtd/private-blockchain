# Private Blockchain Application
An `express.js` app whose endpoints are defined in `BlockchainController.js`.  



## Tests

`baseURL: http://localhost:8000/`


###  Test 1: `getBlockByHeight`

`GET - {{ _.baseURL }}/block/height/0`
The response shows the genesis block, block height 0 which is the precursor of subsequent blocks:
```json
{
	"hash": "29238d9e92a4c2ba36d42b01898cad235ae1269572a4e6212d8d7d989d8039a7",
	"height": 0,
	"body": "7b2264617461223a2247656e6573697320426c6f636b227d",
	"time": "1640298081",
	"previousBlockHash": null
}
```


### Test 2: `requestOwnership`

Endspoint generates a message with the following format `<WALLET_ADDRESS>:<TIME>:starRegistry`.  
`POST - {{ _.baseURL }}/requestValidation`
```
--header 'Content-Type: application/json' \
--data-raw '{
    "address" : "1KEniWgGgxyLUpiAHB7quKYiSbshP6QsS5"
}'
```
Response:
`"1KEniWgGgxyLUpiAHB7quKYiSbshP6QsS5:1640298483:starRegistry"`



### Test 3: `submitStar`

`POST - {{ _.baseURL }}/submitstar`

```
--header 'Content-Type: application/json' \
--data-raw '{
    "address" : "1KEniWgGgxyLUpiAHB7quKYiSbshP6QsS5",
    "signature" : "H3lyrvcXspXzrmsN94wOQ59wI/JWV4IEP3NXv7b3G82wTOk55vUsGJHpCX2bbeVJUWpSpQFvQaBro0xykfqkrQI=",
    "message" : "1KEniWgGgxyLUpiAHB7quKYiSbshP6QsS5:1640298483:starRegistry",
    "star" : {
        "dec" : "68 52 56.9",
        "ra" : "16h 29m 1.0s",
        "story" : "Alpha 1"
    }
}'
```

This POST request returns the following response:
```json
{
    "hash": "590d3577dbe5c2391a1151028a04177983cc2ff16d38049da0fa1246001bc705",
    "height": 1,
    "body": "b2261646472657373223a22314b456e695767476778794c5570694148423771754b596953627368503651735335222c226d65737373616765223a22314b456e695767476778794c5570694148423771754b5969536273685036517353353a313634303239383438333a737461725265676973747279222c227369676e6174757265223a2248336c79727663587370587a726d734e3934774f51353977492f4a575634494550334e587637623347383277544f6b3535765573474a4870435832626265564a5557705370514676516142726f3078796b66716b7251493d222c2273746172223a7b22646563223a2236382035322035362e39222c227261223a223136682032396d20312e3073222c2273746f7279223a22416c7068612031227d7d",
    "time": "1640298577",
    "previousBlockHash": "29238d9e92a4c2ba36d42b01898cad235ae1269572a4e6212d8d7d989d8039a7"
}
```



### Test 4: `getBlockByHash`

`GET - {{ _.baseURL }}/block/hash/590d3577dbe5c2391a1151028a04177983cc2ff16d38049da0fa1246001bc705`
Response:
```json
{
	"hash": "590d3577dbe5c2391a1151028a04177983cc2ff16d38049da0fa1246001bc705",
	"height": 1,
	"body": "7b2261646472657373223a22314b456e695767476778794c5570694148423771754b596953627368503651735335222c226d65737373616765223a22314b456e695767476778794c5570694148423771754b5969536273685036517353353a313634303239383438333a737461725265676973747279222c227369676e6174757265223a2248336c79727663587370587a726d734e3934774f51353977492f4a575634494550334e587637623347383277544f6b3535765573474a4870435832626265564a5557705370514676516142726f3078796b66716b7251493d222c2273746172223a7b22646563223a2236382035322035362e39222c227261223a223136682032396d20312e3073222c2273746f7279223a22416c7068612031227d7d",
	"time": "1640298577",
	"previousBlockHash": "29238d9e92a4c2ba36d42b01898cad235ae1269572a4e6212d8d7d989d8039a7"
}
```




### Test 5: `getStarsByWalletAddress`
Endpoints filters blocks signed by wallet addresses with valid stars:
`GET - {{ _.baseURL }}/blocks/1KEniWgGgxyLUpiAHB7quKYiSbshP6QsS5`

The response shows block signed by the specific star address:
```json
[
	{
		"address": "1KEniWgGgxyLUpiAHB7quKYiSbshP6QsS5",
		"messsage": "1KEniWgGgxyLUpiAHB7quKYiSbshP6QsS5:1640298483:starRegistry",
		"signature": "H3lyrvcXspXzrmsN94wOQ59wI/JWV4IEP3NXv7b3G82wTOk55vUsGJHpCX2bbeVJUWpSpQFvQaBro0xykfqkrQI=",
		"star": {
			"dec": "68 52 56.9",
			"ra": "16h 29m 1.0s",
			"story": "Alpha 1"
		}
	}
]
```
