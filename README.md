# Quantum Deep Learning with Qiskit  
### Team Ube Pancake  
## Project Background and Overview  
Recent advances in many fields have accelerated the demand for classification, regression, and detection problems from few 2D images/projections. Often, the heart of these modern techniques utilize neural networks, which can be implemented with deep learning algorithms. In our project, we wish to implement and extend a quantum analog of the classical implementation following the example of Hybrid quantum-classical Neural Networks with PyTorch and Qiskit, an example from the Qiskit Textbook (https://qiskit.org/textbook/ch-machine-learning/machine-learning-qiskit-pytorch.html#quantumlayer). 
## Implementation:  
By following the example of Hybrid Quantum-Classical Neural Networks from the Qiskit Textbook, we extend it to include implementations with more complex circuits and more complex classification tasks. 
#### Steps Taken:
Beginning with a 1-qubit layer in the neural network architecture used to identify handwritten 0 and 1 digits from the MNIST dataset, we have extended to implementing more complicated circuits, including using u3 (Unitary 3), Ry (rotation operation around the y-axis), and QFT (Quantum Fourier Transform) through PyTorch and Qiskit. Subsequently, we utilized the QuantumCircuit module in Qiskit we started developing an adaptable method to create any number of qubits 
#### Summary of Notebooks and Progress Made:
* **MNIST01-u3:** The first step involved improving the 1-qubit with a single Ry architecture to a more complex design: using a U3 transformation with parameters `theta`, `phi`, and `lambda`. Best accuracy: 97% on training data (100 images)
![u3 Circuit Drawing](https://github.com/liangqiyao990210/Quantum-Deep-Learning/blob/master/MNIST01-u3/Figures/1-qubit%20u3-circuit.jpg)
    * mnist01-u3.ipynb: heavily borrowed and improved from QizGloria, winners of 2019 Qiskit Camp Europe: https://github.com/BoschSamuel/QizGloria/blob/master/Notebooks/pytorch-qiskit-0.1-u3.ipynb
* **MNIST01-QFT:**
![QFT Circuit Drawing](https://github.com/liangqiyao990210/Quantum-Deep-Learning/blob/master/MNIST01-QFT/Figures/qft-circuit.jpg)
    * mnist01-qft.ipynb: in progress implementation of Quantum Fourier Transform
* **MNIST01-ryN:** The next step was to extend the 1-qubit, Ry architecture of the Qiskit Textbook example. By making the design modular, we are able to easily change the number of qubits in the architecture by adjusting a single parameter (NUM_QUBITS) at the top of the file. Best accuracy: 100.0% accurate
![ryN Circuit Drawing](https://github.com/liangqiyao990210/Quantum-Deep-Learning/blob/master/MNIST01-ryN/Figures/4-qubit%20circuit%20ryN.jpg)
    * mnist01-ryN-v1.ipynb: first extension of 1-qubit architecture; uses hard-coded circuit (4 qubits). Neural net and quantum circuit not working.
    * mnist01-ryN-v2.ipynb: adjustable NUM_qubits, quantum layer returns NUM_QUBIT outputs representing expected value for the $ZZ...Z$ operator, calculated from the counts returned by the circuit
    * mnist01-ryN-v3.ipynb: adjustable NUM_qubits, quantum layer returns 2^(NUM_QUBIT) outputs representing expected value of each unique permutation of measurements (e.g. '0000', '0001', '0010', etc.). Although this works well for classifying 0 and 1 (near perfect accuracy), this measurement does not scale well to classifications of a higher number of classes, such as of the digits 0-9 (see below in Summary & Discussion for explanation).
* **MNIST01-bell:** Best accuracy: 99.8% accurate (1712/1715 *previously unseen* test images correct) after training on 300 images.
![bell Circuit Drawing](https://github.com/liangqiyao990210/Quantum-Deep-Learning/blob/master/MNIST01-bell/Figures/4-qubit%20circuit%20bell.jpg)
    * mnist01-bell.ipynb: uses 1 measurement, quantum layer returns 2 outputs (representing counts) for 0 and 1.
* **MNIST01-NControlledUnitary:**
## Potential Applications:  
There could be many applications for our project such as in virtual reality, 3D game design, autonomous vehicle, 3D modeling/reconstuction, etc.  
## Summary of Results & Discussion
* Don't need more qubits than necessary
* Returning 2^NUM_QUBITS does not work as intended; this is because the circuit "thinks" that there should be some correlation with measurements that differ only by a little. For example, let's say we are trying to get the measurements of a 4-qubit circuit to match the binary encoding of the digits 0 to 9. There are a few unintended problems that manifest using this result. An easy thing to see is that, once can see that the first, most significant bit is only '1' for the numbers 8 and 9 ('1000' and '1001', respectively). Thus, the neural net would be trained to "know" that a guess of '0' for this bit leads to a higher chance of getting the classification right (80% of the time). This is a manifestation of greater problems, such as the fact that the layer treats numbers that are close in binary (such as '0111' [7] and '0101' [3]) are close, since their binary representations are only a single digit off, even though they appear very different when written. So, it's likely that only a certain subset of these output 
## Further Development:  
We hope that we can continue to train and improve our model with more data and that our project would eventually be of use for deployment in real-world applications.

*** Note: this is a project for submission in the IBM Qiskit Community SummerJam Quantum Hackathon (North Carolina) ***

<center><img src="https://i.ebayimg.com/images/g/HH4AAOSwPW9esi90/s-l400.jpg"></center>