# Ethereum API Specification

## JSON-RPC

[View the spec][playground]

The Ethereum JSON-RPC is a collection of methods that all clients implement.
This interface allows downstream tooling and infrastructure to treat different
Ethereum clients as modules that can be swapped at will.

### Building

The specification is split into multiple files to improve readability. The 
spec can be compiled into a single document as follows:

```console
$ npm install
$ npm run build
Build successful.
```

This will output the file `openrpc.json` in the root of the project. This file
will have all schema `#ref`s resolved.

### Contributing

The specification is written in [OpenRPC][openrpc]. Refer to the
OpenRPC specification and the JSON schema specification to get started.

#### Testing

There are currently three tools for testing contributions. The main two that
run as GitHub actions are an [OpenRPC validator][validator] and a
[spellchecker][spellchecker]:

```console
$ npm install
$ npm run lint
OpenRPC spec validated successfully.

$ pip install pyspelling
$ pyspelling -c spellcheck.yaml
Spelling check passed :)
```

The third tool can validate a live JSON-RPC provider hosted at
`http://localhost:8545` against the specification:

```console
$ ./scripts/debug.sh eth_getBlockByNumber \"0xc7d772\",false
data.json valid
```

## GraphQL

[View the spec][graphql-schema]

[EIP-1767][eip-1767] proposed a GraphQL schema for interacting with Ethereum clients. Since then Besu and Geth have implemented the interface. This repo contains a live specification to integrate changes to the protocol as well as other improvements into the GraphQL shema.

### Generation

The schema in this repo is generated by issuing a meta GraphQL query against a live node. This can be done as follows:

```console
$ npm run graphql:schema
```

### Testing

A script is included in the source code which reads and validates the given schema to be a valid one. It is recommended to perform this check after modifying the schema by:

```console
$ npm run graphql:validate
```

## License

This repository is licensed under [CC0](LICENSE).


[playground]: https://playground.open-rpc.org/?schemaUrl=https://raw.githubusercontent.com/ethereum/execution-apis/assembled-spec/openrpc.json&uiSchema[appBar][ui:splitView]=false&uiSchema[appBar][ui:input]=false&uiSchema[appBar][ui:examplesDropdown]=false
[openrpc]: https://open-rpc.org
[validator]: https://open-rpc.github.io/schema-utils-js/globals.html#validateopenrpcdocument
[spellchecker]: https://facelessuser.github.io/pyspelling/
[graphql-schema]: http://graphql-schema.ethdevops.io/?url=https://raw.githubusercontent.com/ethereum/execution-apis/main/graphql.json
[eip-1767]: https://eips.ethereum.org/EIPS/eip-1767
