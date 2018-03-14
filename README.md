# model_proposal
Iris Rivera 
Course ID: CMPLXSYS 530,
Course Title: Computer Modeling of Complex Systems
Term: Winter, 2018

&nbsp;

# Goal 
Explore two different pattern distribution of two ants in a cellular automata model. Azteca ant which distribution is formed by dense- dependent forces, specifically by a parasitic fly and Wasmania ant which distribution is in mosaics (edge effect), and see how competition between the ants alters their spatial patter formation. 

&nbsp;

# Justification 
An ABM will allow me to ask specific questions about the mechanisms behind pattern formation and understand how multiple mechanisms interact when agents are antagonistic. I hope to gain insight by combing both of these models and adding competition to see how that alters the spatial patterning of both ants. 

&nbsp;

# Main Micro-level Processes and Macro-level Dynamics of Interest
To begin with the cellular automata model, the ants will appear randomly, each in one patch in the environment, which is going to finite. Each species will be of a different color to make it easy to identify. Once the two species are in the environment, each time step there will be a set probability of one ant spreading to one of its moore neighborhoods. If the picked cell is empty the ants will take that space and change its color. For Azteca, to simulate density dependent attack by parasitoids, the probability of a nest dying in a cluster will depend on the size of the cluster. For Wasmannia, there will be not density dependent dead. I will simulate competition by having one ant be able to take the place of the other. 

&nbsp;

# Environment
- Boundary conditions - finite environment 
- 2D
- Grid 'wrap around'
- list of environment -owned variables (e.g. resources, states, roughness)
  * The environment is going to be empty. 
  * Discrete space
  * Square lattice 
 
- List of environment-owned methods/procedures (e.g. resource production, state change, etc.)
 * In the environmnet one patch of azteca and one patch of wasmania will appear randomly.
 * pseudocode

__*LS COMMENTS:*__
*Good first pass with the pseudocode! Not too far away from what you'll need in order to implement in NetLogo. Next step is to start translating it into a runnable model ASAP to make sure you can get everything up and running in time to have something to present in April.*
 
 ```
patches-own [
  azteca-ant         ;; azteca patch  
  wasmania-ant       ;; wasmania patch 
  Azteca-dying       ;; dense dependent forces
  ]

;;;;;;;;;;;;;;;;;;;;;;;;
;;; Setup procedures ;;;
;;;;;;;;;;;;;;;;;;;;;;;;

to setup
  clear-all
  ask one-of patches [set pcolor cyan ]  ;; create one azteca patch
  ask one-of patches [set pclor sky] ;; create one wasmania patch
     reset-ticks
end

### LS COMMENTS ##

# If you are using the "azteca-ant" and "wasmania-ant" variables, you'll also want to make sure to set those variables as "True" or 
# "False" as appropriate during setup.

;;;;;;;;;;;;;;;;;;;;;
;;; Go procedures ;;;
;;;;;;;;;;;;;;;;;;;;;

to go

 setup- patch  interactions ;; create azteca and wasmania patch procedures
[
  [
  ask patches ;;azteca patch
  if random neighbord cell is empy, occupy and change it to aztecas color
  when azteca patch reaches 10 cells, randomly pick one to die];; dense- dependent forces

## LS COMMENTS ##
# Key thing to think through here is how you will tell NetLogo to determine the size of a given cluster. This can be a little bit  
# trickier than expected. Relatedly, you'll need to think about what "counts" as an azteca cluster. For instance, would you want 10 
# azteca patches all in a row to qualify?

[
ask patches ;; wasmania patch
if random neighbor cell is empty, occupy and change it to wasmanias color
]

[ask patches;; competition
  if patch find a empty cell of the other patch, occupy that space
]
]

## LS COMMENTS ##
# I might be a bit confused here. Can an Azteca patch be empty? I had assumed an Azteca patch was the same as it being occupied Azteca 
# ant. Or does that indicate it *used* to be occupied by an Azteca? If so, you'll need a way to distinguish between occupied vs. non-
# occupied along with which ant type a patch is.

```
# Agents 
 * The model is going to have patches, one for the ant azteca and one for the ant wasmania. 
 * Each patch (Azteca and Wasmania) is going to have its own procedures. 
 * Once the two ants are in the environment each time step there will be a set probability of one ant spreading to a patch with in its moore neighborhood.
 * If the space is empty the ant will take it and change it to its color. 
 * For Azteca, to simulate density dependent attack by parasitoids, the probability of a nest dying in a cluster will depend on the size of the cluster, for example when the cluster reaches 10 cells one cell will die randomly.
  * For Wasmannia, there will be not density dependent dead. Wasmania population will grow until enconter azteca in the environment. 
  * Competition will be simulated by having one ant able to take the pleace of the other ant.
  
  * pseudocode in the environment section

# Action and Interaction 
  * Interaction topology, in the moore neighborhood the two ants ( wasmania and Azteca) will interact trough competition. The stronger competitior will take the position of the weak competitor. 
  
&nbsp;

__*LS COMMENTS:*__
*How will ant strength be indicated in the competition? Will individual ants be stronger or weaker, or is this a species-level thing that can be set with a global parameter?*
 
  * Action sequence 
  * step one : We are going to randomly place azteca and wasmania in the environment. Each ant with different color.
  * step two : Each time step there is a probabiity that azteca is going to move to one of the patches in its moore neighborhood. If wasmania is there azteca can not occupy that patch. 
  * Step three: Each time step there is a probability that wasmania is going to move to one of the patches in its moore neighborhood. If azteca is there wasmania can occupy that patch base on the strenght of competition between azteca and wasmania. 
  * Step four : Calculate the cluster size of azteca. 
  * pseudoce in the environment section  
    
# Model Parameters and Initialization
  - Global parameters: Competition coeficient, probability of extinction, area occupy by azteca, area accupy by wasmania.
   * Competition coeficinet, strenght of the interaction. This is going to be a slider from 0 to 1 which will represent the probability of an ant occupying the other ant patch.
   * Probability of azteca extintion wich will be base on the size of the cluster. This is going to be a slider where we can select the maximum number of cells until a patch of azteca can grow before start picking one cell randomly to die.
   - Describe how your model will be initialized
   * Each time step we can set up the competition coefition of each ant which can be 0 or 1. 
   * Each time step we can set up the probability of azteca extinction which will range from 1 to 10. 

__*LS COMMENTS*__
*In general, global parameters are usually set at the beginning of a simulation run and are not updated in subsequent turns. Allowing for these exogenously set, global parameters to vary in the middle of runs would make analysis extremely complicated.*

*Also, if competition coefficient is not universal between species but instead a property of individual ants, you'll want to change that from a global parameter (i.e. variable) into a patch or turtle-owned variable.*

# Assessment and Outcome Measures
What quantitative metrics and/or qualitative features will you use to assess your model outcomes?
* Taking into account the model parameters such as competition coefitient and probability of extinction, the model is going to measure the area occupy by azteca and wasmania. 

# Parameter Sweep
 I am interested in looking at how pattern distributions of these two ants is modify by competition. Whit the model I will explore how azteca pattern formation which is formed by density depenndent factors and also limited by competition with wasmania.
 
 &nbsp;
 
 __*LS COMMENTS*__
 *It looks like your main parameters that you will need to explore different values of are competition coefficient, extinction probability, and probability of spread on a given turn. Also, since space is so important to this model, I would suggest considering looking at some variants where you use a Von Neumann neighborhood and turn off wrapping.
