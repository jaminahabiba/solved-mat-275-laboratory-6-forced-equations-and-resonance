Download Link: https://assignmentchef.com/product/solved-mat-275-laboratory-6-forced-equations-and-resonance
<br>
In this laboratory we take a deeper look at second-order nonhomogeneous equations. We will concentrateon equations with a periodic harmonic forcing term. This will lead to a study of the phenomenon knownas resonance. The equation we consider has the formd2ydt2 + cdydt+ !20y = cos !t: (L6.1)This equation models the movement of a mass-spring system similar to the one described in Laboratory5. The forcing term on the right-hand side of (L6.1) models a vibration, with amplitude 1 and frequency! (in radians per second = 12&#x19; rotation per second = 602&#x19; rotations per minute, or RPM) of the plateholding the mass-spring system. All physical constants are assumed to be positive.Let !1 =√!20− c2=4. When c &lt; 2!0 the general solution of (L6.1) isy(t) = e−12 ct(c1 cos(!1t) + c2 sin(!1t)) + C cos (!t − &#xb;) (L6.2)withC =1 √(!20− !2)2 + c2!2; (L6.3)=arctan(c!!20−!2)if !0 &gt; !&#x19; + arctan(c!!20−!2)if !0 &lt; !(L6.4)and c1 and c2 determined by the initial conditions. The first term in (L6.2) represents the complementarysolution, that is, the general solution to the homogeneous equation (independent of !), while the secondterm represents a particular solution of the full ODE.Note that when c &gt; 0 the first term vanishes for large t due to the decreasing exponential factor.The solution then settles into a (forced) oscillation with amplitude C given by (L6.3). The objectives ofthis laboratory are then to understand1. the effect of the forcing term on the behavior of the solution for different values of !, in particularon the amplitude of the solution.2. the phenomena of resonance and beats in the absence of friction.The Amplitude of Forced OscillationsWe assume here that !0 = 2 and c = 1 are fixed. Initial conditions are set to 0. For each value of !, theamplitude C can be obtained numerically by taking half the difference between the highs and the lowsof the solution computed with a MATLAB ODE solver after a sufficiently large time, as follows: (notethat in the M-file below we set ! = 1:4).1 function LAB06ex12 omega0 = 2; c = 1; omega = 1.4;3 param = [omega0,c,omega];4 t0 = 0; y0 = 0; v0 = 0; Y0 = [y0;v0]; tf = 50;5 options = odeset(‘AbsTol’,1e-10,’RelTol’,1e-10);6 [t,Y] = ode45(@f,[t0,tf],Y0,options,param);7 y = Y(:,1); v = Y(:,2);8 figure(1)9 plot(t,y,’b-‘); ylabel(‘y’); grid on;c⃝2011 Stefania Tracogna, SoMSS, ASU 1MATLAB sessions: Laboratory 610 t1 = 25; i = find(t&gt;t1);11 C = (max(Y(i,1))-min(Y(i,1)))/2;12 disp([‘computed amplitude of forced oscillation = ‘ num2str(C)]);13 Ctheory = 1/sqrt((omega0^2-omega^2)^2+(c*omega)^2);14 disp([‘theoretical amplitude = ‘ num2str(Ctheory)]);15 %—————————————————————-16 function dYdt = f(t,Y,param)17 y = Y(1); v = Y(2);18 omega0 = param(1); c = param(2); omega = param(3);19 dYdt = [ v ; cos(omega*t)-omega0^2*y-c*v ];When executing this program we getcomputed amplitude of forced oscillation = 0.40417theoretical amplitude = 0.40417Lines 10-14 deserve some explanation. Line 10 defines a time t1 after which we think the contributionof the first term in (L6.2) has become negligible compared to the second term. This depends of courseon the parameter values, in particular c. With c = 1 we obtain e−12 ct ≃ 3:7 × 10−6 for t = 25, so thisis certainly small enough compared to the amplitude seen on Figure L6a. The index i of time valueslarger than t1 is then determined. The quantity Y(i,1) refers to the values of y associated to timeslarger than t1 only. The computed amplitude is simply half the difference between the max and the minvalues. This value is compared to the theoretical value (L6.3).0 10 20 30 40 50−0.5−0.4−0.3−0.2−0.100.10.20.30.40.5yFigure L6a: Forced oscillation.1. (a) What is the period of the forced oscillation? What is the numerical value (modulo 2&#x19;) of theangle &#xb; defined by (L6.4)?(b) In this question you are asked to modify the file LAB06ex1.m in order to plot the complementarysolution of (L6.1), that is, the first term in (L6.2). First define in the file the angle(alpha) using (L6.4), then evaluate the complementary solution yc by subtracting the quantityC cos(!t − &#xb;) from the numerical solution y. Plot the resulting quantity. Does it looklike an exponentially decreasing oscillation? Why or why not? Include the modified M-fileand the corresponding plot.2. We now consider C as a function of !. We use again !0 = 2, c = 1 and y(0) = y′(0) = 0. Theprevious problem determined C for a specific value of !. Here we consider a range of values for !c⃝2011 Stefania Tracogna, SoMSS, ASU 2MATLAB sessions: Laboratory 6and determine numerically the corresponding amplitude C. We then plot the result as a functionof !, together with the theoretical amplitude from (L6.3). You may need the following MATLABprogram.function LAB06ex2omega0 = 2; c = 1;OMEGA = 1:0.02:3;C = zeros(size(OMEGA));Ctheory = zeros(size(OMEGA));t0 = 0; y0 = 0; v0 = 0; Y0 = [y0;v0]; tf = 50; t1 = 25;for k = 1:length(OMEGA)omega = OMEGA(k);param = [omega0,c,omega];[t,Y] = ode45(@f,[t0,tf],Y0,[],param);i = find(t&gt;t1);C(k) = (max(Y(i,1))-min(Y(i,1)))/2;Ctheory(k) = ??; % FILL-INendfigure(2)plot(??); grid on; % FILL-INxlabel(‘omega’); ylabel(‘C’);%———————————————————function dYdt = f(t,Y,param)y = Y(1); v = Y(2);omega0 = param(1); c = param(2); omega = param(3);dYdt = [ v ; cos(omega*t)-omega0^2*y-c*v ];1 1.5 2 2.5 30.20.250.30.350.40.450.50.55wCFigure L6b: Amplitude as a function of !(a) Fill in the missing parts in the M-file LAB06ex2.m and execute it. You should get a figure likeFigure L6b. Include the modified M-file in your lab report.(b) Examine the graph obtained by running LAB06ex2.m and determine for what (approximate)value of ! the amplitude of the forced oscillation, C, is maximal. This value of ! is called thepractical resonance frequency. Give the corresponding maximum value of C.c⃝2011 Stefania Tracogna, SoMSS, ASU 3MATLAB sessions: Laboratory 6(c) Determine analytically the value of ! for which the amplitude of the forced oscillation, C, ismaximal by differentiating the expression for C in (L6.3) as a function of !. Compare thevalue you find with the value obtained in part (b).(d) Run LAB06ex1.m with the value of ! found in part (c) (include the graph). What is theamplitude of the forced oscillation? How does it compare with the amplitude of the forcedoscillation in problem 1.? If you run LAB06ex1.m with any other value of !, how do youexpect the amplitude of the solution to be?(e) Are the results affected by changes in the initial conditions? Answer this question both numerically(by modifying the initial conditions in LAB06ex2.m) and theoretically (by analyzingthe expression for C in (L6.3)). Note that the initial conditions for the DE are y0 and v0.ResonanceWe now investigate what happens to the solution (L6.2), and more specifically to the maximal amplitudeC of the forced oscillation, when we let c → 0. The value of ! corresponding to this maximal amplitude iscalled pure resonance frequency. When a mechanical system is stimulated by an external force operatingat this frequency the system is said to be resonant.3. Set c = 0 in LAB06ex2.m.1 1.5 2 2.5 302468101214wCcomputed numericallytheoretical(a) Explain what happens. What is the maximal amplitude? What is the value of ! yielding themaximal amplitude in the forced solution? How does this value compare to !0?(b) Run LAB06ex1.m with c = 0 and ! equal to the value found in part (a). Comment on thebehavior of the solution. Include the graph.BeatsWhen c = 0 and ! ̸= !0 , the solution (L6.2) to (L6.1) reduces toy(t) = c1 cos(!0t) + c2 sin(!0t) + C cos(!t − &#xb;)with C = 1|!20−!2| . If the initial conditions are set to zero, the solution reduces toy(t) = C(cos(!t) − cos(!0t))which can be rewritten asy(t) = 2C sin(12(!0 − !)t)sin(12(!0 + !)t):c⃝2011 Stefania Tracogna, SoMSS, ASU 4MATLAB sessions: Laboratory 6When ! is close to !0 we have that ! + !0 is large in comparison to |!0 − !|. Then sin( 12 (!0 + !)t)is a very rapidly varying function, whereas sin( 12 (!0 − !)t)is a slowly varying function. If we defineA(t) = 2C sin( 12 (!0 − !)t), then the solution can be written asy(t) = A(t) sin(12(!0 + !)t)and we may interpret it as a rapidly oscillating function with period T = 4&#x19;!0+! , but with a slowly varyingamplitude A(t). This is the phenomenon known as beats. Note that A(t) and −A(t) are the so-called“envelope functions”. The period of A(t) is 4&#x19;|!0−!| , thus the length of the beats is 2&#x19;|!0−!| .4. To see the beats phenomenon, set c = 0 and ! = 1:8 in LAB06ex1. Also extend the interval ofsimulation to 100.0 20 40 60 80 100−3−2−10123y(a) In LAB06ex1 define the “envelope” function A = 2C sin( 12 (!0 − !)t)with C = 1|!20−!2| .Plot A in red and −A in green, together with the solution. You should obtain Figure L6c.Include the modified M-file.0 20 40 60 80 100−3−2−10123yFigure L6c: Solution and envelope functionsc⃝2011 Stefania Tracogna, SoMSS, ASU 5MATLAB sessions: Laboratory 6(b) What is the period of the fast oscillation (that is, the period of sin( 12 (!0 + !)t))? Confirmyour answer by zooming in on the graph of the solution. Include a graph to support youranswer.(c) What is the length of the beats? Determine the length analytically using the envelope functions,and numerically from the graph.(d) Change the value of ! in LAB06ex1 to 1:9 (a value closer to !0) and then ! = 1:6 ( a valuefarther away from !0). Include the two graphs. For each of these two values of ! find theperiod of the fast oscillation and the length of the beats. How do the periods change comparedto parts (b) and (c)?(e) If you let ! = 0:5, is the beats phenomenon still present? Why or why not?c⃝2011 Stefania Tracogna, SoMSS, ASU 6