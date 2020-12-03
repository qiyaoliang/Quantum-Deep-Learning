# Quantum Deep Learning with Qiskit  
### Team Ube Pancake  
## Project Background and Overview  
Recent advances in many fields have accelerated the demand for classification, regression, and detection problems from few 2D images/projections. Often, the heart of these modern techniques utilize neural networks, which can be implemented with deep learning algorithms. In our neural network architecture, we embed a dynamically programmable quantum circuit, acting as a hidden layer, to learn the correct parameters to correctly classify handwritten digits from the MNIST database. By starting small and making incremental improvements, we successfully reach a stunning ~95% accuracy on identifying previously unseen digits from 0 to 7 using this architecture!

**For our most RECENT work, see folder [MNIST/0-7 3-qubit](https://github.com/liangqiyao990210/Quantum-Deep-Learning/tree/master/MNIST/0-7%203qubits%2010epochs%2095%25), where we train our hybrid quantum-classical network to get 94.7% accuracy on MNIST handwritten digits from 0 to 7.**

## Video and Presentation:
#### Video
[Link to YouTube video](https://youtu.be/dlIZVF9xVpU)

#### Presentation
[Click here view our presentation slides (PDF).](https://github.com/liangqiyao990210/Quantum-Deep-Learning/blob/master/Quantum%20Deep%20Learning.pdf) [PPTX Version](https://github.com/liangqiyao990210/Quantum-Deep-Learning/blob/master/Quantum%20Deep%20Learning.pptx)

## Implementation:  
By following the example of Hybrid Quantum-Classical Neural Networks from the Qiskit Textbook, we extend it to include implementations with more complex circuits and more complex classification tasks. 

#### Steps Taken:
Beginning with a 1-qubit layer in the neural network architecture used to identify handwritten 0 and 1 digits from the MNIST dataset, we have extended to implementing more complicated circuits, including using u3 (Unitary 3), Ry (rotation operation around the y-axis), and QFT (Quantum Fourier Transform) through PyTorch and Qiskit. Subsequently, we utilized the QuantumCircuit module in Qiskit we started developing an adaptable method to create any number of qubits we want! 

#### Summary of Notebooks and Progress Made:
* **MNIST01-u3:** The first step involved improving the 1-qubit with a single Ry architecture to a more complex design: using a U3 transformation with parameters `theta`, `phi`, and `lambda`. Best accuracy: 97% on training data (100 images)<p align="center"><img src="https://github.com/liangqiyao990210/Quantum-Deep-Learning/blob/master/MNIST01-u3/Figures/1-qubit%20u3-circuit.jpg" width="60%">
  * mnist01-u3.ipynb: heavily borrowed and improved from QizGloria, winners of 2019 Qiskit Camp Europe: https://github.com/BoschSamuel/QizGloria/blob/master/Notebooks/pytorch-qiskit-0.1-u3.ipynb

* **MNIST01-QFT:** Quantum Fourier Transform is commonly used in quantum algorithms, so we tried to implement this circuit next to train our model.<p align="center"><img src="https://github.com/liangqiyao990210/Quantum-Deep-Learning/blob/master/MNIST01-QFT/Figures/qft-circuit.jpg" width="60%">
  * mnist01-qft.ipynb: in progress implementation of Quantum Fourier Transform.

* **MNIST01-ryN:** The next step was to extend the 1-qubit, Ry architecture of the Qiskit Textbook example. By making the design modular, we are able to easily change the number of qubits in the architecture by adjusting a single parameter (NUM_QUBITS) at the top of the file. Best accuracy: 100.0%!<p align="center"><img src="https://github.com/liangqiyao990210/Quantum-Deep-Learning/blob/master/MNIST01-ryN/Figures/4-qubit%20circuit%20ryN.jpg" width="60%">
  * mnist01-ryN-v1.ipynb: first extension of 1-qubit architecture; uses hard-coded circuit (4 qubits). Neural net and quantum circuit not working.
  * mnist01-ryN-v2.ipynb: adjustable NUM_qubits, quantum layer returns NUM_QUBIT outputs representing expected value for the ZZ...Z operator, calculated from the counts returned by the circuit.
  * mnist01-ryN-v3.ipynb: adjustable NUM_qubits, quantum layer returns 2^(NUM_QUBIT) outputs representing expected value of each unique permutation of measurements (e.g. '0000', '0001', '0010', etc.). Although this works well for classifying 0 and 1 (near perfect accuracy), this measurement does not scale well to classifications of a higher number of classes, such as of the digits 0-9 (see below in Summary & Discussion for explanation).

* **MNIST01-bell/GHZ:** Now, we try using the 'bell' circuit, which employs a dynamic number of qubits. This generates **ENTANGLEMENT**! We wanted to see how this would perform compared to the other circuits, which mostly have isolated qubits which don't interact with each other. The results were ***remarkable***! Best accuracy: 99.8% accurate (1712/1715 *previously unseen* test images correct) after training on 300 images.<p align="center"><img src="https://github.com/liangqiyao990210/Quantum-Deep-Learning/blob/master/MNIST01-bell/Figures/4-qubit%20circuit%20bell.jpg" width="60%">
  * mnist01-bell.ipynb: current implementation uses 4 qubits and takes 1 measurement, resulting with 2 outputs (representing counts) for each of 0 and 1. Here are some sample predictions (again, for random, previously unseen test images):
   <p align="center">
      <img src="https://github.com/liangqiyao990210/Quantum-Deep-Learning/blob/master/misc_images/MNIST01-prediction-samples.jpg" width = "60%">
    
* **MNIST01-QAOA:** Using 2 qubits, we try to create a circuit modeling the popular QAOA. Currently, the training loss does not converge, so fixes must be added before the model will train and predict well!<p align="center"><img src="https://github.com/liangqiyao990210/Quantum-Deep-Learning/blob/master/MNIST01-QAOA/Figures/2-qubit%20circuit%20ryN.jpg" width="60%">
  * mnist01-QAOA.ipynb: Currently having problems running inside the model! Deprecated in favor of training MNIST, but potential improvements may be implemented in the future.

* **MNIST:** In the most recent step of our project, we extended our learning about the Qiskit + Pytorch framework to classifying a higher number of classes, where we try classifying the digits from 0 to 7.  By tweaking hyperparameters and the number of qubits, we reached a **stunning 94.7% accuracy** on classifying 1200 previously unseen test images from 0 to 7.
  * Each subfolder is named by [0-5 or 0-7] [# of qubits] [# epochs] [% accuracy on test data], and each folder contains a screenclip of the final accuracy, the graph of training loss over each epoch, sample predicitons of test data, and the iPython notebook used.
  * Here is a sample of predictions for labels on test images from the [07 3qubit 10epochs 95%](https://github.com/liangqiyao990210/Quantum-Deep-Learning/tree/master/MNIST/0-7%203qubits%2010epochs%2095%25) run:
  <p align="center"><img src="https://github.com/liangqiyao990210/Quantum-Deep-Learning/blob/master/misc_images/Predictions%200%20to%207.png" width="60%">
   
## Summary of Results & Discussion
* Hybrid NNs could have potential applications for NISQ devices!! (Using Qiskit and Pytorch)
* Through this project, we gained a deeper understanding of Qiskit's circuit-building and integration with the popular package Pytorch. After playing with different circuit structures, data, training hyperparameters, and model architectures, we fine-tuned our model to fit it for the right task.
* An important takeaway is that *choosing the right number of qubits for the task* is a key part. For simpler training (e.g. distinguishing MNIST's 0's and 1's), we don't need more qubits than necessary.
* Returning 2^NUM_QUBITS from the quantum layer's output does not work as intended; this is because the circuit "thinks" that there should be some correlation with measurements that differ only by a little. For example, let's say we are trying to get the measurements of a 4-qubit circuit to match the binary encoding of the digits 0 to 9. There are a few unintended problems that manifest using this result. An easy thing to see is that, once can see that the first, most significant bit is only '1' for the numbers 8 and 9 ('1000' and '1001', respectively). Thus, the neural net would be trained to "know" that a guess of '0' for this bit leads to a higher chance of getting the classification right (80% of the time). This is a manifestation of greater problems, such as the fact that the layer treats numbers that are close in binary (such as '0111' [7] and '0101' [3]) are close, since their binary representations are only a single digit off, even though they appear very different when written. So, it's likely that only a certain subset of these output were being trained, while the rest were being ignored.
   
## Potential Applications:  
In the realm of classification tasks, there are many obvious places where this project could be used. Beyond classification, hybrid quantum-classical neural net architectures could be deployed in many data-intensive applications, such as in virtual reality, 3D game design, autonomous vehicle, 3D modeling/reconstuction, etc.  

## Further Development:  
Below are some of the short-term improvements we can make on the project to extend this towards real-world application:
1. Try out different classification problems:
    * MNIST Fashion, Cats and dogs, etc. 
2. Try out different circuits:
    * Investigate the differences between multiple parameters per single qubit versus multiple qubits each with a single parameter
    * Try out more complex circuits, composite circuits, entanglement-generating circuits, n-controlled unitary, etc. (in progress)
    * Explore suitable circuits for specific problems
3. Implement CUDA for GPU acceleration of training
4. Implement on NISQ devices (IBM quantum hardware) - already begun:
    * Try training our neural nets on the actual IBM machine (have attempted)
    * Compare results from an actual hardware with that from the simulator
    * Implement QECCs (Quantum Error Correction)

Beyong classification tasks, we hope that we can continue to train and improve our model with more data and that our project would eventually be of use for deployment in real-world applications, and perhaps personally become involved in this field of research with IBM!

*** Note: this is a project for submission in the IBM Qiskit Community SummerJam Quantum Hackathon (North Carolina) ***

<p align="center"><img src="https://i.ebayimg.com/images/g/HH4AAOSwPW9esi90/s-l400.jpg">
