# 3d-Growing-neural-cellular-automata
This project is inspired by the paper "Growing Neural Cellular Automata" found at the link: https://distill.pub/2020/growing-ca/.

Find the  Colab document of this project at:
https://colab.research.google.com/drive/1F3xIUltW6hg9AVLXfJq7c8IMRp8Leq01?usp=sharing

The project explores the fascinating concept of Neural Cellular Automata (NCA) and its application in modeling complex morphogenetic processes. The primary aim is to learn the local-level rules that govern the growth of a structure from a single cell, ultimately leading to the creation of a specific type of structure.

The project's objective is to develop an extension of the methodology described in the paper “Growing Neural Cellular Automata” to facilitate complex structure generation in three dimensions

## Algorithm Details 

## Defining Target Object
The process starts by representing the iniput file in a format suitable for 3d convolutional operation. Prior to training the model to learn the update rule defining the global structure of the 3d object, the object is represented as a stack of RGBA values. Every layer in the stack holds information about the 3d object for a particular z coordinate, where the layer also represents the corresponding x and y coordinates of the voxel along with the RGB value. The data is finally presented as a 4d array for further processing. Subsequently, the resulting matrix can be visualized using the matplotlib library.

 ![image](https://github.com/Aadityaza/3d-Growing-neural-cellular-automata/assets/45432533/c0e0d125-3a00-4fe8-95cd-c52f6317f5a7)

Figure : Defining target 

The target is defined as a 4D numpy array, where the first three dimensions represent the x, y, and z coordinates of a 3D object, and the last dimension represents the RGB and alive channel. The RGB values for each voxel are normalized to a range of 0 to 1 by dividing them by 255.                                                                                                                              



## Define seed
After defining the target, an initial seed must be established for the structure to grow from. This seed comprises of a single cube situated at the center of the 3d space.

 ![image](https://github.com/Aadityaza/3d-Growing-neural-cellular-automata/assets/45432533/e1fe4fcd-aab4-4123-9fd0-2d3effad2666)
 
Figure : Seed value

## Model Architecture

![image](https://github.com/Aadityaza/3d-Growing-neural-cellular-automata/assets/45432533/451e2b92-1709-423d-8359-5388f1369886)

The 2D convolution used in the original paper is replaced with a 3D convolution to allow for cell awareness of its neighbors in the 3D space. In contrast to [1], a learnable perception network akin to [7] is used rather than a static perception network with a Sobel filter. The dynamic perception network is realized as a 3D convolutional layer with a kernel size of 3, a stride of 1, output channels equal to the cell state channels multiplied by 3, and an activation function of tf.nn.relu. Similar to [1], a stochastic update approach is adopted, in which the output of the CA is multiplied by a randomly generated binary matrix with half of its values being 0. Then, the "alive mask" is applied to the updates, which leverages the interaction with the living channel mentioned earlier. This is accomplished by multiplying the updates with the results of a MaxPool layer and a Boolean mask where the value is 1 if it exceeds 0.1 and 0 otherwise. 
 Figure 9: Single update step of the model
Figure above shows how deep learning is used to learn the set of rules that produce a desired multicellular pattern.

## Training procedure

![image](https://github.com/Aadityaza/3d-Growing-neural-cellular-automata/assets/45432533/c0786559-df1d-4444-9dfd-945953f264ea)

Figure : Training scheme for learning target pattern

Using a differentiable update rule, a set of rules can be found through numerical optimization techniques, such as gradient descent, to produce a desired multicellular pattern in 3D space. The approach employed in this work is reminiscent of the method outlined in the paper "Growing Neural Cellular Automata" [1], where the local rules are learned through reconstruction tasks. Similar to previous studies , the NCA (Neural Cellular Automata) endeavors to generate a target entity from a single living cell and optimize the reconstruction process using supervised learning and a reconstruction loss. Unlike th aproach in the paper _"Growing 3D Artefacts and Functional Machines with Neural Cellular Automata"_, the structure reconstruction task cannot be treated as a multiclass classification problem since there is no fixed number of classes to consider.
To compute the loss, the seed value is initialized and the loss function is determined using mean squared error (MSE). Specifically, the loss is calculated by computing the mean of the sum of the squared differences between the first 4 channels of the output and the target structure:

## Data

![image](https://github.com/Aadityaza/3d-Growing-neural-cellular-automata/assets/45432533/b25e534a-7e1a-4630-970f-4eb2f19f091d)

## Results



https://github.com/Aadityaza/3d-Growing-neural-cellular-automata/assets/45432533/ac7db461-b5ca-4b54-8836-807e83bf04ca



https://github.com/Aadityaza/3d-Growing-neural-cellular-automata/assets/45432533/1dd7ff5a-54f4-4db7-95b9-b6c50b7febca


https://github.com/Aadityaza/3d-Growing-neural-cellular-automata/assets/45432533/ecff6d91-7f0b-4b19-8400-afa847c8d680


https://github.com/Aadityaza/3d-Growing-neural-cellular-automata/assets/45432533/aa229426-49b0-4ee7-aa8e-84d8c889d324





## Regeneration



https://github.com/Aadityaza/3d-Growing-neural-cellular-automata/assets/45432533/426d64ba-6167-442a-9e19-db85ed4bd5f0


