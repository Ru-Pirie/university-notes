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
