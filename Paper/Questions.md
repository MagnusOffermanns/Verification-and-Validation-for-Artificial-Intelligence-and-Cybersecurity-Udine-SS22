# Formulas and variables
$\theta_+$ and $\theta_-$  are thresholds.
	corresponds to a concentration of the corresponding protein above $\theta_+$ , while the value false corresponds to the concentration being below $\theta_-$

what is $\delta$ and $\lambda$ 
	- $\delta$ is the is the maximum response time of a circuit
	- $\lambda$ is the minimum duration of the output signal

# 1 Introduction
 - [x] What is synthetic biology?
- [x] What is de-novo synthesis and not new synthesis
- [x] Why should we divide systems in subunits?
- [x]  What is the difference between a top-down and a bottom up approach
- [ ]  What is a genetic regulatory circuit
- [ ] What are logic gates?
- [x] What is the idea of this paper?
- [x] Which logic is used
- [x] What are the contributions of this paper?
- [ ] What is parameter synthesis?

# 2 Background
## Modeling of regulatory networks
- What is a gene regulatory network?
- What are lumped models of gene expression?
- Why can it be modeled ba a ODE -> What ODE solvers can we use to solve the ODEs
- What is a regulatory mechanism of a gene
- What is a Michaelis-Menten function
- What is a oderhil function?
## Signal temporal Logic
- What is a [STL](Signal%20Temporal%20Logic.md)
- Why was [STL](Signal%20Temporal%20Logic.md) used in this paper?
- What two forms of [STL](Signal%20Temporal%20Logic.md) are there?
	- Boolean Form
	- Quantitative form
- Where is it successfully used for modelling?

# 3 Logical Characterisation of Modules
-  What is the approach for the synthesis of Biological circuits?
- What are modules the basic building blocks for building a genetic network?
- What is a genetic network?
- What are transcription factors
- Waht are activators?
- What are repressors?
- Why is the temporal dimension more relevant when building logical gates in systems biology
- What outputs do biological modules create apart from a boolean response?
- What is the relevance of concentrations?
- What are external transcription factors?
- What are produced proteins
- What is the relatinship and role of the transcription factors and the produced proteins in the [STL](Signal%20Temporal%20Logic.md) Formula?
## Example Logic Gates
- What is the gene expression?
- What is a gene promoter?
- What is a complex in the context of synthetic biology
- How is true and false defined with concentrations
### And gate
- What is the maximum response time $\delta$ and the minimum duration $\lambda$ 
- What is a zero basal expression rate?
- What is a hill activation function
- What is the difference between the normal hill function and the product of a hill function
- How are and or and not gates actually biologically implemented.

### XOR Gate
- what is $\delta$ and $\lambda$ 
	- $\delta$ is the is the maximum response time of a circuit
	- $\lambda$ is the minimum duration of the output signal
- how can we build a XOR gate from and, or and not gates
- what is a karnaugh map
- What do we need to define to go from circuit to STL
- What is the target temporal behavior & how do we constraint the temporal behavior
- how do we calculate minimum response time and minimum duration

## Constraints for arbitrary acyclic networks of logic gates
- what makes a acyclic network arbitrary and acyclic
- [x] Why does he not care for cyclic logic networks?
- How can we calculate the minimum response time and minimum duration for common circuits
- How can we calculate the the minimum response time and minimum duration for arbitrary acyclic networks.
- How can we represent this in an STL formula
- What does remark 1 mean.
## Parameter Synthesis
- What is parameter synthesis
- How does the paper satisfy constraints on a local level?
- What does the satisfaction of local constraints to do with that.
- What parameters are defined?
- Why define a set of values?
- How can we optimize it
- How does it go into pratice for instance using biobricks?
- How can this constraints be calculated and with which software? (Breach)
- What is the advantage of looking at gates individually

## Modularity of parameter synthesis for logic gates
- Why does the connection of modules in a network make the modelling with STL complicated?
- What is a worst case analysis.
- Why do we choose a worst case analysis?
- How can the worst case in STL be defined?
- What is a quantitative satisfaction score?
- What is the monotonicity of the Hill function? 
- What is monotonicity

## Remark 2
- why does the worst case analysis rely on the monotonicity of the robustness score with respect to the input signa?
- what is the translation constant $k_t$
- what is the degradation constant $k_d$


# The algorithm
## Sketch of the algorithm
- What are the necessary steps to calculate the parameters?
- For which parts of the network do we apply the algorithm (for each module, for each row of the truth table)
- Why do we do a intersection of the parameter space?
- What is the sensitivity based algorithm that is implemented in breach?
- Why can we calcualte a analytical result for the AND OR and NOT gates?

## Example Half-adder
- How do we calculate the maximum time delay of 4 units and the maximum response time of 12 units?
- Why do we rescale the proteins between \[0 and 1 \]?
- what is the maximum steady state expression level of a protein
- Where do all the variables for the calculation come from
- How do we need to adapt this example to fit into real life?
# Discussion
- What is the problem with non interfering output proteins
- how can the work be extened?
	- more complex modules
	- Feedback loops?
- How can you look at the parameter synthesis as fix point calculation
- How can we take the stochastizity into account?

#  Related work
- How do synthetic biological circuits implemented? Why is it computationally intensive?
- What are existin approaches?
- What do Marchisio and stelling do
- How is the problem of signal compatibility solved in 31?
- How do Batt et al. \[2\] approximate the behavior of genetic regulatory networks?
- How does 25 study the timing behavior of acyclic circuits?
