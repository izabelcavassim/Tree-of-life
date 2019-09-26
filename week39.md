---
title: "Simulation Wright-Fisher model with R"
author: "Maria Izabel"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## Exercise goals

In the following exercise you will:

1.  **Learn** the assumptions of Wright-Fisher and Coalescence Model.
2.  **Simulate** different scenarios using the different models.
3.  **Understand** the concept and effects of genetic drift and effective population size in the different scenarios.

## Introduction to population genetics
A lot of population genetics theory is focused on describing the changes of allele frequencies through time. Once we understand how and why the frequencies of alleles change, we have learned a great portion of evolution.

There are two most important factors that cause allele frequencies to change through time: 
**natural selection** and **genetic drift**.
**Genetic drift** is the **random change of allele frequencies** in populations of finite sizes. Genetic drift occurs because more or less copies of an allele by chance can be transmitted to the next generation. This can occur because by chance the individuals carrying a particular allele can leave more or less offspring in the next generation. In a sexual diploid population genetic drift also occurs because Mendelian transmission means that only one of the two alleles in an individual, chosen at random at a locus, is transmitted to the offspring.

Genetic drift can play a role in the dynamics of all alleles and populations, but it will play the biggest role for neutral alleles. A neutral polymorphism occurs when the segregating alleles at a polymorphic site have no discernible differences in their effect on fitness. And because has no effect on fitness, natural selection is not truly orchestrating those changes.

For now (Chapter 2 and 3) we will only focus our attention on the effect of genetic drift on shaping allele frequencies. But later in this course you will see that we can include selection into the models.

Population geneticists have developed a number of different models to describe genetic drift. The most common model is the **Wright-Fisher** model. And is built based in multiple assumptions that will be discussed below. 

During the 1980s mathematicians and biologists used part of the concepts of **Wright-Fisher** model and developed the **Coalescence theory**, which could be readly used and applied for real data.

The differences between two models are quite simple: while Wright-Fisher models changes of allele frequencies forward in time, the coalescence theory considers a sample and the genealogical history of the sample, in other words: backwards in time.

Just to test you knowledge I first ask you too questions:

1. What are the assumptions of Wright-Fisher model? What is the distributions used for modelling allele frequencies?

```{r, echo = F}
#The discrete-time wright-fisher model follows a binomial distribution (success and failures).
#Assumptions: constant pop size, randomly mating, no selection, no migration, non-overlaping generations.

#Frequencies of alleles are changed due to genetic drift, and its intensity will depend on the effective population size. Under a very small population the fluctuations of allele frequencies will be much more drastic.
#Assuming no mutation all alleles will reach fixation or get extinct. 

#page 
```

2. In a sample of two gene copies taken from a population, what is the distribution and expectation of the time until the two copies find a most recent common ancestor?

```{r, echo = F}
#geometric distribution, probability = 1/2n, expected coalescence time is 2 for a population of size 2N, page 242 of the small book

```

## Exercises using the Wright-Fisher model
(based on scripts by Graham Coop and Fernando Racimo)

Download the R script simulateWF.R from this github repository into a folder in your computer, then cd into that folder and start running the R console:

```{r}
setwd("/Users/PM/Dropbox/PHD/POPGEN_SUMMERCOURSE/")
source("simulateWF.R") # sourcing the functions of the code
```

This script contains a set of functions for simulating the Wright-Fisher model, both forwards and backwards in time. We'll play with these functions to gain some intuition about how the models work.

## 1 - Thinking forwards in time: 2 alleles

### Wright-Fisher model

First, we'll run a Wright-Fisher model beginning with a population with two alleles. The population will have size 2N = 10 (so N = 5 diploid individuals) and we'll run the simulation for 15 generations:

```{r}
WF_twoalleles(5,15)
```

3. What do you observe plotted on the screen?


```{r, echo = F}
# changes from allele blue to allele red occurs from one generation to another, from left to right
#4 times red got fixed.
#3 times blue got fixed.
#3 times both co-existed.
#On average it will continue to be 0.5.


```

a) Run this line 10 times, and record how many times the red allele fixes, how many times the blue allele fixes and how many times the population remains polymorphic (both the blue and the red allele still co-exist). Compare your results with your neighbor. Does there seem to be a preference for whether the blue or red allele fixes? Why do you think this is so? Hint: check the frequency of the two alleles at the beginning of the simulation.

You may have noticed that a vector of values also gets printed into the console every time we run this simulation. This is the allele counts of the blue allele. We can use this vector to trace the frequency of the blue allele over time:

```{r}
bluecounts <- WF_twoalleles(5,15)
bluefreq <- bluecounts / (2 * 5)
plot(bluefreq,ylim=c(0,1),type="b",col="blue",pch=19,xlab="generations",ylab="Blue frequency")
```

b) Repeat exercise a) but with N=3 and N=10. Do alleles tend to "fix" faster when N is large or when N is small?

```{r, echo=FALSE}
par(mfrow=c(2,2))
bluecounts <- WF_twoalleles(3,15)
bluefreq <- bluecounts / (2 * 3)
plot(bluefreq,ylim=c(0,1),type="b",col="blue",pch=19,xlab="generations",ylab="Blue frequency (3)")

bluecounts <- WF_twoalleles(10,15)
bluefreq <- bluecounts / (2 * 10)
plot(bluefreq,ylim=c(0,1),type="b",col="blue",pch=19,xlab="generations",ylab="Blue frequency (10)")

dev.off()

#Alleles fix faster when N is smaller, due to the fact that random genetic drift has a stronger influence in the fluctuations. 
```


## 2 - Thinking forwards in time: many alleles

We can also run a Wright-Fisher model with more than two alleles. The function below begins with a population in which each individual contains two distinct alleles, which are different from all other alleles in the population.

```{r}
WF_manyalleles(5,15)
```

a) What happens to the allelic diversity (number of alleles present) as time goes forward? Are there more or less heterozygotes at the end of the simulation than at the beginning?


```{r, echo =F}
#The allelic diversity decrease over generations, there is less heterozygostes than in the beginning. 
```

b) Check what happens to allelic diversity over time, when N = 3 and when N = 10.


```{r, echo =F}
#The allelic diversity decrease slower in a bigger population.
```

```{r, echo =F}
par(mfrow=c(2,1))
bluecounts <- WF_manyalleles(3,15)

bluecounts <- WF_manyalleles(10,15)
dev.off()
```


### Coalescence model


## 3 - Thinking backwards in time

So far, we've been running the Wright-Fisher model forwards in time. We began with a population of individuals with (possibly) distinct alleles and observed what happened as we approached the present. Now, we'll start in the present and go backwards in time. Specifically, we'll aim to trace the lineages of particular individuals that exist in the present and see how they "coalesce" (find a common ancestor) in the past.

a) We will trace the genealogy of 3 lineages in a population of size N = 10 (2N = 20) over 20 generations:

```{r}
track_lineages(N.vec=rep(10,20), n.iter=1, num.tracked=3)
```

Repeat this simulation 10 times. For each simulation, record the time between the present and the first coalescent event, and the time between the first coalescent event and the second coalescent event (i.e. the most recent common ancestor of all 3 lineages). You can ignore simulations where lineages have not coalesced at generation 20. Which of the two times tends to be larger? Why do you think this is?

```{r, echo =F}
#The time that tends to be larger is the time to the most recent common ancestor of all 3 lineages.
#This is due to the fact that coalescence times follow an exponential distribution, implying that more recent coalescence times are more likely, although the rate at which the coalescence event happens (given that it has not already happened) is constant in time. 
#Exponential random variables are continuous random variables, and the mean of the exponential random variable is 1/lambda. 
```


b) Check what happens to the coalescence rate, when N = 7 and when N = 20. Do lineages coalesce faster or slower with larger population size?

```{r, echo =F}
# When the effective population size is smaller the lineages coalesce faster. 
```


## Exercise	A:	Simulating	a	coalescence	tree	assuming	a	constant	population	size

The	purpose	of	this first	exercise	is	to	make	sure	it	is	clear	how	a	coalescence tree	is	simulated. We will use R so a little familiarity with this language will help. First, let	us try to	simulate	a	coalescence tree	for	five gene	copies by	hand:

1. Start	by	drawing	a	node	for	each	of	the	five	gene	copies on	an	invisible line	(with	space	for	drawing	a	tree	above them).	Name	these	nodes 1,2,3,4,5

2. Also,	make	a	list	of	the	node	names.	You	can	either	do	this	by	hand	or	you	can	do	it	in	R	by	
simply	writing:

```{r}
nodes = c(1,2,3,4,5) # make the list and call it nodes
nodes # print the list
```

3. Sample	which	two	nodes	will	coalesce	first	(going	back	in	time)	by	randomly	picking	two	of	the	
nodes.	You	can	either	do	this	by	hand	or	you	can	do	it	in	R	by	typing:

```{r}
nodecount = length(nodes) # save the number of nodes in the variable nodecount
tocoalesce = sample(1:nodecount, size=2) # sample 2 different nodes in node list
nodes[tocoalesce[1]] # print the first node sampled
nodes[tocoalesce[2]] # print the second node sampled
```

If	you	used	R	then	make	sure	you	understand	what	the	R	code	does	before	moving	on.

4. Sample	the	time	it	takes	before	these	two	nodes	coalesce	(measured	from	previous	
coalescence	event in	units	of	2N)	by	sampling	from	an	exponential	distribution	with	rate	equal	
to	nodecount*(nodecount-1)/2	where	nodecount	is	the	number	of	nodes	in	your node	list.	Do	
this	in	R	by	typing:

```{r}
coalescencerate = nodecount*(nodecount-1)/2 # calculate the coalescent rate
coalescencetime = rexp(1, rate=coalescencerate) # sample from exponential w. that rate
coalescencetime
```

Make sure	you	understand	what	the	R	code	does	before	moving	on.

5. Now	draw	a	node	that	is	the	sampled amount	of	time	further	up	in	the	tree	than	the currently	highest node	(so	if	the	currently	highest	node	is	drawn	at	height	T	then	draw	the	new	one	at height	T plus the	sampled	coalescence	time)	and	draw	a	branch	from	each	of	the	nodes	you	
sampled	in	step	3	to	this	new	node	indicating	that	these	two	nodes	coalesce at	this	time.	

```{r}
nodecount = nodecount-2
coalescencerate = nodecount*(nodecount-1)/2 # calculate the coalescent rate
coalescencetime = rexp(1, rate=coalescencerate+coalescencetime) # sample from exponential w. that rate
coalescencetime
```


6. Next,	make	an	updated	list	of	the	nodes	that	are	left	by	removing	the two	nodes	that	
coalesced	and	instead	adding	the	newly	drawn	node	that represents	their	common	ancestor.	
You	can	call	the	new	node	the	next	number	not	used	as	a	name	yet	(e.g. if	this	is	the	first	
coalescence event you	can	call	it	6, if	it	is	the	second	coalescence	event you	can	call	it	7	etc.).	
You	can	either	do	this	by	hand	or	in	R.	If	you	want	to	do	it	R	you	can	do	it	as	follows:

```{r}
nodes <- nodes[-tocoalesce] # remove the two nodes that coalesced
nodes <- c(nodes,2*5-length(nodes)-1) # add the new node
nodes # print the new list
```

If	you	used	R	then	make	sure	you	understand	what	the	R	code	does	before	moving	on.

7. If	you	only	have	one	node	left	in	your	list	of	remaining	nodes	you	are	done.	If	not,	go	back	to	
step	3.	

In	the	end you	should	have	a	tree,	which	is	a	simulation	of	a	coalescence	tree J Try	to	do	this	a	couple times	until	you	feel	like	you	know	how	it	is	done	and	understand	what	is	going	on	(if	you	after	a	drawing	a	few	trees still	don't	understand	then	feel	free	to	ask for	help!)

## Exercise	B:	Exploring	the	basic	properties	of	a	standard	coalescence tree	

Doing	this	by	hand	is	obviously a	bit	tedious.	So	based	on	the	R	code	snippets	you	already	got, we have built a function	that	allows	you	to	do	this	automatically	(it	even	makes	a	drawing	of	the	tree).	You	
can	use	it from the course server	by	typing the	following	in	R:

```{r}
source("/Users/PM/Dropbox/PHD/POPGEN_SUMMERCOURSE/simulatecoalescencetrees.R")
```

Once	you	have	done	this	you can	simulate	and	draw	trees just like	you	just	did	by hand by	typing the code below, which will print out ten trees on the screen:

```{r, eval =F}
par(mfrow=c(2,5))
for(i in c(1:10)){
         print("New Tree")
         yourtree <-simtree(5) # simulate tree with 5 nodes
         ct<-read.tree(text=yourtree);plot(ct,cex=1.5);add.scale.bar(y=1.2,x=0.2,cex = 2,col = "red",lcol="red",lwd=3)
         print(" ")
}

```

You should see several trees printed out in the screen. If this doesn't happen, try downloading the R script from this github website, and then running it locally in your machine (after you cd to the folder in which you downloaded the script).

```{r, eval = F}
library("ape")
```

Note that the code also	prints the	simulated	coalescence	times.	

Based	on the results you get answer the following questions:

1) Which	coalescence event takes	the	longest on	average (the	first coalescence event,	the	
second,	third, or the last)? And	which	event	takes	the	shortest on	average?

```{r, echo = F}
#The last coalescence event take the longest on average to happen.
```

2) Is	that	what	you	would	expect? Recall that the	mean	of	an	exponential	distribution	with rate	lambda	is	1/lambda and	the	coalescence rate	when	there	are	n nodes	left	is	n(n-1)/2.	So	the	mean is 2/(n(n-1)),	so for	instance	for	when	there	are	5	nodes	left	the	mean	coalescent	time is	2/(5(5-1))=0.1

```{r, eval=F, eval =F}
for(n in c(1:5)){
  print(n)
  mean_coalesnce_time = 2/(n*(n-1))
  print(mean_coalesnce_time)
}
```

3) Which	coalescence event	time	seems to	vary	the	most?

```{r, echo = F}
#The last coalescence events, the smaller the rate the higher the variance.
```

4) Is	that	what	you	would	expect? Recall that the	variance	of	an	exponential	is	1/(lambda^2).

