**Contract Succession Paradigm**
======================================

**Introduction**
---------------
The Contract Succession Paradigm (CSP) is a standardized mechanism for smart contracts to announce their obsoletion and point to a replacing smart contract. This allows for the safe and atomic passage of control to a successor smart contract, while enabling the evolution of the contract's state and functionality.

**Why CSP?**
-----------

By its very nature, immutable smart contracts cannot modify their own codebase, leading to limitations such as:

* Bugs that cannot be fixed
* Features that cannot be implemented
* Inability to adapt to changing requirements or use cases

The CSP addresses these issues by providing a standardized mechanism for smart contracts to evolve.


**Adhering to the CSP**
-----------
To adhere to the CSP, smart contracts should:
* Implement a setter for the following metadata fields:
	+ `cspScid`: The id of the successor smart contract
	+ `cspData`: Arbitrary additional (structured json-)data (technical and informative)
	+ `cspUpdated`: Timestamp indicating when any of the fields was updated


**Reference implementation**
-----------

The following function is a reference implementation and can be added to any smart contract:

```basic
Function SetCsp(scid String, data String) Uint64
1 IF LOAD("owner") != SIGNER() THEN GOTO 6
2 STORE("cspScid", scid)
3 STORE("cspData", HEXDECODE(data))
4 STORE("cspUpdated", BLOCK_TIMESTAMP())
5 RETURN 0
6 RETURN 1
End Function
```

This function allows the smart contract's "owner" to set and update the required metadata fields.

**Benefits**
-----------

By adhering to the Contract Succession Paradigm, smart contracts can:

* Announce their obsoletion and point to a replacing smart contract
* Provide additional metadata for tooling and management
* Enable the safe and atomic passage of control to a successor smart contract

All developers and maintainers of smart contracts are encouraged to implement the CSP and take advantage of its benefits.