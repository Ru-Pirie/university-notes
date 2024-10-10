## Packed vs Unpacked
```systemverilog
logic [7:0] register [0:15];
```
This is a thing called "register" of type **logic** which has 8 bits and 16 addresses.

Packed dimmensions:
- Are guarenteed to be laid out contiguously in memory
- can be copied onto any other pcked object of same size
- can be sliced
- are restricted to bit types: bit, logic etc...
Unpacked dimmensions:
- can be arranged in memory as simulator chooses
- only unpacked arrays of teh same type can be copied
- can be used with all data types
## Enumberated data types
```systemverilog
enum {Monday, Tuesday, Wednesday, Thursday, Friday} WeekDay;
state present, next;
typedef enum {idle, cycle1, cycle2};
enum {a=0, b=7, c=5, d=8} myEnum;
```
The named values of an enumeration type act as int constants. Enumerations are strongly types.
```systemverilog
present=2 // ERROR, cant assign a numerical constant to an enum object
present = state'(2); // type castnig must be used instead
```
## Literals
```systemverilog

1'b0;
4'hF;
10;
'o6;
```
Binary, Hex, Decimal, Octal

Base represents the radix, default is decimal

# Hierarchy
- Define each of the blocks as a module and instanciate each module in a top level module
- Define each of the signals connecting modules
## CPU Example
### Parameters
```systemverilog
module cpu #(parameter Dsize=8)
	(input logic clk, input logic reset, output logic[Dsize-1:0] outport);
```
```systemverilog
cpu #(.Dsize(8)) c0 (.*); // Note the ports are mapped implicitly 
```
```systemverilog
parameter Psize = 6;
```
### Port Mapping
- Named Port Mapping
	- used where implicit mapping cannot be used
- Implicit Port Mapping
	- 'magic' SystemVerilog mapping with .*
- Positional (ordered) Port Mapping
	- ports are passed in the order in which they are used
#### Named Port Mapping
```systemverilog
prog #(.Psize(Psize), .Isize(Isize))
progMemory(.address(ProgAddress),.I(I));
```
Named mapping may always be used in prefernce to other mapping styles but must be used when the port names in the module are not the same as the variables defined in a higher module.
Can be used when 
- The port and connecting sizes do not matter
- The port is to be left unconnected
#### Positional Port Mapping
```systemverilog
prog #(PSize, Isize)
progMemory(ProgAddress,I);
```
### Implicit Port Mapping
```systemverilog
cpu c0 (.*);
```
There are six rules in order to use Implicit Port Mapping.
1. Named and implicit ports may be mixed in the same instansiation but there must only be one implicit item
2. Positional  and implicit ports may be mixed same as above
3. Implicit mapping may not be used if the port and connecting net sizes do not match
4. Immplicit mapping may not be used if the port and connecting net have different names
5. Implicit mapping may not be used if the port is unconnected
6. All nets or variables connected to the implicit ports must be delcared in the instantiationg module, either as explicit local declatations or as explicit port declerations
# picoMIPS
## Rough ALU thing
```systemverilog
logic [2:0] ALUfunc
logic V,N,Z,C;
logic imm;
logic [Dsize-1:0];

parameter Aasize = 5;
logic [Dsize-1:0] Rdata1, Rdata2, Wdata;
logic w;

paarameter Psize = 4;
logic PCiner,PCabsbranch,PCrelbranch;

logic [Psize-1:0]
```