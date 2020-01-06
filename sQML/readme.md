# sQML: Simple- Quantum Language  
  
This is my language is designed for my "Simple Quantum Computer System Simulator" (tentative name), which I made during my internship at
IIIT-Delhi. It is , in **NO WAY** targed as competition to the professional simulators like Qiskit, Qcirq, Pennylane, Forest or Ocean. 
On the contrary, it is aimed at providing a simple, very basic, quantum computer simulation capabilities, that anyone can read and 
quickly modify it to their research needs.  
  
Need a custom simulator for Quantum Machine Learning?, Quantum Biology? or Quantum Chemistry? or anything else, Simple quantum simulator 
is easy, modular, and super fast to modify for any project related to quantum!  

Entire software stack is divided into 4 modules: (this is tentative and subjected to change)

* [Language processor](lang_proc.md).
* [Quantum Gate](q_gate.md).
* [Assembler](q_asm.md).
* [Simulator](q_sim.md).
* [OpenQASM Wrapper](qasm_warp.md) _this is a alpha-level thought work will be done later_

## sQML: Syntax  

___
### Gate Library Syntax
**NOTE: DO NOT put '_underscore' in GateName. It is a special charater**
The gate libary can be used for defining custom gates. Its syntax is as follows:   
```
GateName:(gate matrix)
```
  
___   

### Circuit File Syntax
The circuit file can be defined as follows:  
* For single qubit gate:
```
GateName:(qubit number)
```   

* For CNOT gates:  
**NOTE: Qubits number must ONLY be in ascending order**
```
For CNOT Gate:
cnot:(control_qubit, target_qubit)

For reversed CNOT Gate:
cnot_r:(target_qubit, control_qubit)
```  

* Custom U-Gates:
```
u3_(theta,phi,lambda):(qubit number)

u2_(phi,lambda):(qubit number)

u1_(lambda):(qubit number)
```
  
* Custom Rotation gates:
```
rx_(angle):(qubit number)

ry_(angle):(qubit number)

rz_(angle):(qubit number)
```
