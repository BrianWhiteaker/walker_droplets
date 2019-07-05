# Walker Droplets
The following is an ongoing project whose goal is to predict the "chaotic" trajectories of oil walker droplets<br>
in a circular corral.  These droplets are described as hydrodynamic quantum analogs. Some strange behaviors observed<br> 
which are fun to look at are [here](https://www.youtube.com/watch?v=-2yYgfaU6Ik) and [here](https://www.youtube.com/watch?v=MP-NZ5EoTm4).<br>

### What are walker droplets?
The walker droplets are created using a fluid such as silicon oil in a corral, placed on a vibration table. The table
vibrates at around 60 HZ vertically.  When a pointed object such as a toothpick is dipped into the oil a droplet will
fall off, and if the timing is right, will fall into a trough and begin bouncing on a cushion of air without coalescing
into the bath. The droplet can range from 0.5-1.5mm in diameter. In various experiments the droplet can continue propogation
for days. A key point is to keep the vibration below the Faraday threshold of the corral, thereby creating standing waves
which interfere with the trajectories. If this limit is maintained the droplets will explore the corral/bath with "chaotic" 
trajectories.  It is true that the statistics of these trajectories mimic the statistics of a particle in a quantum corral.

### Why do they travel?
The droplets begin to propogate when the frequency of forcing nears the Faraday threshold of the corral.  At this point the
waves created from previous bounces interact with newer waves.  These waves reflect off of the corral and interact with
constructive and destructive interference so that the droplet will hit the surface at different angles to move it in some
direction.  These waves will dissipate due to viscosity after a few seconds.  In this time these waves are imposing a memory
of previous bounces and so the droplet is in a sense interacting with this memory carried by the medium. This effect has been
viewed as a macroscopic analog of how a de Broglie-Bohm Pilot Wave Theory may behave.  

### Caveat
Firstly, I am no physicist but an interested enthusiast and this presents me with an intersting and fun machine learning task!

Secondly, it should be noted that some issues have arisen around the experiments of Couder and Fort. In particular issues
revolve around the double slit experiment performed with walker droplets. It may be that these issues will be resolved in a 
future experiment. For the time being we still see the quantum tunneling, orbit quantization, gravitation, spin lattices, and 
cooper pair analog behavior. Beyond the walker experiments, there have been some interesting experiments with fluid analogs of
[Unruh radiation](https://journals.aps.org/pra/abstract/10.1103/PhysRevA.98.022118) and [sonic black holes](https://www.quantamagazine.org/philosophers-debate-new-sonic-black-hole-discovery-20190625/).  

### Motivation
I am personally interested in de Broglie-Bohm Mechanics as a quantum interpretation.  I became interested in machine learning
and data science because of a fascination with math and systems that self-organize. Underlying this is a belief that as humans
we are limited by our perception of the world, experiences, and creativity.  So my thought is that the pure logic of machine
learning given data might provide a way to move beyond the bounds of logic, and allow a purely logical system to organize
towards solutions we have not considered- similar to AlphaGo's invention of never-seen-before strategies in Go. A great 
example is how Biomimetics draws inspiration for engineering from nature. Organisms in nature arise as solutions to the best
way to use energy available in some system.  No imagination required. I should say the imagination will go into how to build 
the needed model.

### The Model
As I have accumulated knowledge I realized that CNN's paired with RNN's would be a great way to approach this problem. The
CNN would be used to learn features of an image frame taken in sequence from video footage of a droplet propogating
in a circular corral. These features would be spatial local structure relationships of waves interacting captured in an image. 
These features could then be passed in time-sequential order to the RNN. Here the RNN would learn temporal structure from 
feature set to feature set in time.

More specifically, a CAE is trained with the encoder and decoder attached together. Once trained, they are separated
and an LSTM is inserted between them. This three part network is then trained as a whole. The encoder breaks each image
into useful filters, the LSTM learns the sequence of filters, and the decoder reconstructs an image. For the LSTM, increasing 
context lengths are used to a maximum of 15. Truncated backpropogation through time is used on the unrolled sequence of 
forward passes for a given context length. 

Making predictions with the trained model is similar to character sequence generation, where a seed character is given to the 
model. A prediction of the next character is returned by said model, and this is passed back into the network in order to 
generate the following prediciton.

At a later date I found [this](https://www.quantamagazine.org/machine-learnings-amazing-ability-to-predict-chaos-20180418/) 
article describing work at MIT and U of Maryland in predicting flame fronts or propogating differential equations. They used 
Reservoir Computing or LSTM's for the task.

Hopefully I will be as successful.

### Work to follow
1) GRU recurrent layer comparison.
2) Construct a Reservoir Computing network.
3) Work in the direction of NN's and DE governing equations.

