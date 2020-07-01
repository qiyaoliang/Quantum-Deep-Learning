# Quantum Deep Learning with Qiskit  
### Team Ube Pancake  
## Objective:  
Recent advances in many fields have accelerated the demand for classification, regression, and detection problems from few 2D images/projections. Often, the heart of these modern techniques utilize neural networks, which can be implemented with deep learning algorithms. In our project, we wish to implement and extend a quantum analog of the classical implementation following the example of Hybrid quantum-classical Neural Networks with PyTorch and Qiskit, an example from the Qiskit Textbook (https://qiskit.org/textbook/ch-machine-learning/machine-learning-qiskit-pytorch.html#quantumlayer).  
## Implementation:  
By following the example of Hybrid Quantum-Classical Neural Networks from the Qiskit Textbook, we extend it to include implementations with more complex circuits and more complex classification tasks. 
#### Steps:
Beginning with a 1-qubit layer in the neural network architecture used to identify handwritten 0 and 1 digits from the MNIST dataset, we have extended to implementing more complicated circuits, including using u3 (Unitary 3), Ry (rotation operation around the y-axis), and QFT (Quantum Fourier Transform) through PyTorch and Qiskit. Subsequently, we utilized the QuantumCircuit module in Qiskit we started developing an adaptable method to create any number of qubits 
## Potential Applications:  
There could be many applications for our project such as in virtual reality, 3D game design, autonomous vehicle, 3D modeling/reconstuction, etc.  
## Final Result: 
We hope to train a model that could be readily used for depth perception.  
#### Summary of Notebooks and Progress Made:
* **MNIST01-u3:** The first step involved improving the 1-qubit with a single Ry architecture to a more complex design: using a U3 transformation with parameters `theta`, `phi`, and `lambda`. Best accuracy: 97% on test
    * mnist01-u3: heavily borrowed and improved from QizGloria, winners of 2019 Qiskit Camp Europe: https://github.com/BoschSamuel/QizGloria/blob/master/Notebooks/pytorch-qiskit-0.1-u3.ipynb
* **MNIST01-QFT:**
    * mnist01-qft: in progress implementation
* **MNIST01-ryN:** The next step was to extend the 1-qubit, Ry architecture of the Qiskit Textbook example. By 
## Further Development:  
We hope that we can continue to train and improve our model with more data and that our project would eventually be of use for deployment in real-world applications.

*** Note: this is a project for submission in the IBM Qiskit Community SummerJam Quantum Hackathon (North Carolina) ***

<center><img src="https://i.ebayimg.com/images/g/HH4AAOSwPW9esi90/s-l400.jpg"></center>
