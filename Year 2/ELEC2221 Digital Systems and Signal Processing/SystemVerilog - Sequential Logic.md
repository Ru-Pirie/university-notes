Arithmetic opertor will be synthesised to combniational logic
- Arithmetic operations + - are mapped into standard adders / subtractors
- The multiplication operator * can be mapped into embedded multipliers but you have to follow code templates provided by the fpga vendor
		- Mapping * into combinational cellular logic will take up far more space.
## Bitwise Operators
~ - negation
& - AND
~& - NAND
| - OR
~| - NOR
^ - XOR
~^ - XNOR

```verilog
logic [3:0] x;
&x; // This takes all the elements in the x array and AND's together all of the bits of the vector
```
This can be usefull for example if you want to check if everything is 0, you could do `|x;` which would tell you if every element was 0;

If you had a binary counter and wanted to keep going untill lets say 
```verilog
logic [3:0] counter;
while(~&counter) do
```
This will loop untill all the bits of counter are 1

## Case
There is such a thing as a priority case which is a specal one where each element of the case statement are considered as they are presented. This is a little bit odd just use an if statement if you want to do that.
