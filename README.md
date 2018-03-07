# model_proposal
Iris Rivera 
Course ID: CMPLXSYS 530,
Course Title: Computer Modeling of Complex Systems
Term: Winter, 2018
# Goal 
Explore two different pattern distribution of two ants in a cellular automata model. Azteca ant which distribution is formed by dense- dependent forces, specifically by a parasitic fly and Wasmania ant which distribution is in mosaics (edge effect), and see how competition between the ants alters their spatial patter formation. 
# Justification 
An ABM will allow me to ask specific questions about the mechanisms behind pattern formation and understand how multiple mechanisms interact when agents are antagonistic. I hope to gain insight by combing both of these models and adding competition to see how that alters the spatial patterning of both ants. 
# Main Micro-level Processes and Macro-level Dynamics of Interest
To begin with the cellular automata model, the ants will appear randomly, each in one patch in the environment, which is going to finite. Each species will be of a different color to make it easy to identify. Once the two species are in the environment, each time step there will be a set probability of one ant spreading to one of its moore neighborhoods. If the picked cell is empty the ants will take that space and change its color. For Azteca, to simulate density dependent attack by parasitoids, the probability of a nest dying in a cluster will depend on the size of the cluster. For Wasmannia, there will be not density dependent dead. I will simulate competition by having one ant be able to take the place of the other. 
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

[
ask patches ;; wasmania patch
if random neighbor cell is empty, occupy and change it to wasmanias color
]

[ask patches;; competition
  if patch find a empty cell of the other patch, occupy that space
]
]

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
  
# Assessment and Outcome Measures
What quantitative metrics and/or qualitative features will you use to assess your model outcomes?
* Taking into account the model parameters such as competition coefitient and probability of extinction, the model is going to measure the area occupy by azteca and wasmania. 

# Parameter Sweep
 I am interested in looking at how pattern distributions of these two ants is modify by competition. Whit the model I will explore how azteca pattern formation which is formed by density depenndent factors and also limited by competition with wasmania. 
