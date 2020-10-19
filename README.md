# ABIForms
Solidity ABI Forms

# A way to shared agnostic microtagged forms with Solidity/RLP/ABI specs


## Spec
### JSON Schema

```js
{ 
    @id: "abiforms:v1:ethr",
    template: '<html><form data:sol-ref="abcde"><input type="text" name="username" value="rogelio" data:sol-input="string" /><input type="password" name="password" value="" data:sol-input="string" /></form></html>',
    abi: [
       "string",
       "string"
    ]
}
```

### Map to inputs

```
form_inputs = html.form.inputs
root.abi for each {
  temp = form_inputs[0]
}

// whitelist form fields...
const data = ethers.utils.defaultAbiEncoder.encode(root.abi, temp);
// html
// todo - sign(sha256(metadata+output))
// form id
id = root.form.id

// web3 or ethers call
method(params, data).call()
```

### Contract

```solidity
    function create(
        address signatoryA,
        address signatoryB,
        uint validUntil,
        string memory multiaddrReference,
        bytes32 agreementFormTemplateId,     // form id
        bytes calldata agreementForm,         // form data
        bytes32 r,
        bytes32 s,
        uint v,
        bytes memory digest
    ) 
    external returns (uint) {

```
### Extensions

HTML Microdata/JSON Schema is compatible with VC, SPA frameworks.


### References
[W3C Microdata](https://www.w3.org/TR/microdata/#the-basic-syntax)
