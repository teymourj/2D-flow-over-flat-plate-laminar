# CFD Problem's Physics & Theory

**In developing CFD simulation for a fluid mechanic problem understanding the general physics and fundamental theory of the problem is extremely important. This knowledge would provide users the ability to make logical decision about the geometry of CFD domain, choice of proper boundary conditions and numerical models for the CFD simulation. Furthermore, user will have a general big picture on the expected outcome of simulation. These knowledges and abilities form the foundation for a successful implementation and validation of the CFD simulation.**

**In other words understanding physics and theory of problem before developing a CFD simulation can be thought of turning on a flash light before taking any step in a completely dark room. Hence, let's review the fundamental physics and theory behind the problem of "2D Laminar Flow in over a Flat Plate." as the first step for development and validation of CFD simulation for this problem of interest:**

Figure 1 visualizes the physics of a uniform and steady flow passing over a solid flat plate. Upon the start of interaction between the fluid and solid plate, fluid elements right on top of the plate will brought to stop due to the "no slip" boundary condition (point "a"). As the flow moves further downstream the plate, static fluid elements decelerate the motion of their neighboring fluid elements due to the viscous effect within the flow field. The result of these fluid-solid and viscous interactions is the formation of a layer close to the fluid-solid common boundary called "boundary layer".

<img src="./Images/fig.9.1.png" width="500">
</br>
Fig.1 - Schematic of uniform and steady flow passing over a flat plate and forming the boundary layer region.

The thickness of this layer increases further downstream the plate. The maximum thickness **&delta;** is defined as a vertical distance above which the velocity will recover to above 90% the free stream velocity. One of the classical definitions of the maximum boundary layer thickness is as follows:

<img src="./Images/lex-smits-9.0.png" width="200">

According to the flow regime (i.e. Reynolds number value) the boundary layer is categorized as either "Laminar" or "Turbulent". In both of these categorizes the flow field behavior inside the boundary layer region is complex and not possible to be modeled analytically. Hence, experimental and computational techniques are needed to fully analyze and understand the flow field and viscous forces behavior inside the boundary layer. In the section below it will show how purely analytical model reach a dead-end and experimental and numerical techniques come into play.

Application of the Control Volume (CV) analysis approach to the control volume ** abcd ** shown in figure 1 provides a general functionality between the velocity field and viscous forces in the 2D laminar flow over a flat plate: General form of conservation of mass states:

<img src="./Images/mass_cons_general.png" width="250">

Since the flow is steady and incompressible the first term in the above equation becomes zero and expansion of the  second term, mass flux integral term, in the above equation on four control surfaces of the CV provides:

<img src="./Images/lex-smits-9.1.0.png" width="500">

where  **n<sub>1**, **n<sub>2** and **n<sub>3** are normal unit vectors pointing out from surfaces **ab**, **cd** and **bc** respectively. Performing the dot product between unit normal and velocity vectors to define the mass flux direction and considering a unit depth **W** for the flat plate, based on the 2D assumption, the above equation will be reduced to:

<img src="./Images/lex-smits-9.1.png" width="200">

where **U<sub>e** is the undisturbed free stream velocity, **u** is the disturbed streamwise velocity and **v** are the normal velocity components of the flow. In this equation both **u=u(y)** and **v=v(x)** are unknowns (i.e. one equation versus two unknowns). To obtain a second equation on can consider the conservation of momentum in streamwise direction. The general form of conservation of momentum equation states:

<img src="./Images/momentum_cons_general.png" width="500">

Assuming that there is no external force exerted on the CV, neglecting body forces and steady floe terms one, four and five, from right, in the above equation will be equal to zero respectively. Furthermore, due to having a uniform flow entering the CV one can conclude the pressure would be constant in the streamwise direction. Additionally assuming that growth of the boundary layer thickness is slow and overall small the pressure variation in the normal direction can also estimated to be almost constant. Application of these assumptions will zero out the third term in the above equation. At this stage expanding the momentum flux integral term, sixth term in the above equation, on four control surfaces of the CV states:

<img src="./Images/lex-smits-9.2.0.png" width="500">

Similar to the equation of mass conservation in the equation **n<sub>1**, **n<sub>2** and **n<sub>3** are normal unit vectors pointing out from surfaces **ab**, **cd** and **bc** respectively. Performing the dot product between normal and velocity vectors to define the momentum flux direction and considering a unit depth **W** for the flat plate, based the 2D assumption, and the fact that the flow in incompressible the above equation is reduced to:

<img src="./Images/lex-smits-9.2.1.png" width="300">

At this stage introduction of conservation of momentum equation added an additional unknown **F<sub>v** into the existing number of unknowns (two equations versus three unknowns)! Multiplying the simplified version of conservation of mass equation by **U<sub>e** and subtracting the resultant equation from conservation of momentum equation would result into elimination of the integral term including the **v** component of the velocity field:

<img src="./Images/lex-smits-9.2.2.png" width="500">

further simplification states:

<img src="./Images/lex-smits-9.2.3.png" width="350">

This equation still includes two unknowns **F<sub>v** and **u**, however these are the overall viscous forces and velocity in the boundary layer region which were the original variables of interest. As mentioned earlier due to the inherent complexity of the flow field inside the boundary layer region analytical method reaches a dead-end here. Introducing the conservation of energy equation would add more variables into the system of equations and would not simplify the current equations. In 1904 Ludwig Prandtl showed that for the flow in a boundary layer, it is possible to make some approximations to the full Navier-Stokes equation using the above-mentioned assumption used in the CV analysis of this flow field. The approximations are based on the observation that a boundary layer grows slowly, and therefore the streamlines within the layer are nearly parallel. In particular, the pressure across the layer is then nearly constant. Application of these assumptions to the full Navier-Stokes equation resulted in an equation named later on "boundary layer equation":

<img src="./Images/lex-smits-9.3.png" width="200">

Later Paul Blasius, one of Prandtl’s students, showed that the boundary layer equation has a “similarity” solution (i.e. a universal solution). Using dimensional analysis and experimental techniques, he first proposed that the normalized velocity distribution is only a function of the freestream velocity **U<sub>e**, the density **&rho;**, the viscosity **&nu;**, the distance from the wall **y**, and the distance along the plate x:

<img src="./Images/lex-smits-9.3.1.png" width="200">

Furthermore Blasius then showed that, instead of depending on two dimensionless variables, the normalized velocity distribution is a function of only one composite dimensionless variable **&eta;** , such that:

<img src="./Images/lex-smits-9.4.png" width="100"> where  <img src="./Images/lex-smits-9.4.1.png" width="100">

It should be highlighted that this is a purely experimental not an analytical approximation. The variables **u/U<sub>e;** and **&eta;** are called similarity variables, which means that if the velocity distribution is plotted using these non-dimensional variables, instead of dimensional variables such as **u** and **y**, it is defined by a universal curve, for **any** Reynolds number and **any** position along the plate. This solution is shown in the following figure:

<img src="./Images/fig.9.2.png" width="500">
</br>
Fig.2 - Blasius velocity approximation plotted via similarity variables.

These two particular similarity variables would transform the boundary layer equation (a PDE) into an ODE which can be then solved numerically. The solution is called the Blasius velocity profile.

At this stage the Blausius approximation for the disturbed velocity **u/U<sub>e;** can be inserted in the final form of the conservation of the momentum equation and value of overall or local viscous forces, exerted by the fluid on the flat plate, can be evaluated. Later on for validation purposes the similarity variables, boundary layer thickness variation and the drag (friction) coefficient values of this flow field will be plotted and compared against Blausius approximation that are as follow:

<img src="./Images/lex-smits-9.14.png" width="300">

With this review one has developed an in-depth understanding of the flow and approximate the expected results from the CFD simulations. Now one can move forward to initiate developing the CFD domain and simulations for this problem of interest.

> For more details on the physics, theory and equation derivation please see chapter 9, section 9.2 of "A Physical Introduction to Fluid Mechanics by Alexander J. Smits" 2nd edition. [Download Book Here!](http://www.efluids.com/efluids/books/efluids_books.htm)