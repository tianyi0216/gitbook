# Lec05

Pytorch

1. Floating point operations - scientific computing/ML. On CPU or GPU. Distributed computing.
2. Optimization features.
3. ML.

Numeric types

Python:

ints: no maximum/minimum size. Bigger/smaller values => more bits necessary.

floats: use the one supported by cpu natively. Usually 64 bits, (double precision), 32 bits (single precision) (like exponential notation)

Complex



Pytorch

Overflow and underflow for integer. (e.g if int get to largest)

Float - does not overflow, but can ge saturated (float\_info.max, float\_info.min)

inf and nan.



float\_info.dig # number of digit it can represent (precision(

float\_info.epsilon&#x20;

x = 1.0

x + float\_info.epsilon # next number after 1.0



