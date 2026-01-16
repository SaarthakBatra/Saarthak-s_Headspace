[📁 Explore](obsidian://open?vault=5aabe01b2a639311&file=📁%20Explore) > [Mechanical Engineering](obsidian://open?vault=5aabe01b2a639311&file=Mechanical%20Engineering) > [Manufacturing Management](obsidian://open?vault=5aabe01b2a639311&file=Manufacturing%20Management) > [Planning Facilities](obsidian://open?vault=5aabe01b2a639311&file=Planning%20Facilities) > [[Product Layouts]] > Line Balancing

---

![[Basic Layouts-Line Balancing.png#align-right|400]]
- The process of equalizing the amount of work at each workstation
- Assembly-line balancing operates under two constraints:
	1. **Precedence requirements:** 
	   Specifying which operations must precede others, and which must wait until later, are an important input to the product layout decision.
	2. **Cycle time restrictions:** 
	   Maximum amount of time the product is allowed to spend at each work station
### Desired Cycle Time
$$C_d=\frac{Production\ Time\ Available}{Desired\ Units\ of\ Output}$$
### Efficiency
$$E=\frac{\sum_{i=1}^j t_i}{nC_a}$$
### Theoretical Minimum Number of Workstations
$$N=\frac{\sum_{i=1}^j t_i}{C_d}$$
where,
	$t_i$ = completion time for element i
	$j$ = total number of work elements
	$n$ = actual number of workstations
	$C_a$ = actual cycle time
	$C_d$ = desired cycle time

### Procedure
1. Draw and label a precedence diagram
2. Calculate the desired cycle time required for the line
3. Calculate the theoretical minimum number of workstations
4. Group elements into workstations, recognizing cycle time and precedence constraints
5. Calculate the efficiency of the line
6. Determine if the theoretical minimum number of workstations or an acceptable efficiency level has been reached otherwise go back to step 4

### Algorithms
1. Largest Operation Time
	- Assignment of work elements to stations based on largest amount of time each work element requires 
2. Kilbridge and Wester Method
	- Assignment of work elements to stations based on position in the precedence diagram
	- Elements at front of diagram are assigned first 
3. Ranked Positional Weights
	- Combines the two preceding approaches by calculating an RPW for each element

### Examples
#### Q1
Real Fruit Snack Strips are made from a mixture of dried fruit, food coloring, preservatives and glucose. The mixture is pressed out into a thin sheet, imprinted with various shapes, rolled, and packaged. The precedence and time requirements for each step in the assembly process are given below. 
$$
\begin{array}{|c|c|c|c|}
\hline
\text{Process}	&\text{Work Element}			&\text{Precedence} & \text{Time (min)} \\
\hline
\text{A} 		&\text{Press out sheet of fruit}&-	 				& 0.1 \\
\text{B} 		&\text{Cut into strips}			&A	 				& 0.2 \\
\text{C} 		&\text{Outline fun shapes}		&A					& 0.4 \\
\text{D} 		&\text{Roll up and package}		&B,C	 			& 0.3 \\
\hline
\end{array}
$$
To meet demand, Real Fruit needs to produce 6000 fruit strips every 40-hour week. Design an assembly line with the fewest number of workstations that will achieve the production quota without violating precedence constraints.

##### ans.
1. Draw Precedence Diagram and add time requirements beside each node
	![[Basic Layouts-Precedense Diagram.png#align-right|Precedence Diagram for data|200]]
2. Calculate the desired cycle time and the theoretical minimum number of workstations
	$$C_d = \frac{40hrs\times60min/hrs}{6000units}=0.4 min$$
	$$N = \frac{0.1+0.2+0.3+0.4}{0.4}=2.5\approx3\ workstations$$
![[Basic Layouts-Grouped Elemnts.png#align-right||Workstation assignments|200]]
- To balance the line, we must group elements into workstations so that the sum of the element times at each workstation is less than or equal to the desired cycle time of 0.4 minute. 
- Examining the precedence diagram, we begin with A since it is the only element that does not have a precedence.
- We assign A to workstation 1. B and C are now available for assignment.
- Cycle time is exceeded with A and C in the same workstation, so we assign B to workstation 1 and place C in a second workstation. 
- No other element can be added to workstation 2, due to cycle time constraints. 
- That leaves D for assignment to a third workstation. Elements grouped into workstations are circled on the precedence diagram and placed into workstations shown on the assembly line diagram.
![[Basic Layouts-Assemply line diagram.png#align-right|Assembly Line Diagram|300]]
$$
\begin{array}{|c|c|c|c|}
\hline
\text{Workstation}	&\text{Element}	&\text{Remaining Time}	& \text{Remaining Elements} \\
\hline
\text{1} 			&\text{A}		&0.3	 				& B, C 						\\
\text{} 			&\text{B}		&0.1	 				& C,D 						\\
\text{2} 			&\text{C}		&0.0					& D 						\\
\text{3} 			&\text{D}		&0.1	 				& none 						\\
\hline
\end{array}
$$
- Since the theoretical minimum number of workstations was three, we know we have balanced the line as efficiently as possible. 
- The assembly line has an efficiency of
	$$E=\frac{0.1+0.2+0.3+0.4}{3\times0.4}=83.3\%$$

#### Q2
The Mach 10 is a one-person sailboat manufactured by Creative Leisure. The final assembly plant is in Victoria, British Columbia. The assembly area is available for production of the Mach 10 for 200 minutes per day. (The rest of the time it is busy making other products.) The daily demand is 60 boats. Given the following information,
1. Draw the precedence diagram and assign tasks using five workstations.
2. What is the efficiency of the assembly line, using your answer to part (a)?
3. What is the _theoretical_ minimum number of workstations?
4. What is the idle time per boat produced?
$$
\begin{array}{|c|c|c|}
\hline
\text{Task}	&\text{Precedence}	&\text{Performance Time (min)} \\
\hline
\text{A} 	&-					&1	 							\\
\text{B} 	&A					&1	 							\\
\text{C} 	&A					&2								\\
\text{D} 	&C					&1	 							\\
\text{E} 	&C					&3	 							\\
\text{F} 	&C					&1	 							\\
\text{G} 	&D,E,F				&1	 							\\
\text{H} 	&B					&2	 							\\
\text{I} 	&G,H				&1	 							\\
\hline
\end{array}
$$
##### ans.
1. Draw Precedence Diagram and add time requirements beside each node
	![[Basic Layouts-Precedence Diagram.png#align-right|Precedence Diagram for data|300]]
2. Calculate the desired cycle time and the theoretical minimum number of workstations
	$$C_d = \frac{200\ min/day}{60\ boats/day}=3.33\ min/boat$$
	$$N = \frac{1+1+2+1+3+1+1+2+1}{3.33}=3.9\approx4\ workstations$$
![[Basic Layouts-Workstation Assignment.png#align-right|Workstation Assignments|400]]
- To balance the line, we must group elements into workstations so that the sum of the element times at each workstation is less than or equal to the desired cycle time of 3.33 minute. 
- Examining the precedence diagram, we begin with A since it is the only element that does not have a precedence.
- We assign A to workstation 1. B and C are now available for assignment. After completion we have the final as shown
- We are unable to achieve our theoretical minimum workstations

$$
\begin{array}{|c|c|c|c|}
\hline
\text{Workstation}	&\text{Element}	&\text{Remaining Time}	& \text{Remaining Elements} \\
\hline
\text{1} 			&\text{A}		&	 				&  						\\
\text{} 			&\text{C}		&	 				& 						\\
\text{2} 			&\text{B}		&					& 						\\
\text{} 			&\text{D}		&	 				&  						\\
\text{3} 			&\text{E}		&	 				&  						\\
\text{4} 			&\text{F}		&	 				&  						\\
\text{} 			&\text{G}		&	 				&  						\\
\text{5} 			&\text{H}		&	 				&  						\\
\text{} 			&\text{I}		&	 				&  						\\
\hline
\end{array}
$$
- Since the theoretical minimum number of workstations was three, we know we have balanced the line as efficiently as possible. 
- The assembly line has an efficiency of
	$$E_{th}=\frac{\text{Total Task Time}}{\text{n(stations)}\times\text
	{Cycle Time}}=\frac{13\ min}{5\times3.33}=78\%$$
	$$E_{actual}=\frac{\text{Total Task Time}}{\text{n(stations)}\times\text
	{Max. Station Time}}=\frac{13\ min}{5\times3}=86.7\%$$


#### Q3
1. 12 work hours/day and 90 units/day needed
$$
\begin{array}{|c|c|c|}
\hline
\text{Task}	&\text{Precedence}	&\text{Performance Time (min)} \\
\hline
\text{A} 	&-					&3	 							\\
\text{B} 	&-					&3	 							\\
\text{C} 	&-					&4								\\
\text{D} 	&A					&3	 							\\
\text{E} 	&D					&5	 							\\
\text{F} 	&B,E				&2	 							\\
\text{G} 	&B,C,E				&6	 							\\
\text{H} 	&F					&4	 							\\
\text{I} 	&G					&4	 							\\
\text{J} 	&H,I				&2	 							\\
\hline
\end{array}
$$
##### ans.
1. Draw Precedence Diagram and add time requirements beside each node
	
2. Calculate the desired cycle time and the theoretical minimum number of workstations
	$$C_d = \frac{12\times60\ min/day}{90\ units/day}=8\ min/unit$$
	$$N = \frac{3+3+4+3+5+2+6+4+4+2}{8}=4.5\approx5\ workstations$$
![[Basic Layouts-Workstation Assignment.png#align-right|Workstation Assignments|400]]
- To balance the line, we must group elements into workstations so that the sum of the element times at each workstation is less than or equal to the desired cycle time of 3.33 minute. 
- Examining the precedence diagram, we begin with A since it is the only element that does not have a precedence.
- We assign A to workstation 1. B and C are now available for assignment. After completion we have the final as shown
- We are unable to achieve our theoretical minimum workstations

$$
\begin{array}{|c|c|c|c|}
\hline
\text{Workstation}	&\text{Eligible tasks}	&\text{Assigned}	& \text{Task time} & \text{Total time}& \text{Idle time} \\
\hline
\text{1}	&\text{A, B, C}	&\text{C}	&4	&4	&4	\\
\text{}		&\text{A, B}	&\text{A}	&3	&7	&1	\\
\text{2}	&\text{B, D}	&\text{B}	&3	&3	&5	\\
\text{}		&\text{D}		&\text{D}	&3	&6	&2	\\
\text{3}	&\text{E}		&\text{E}	&5	&5	&3	\\
\text{}		&\text{F}		&\text{F}	&2	&7	&1	\\
\text{4}	&\text{G, H}	&\text{G}	&6	&6	&2	\\
\text{5}	&\text{H, I}	&\text{H}	&4	&4	&4	\\
\text{5}	&\text{I}		&\text{I}	&4	&8	&0	\\
\text{2 (or 4)}	&\text{J}	&\text{J}	&2	&8	&0	\\
\hline
\end{array}
$$
- Since the theoretical minimum number of workstations was three, we know we have balanced the line as efficiently as possible. 
- The assembly line has an efficiency of
	$$E_{th}=\frac{\text{Total Task Time}}{\text{n(stations)}\times\text
	{Cycle Time}}=\frac{13\ min}{5\times3.33}=78\%$$
	$$E_{actual}=\frac{\text{Total Task Time}}{\text{n(stations)}\times\text
	{Max. Station Time}}=\frac{13\ min}{5\times3}=86.7\%$$

