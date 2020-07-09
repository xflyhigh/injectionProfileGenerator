# injectionProfileGenerator
Injection Profile was caculated by the empirical model.

> Thanks for the help of Yan Zhang. His blog:  https://openfoam.top/

> Thanks for the help of Shijie Xu. His blog:  https://openfoam.tech/

---
## ------------Related articles----------------
Xu L, Bai X S, Jia M, et al. Experimental and modeling study of liquid fuel injection and combustion in diesel engines with a common rail injection system[J]. Applied Energy, 2018, 230: 287-304.
DOI: 10.1016/j.apenergy.2018.08.104
https://www.sciencedirect.com/science/article/pii/S0306261918312741


## ------------parameters required  in this model----------------
```C++
Pinj	        800e+5; // injection  pressure bar
umbreangle      120.0; // spray umbrella angel. For the constant volume vessel the umbrella is 0.0;
```
### A sample of the injetionModels.model1
```C++
    injectionModels
    {
        model1
        {
            type            coneInjection;
            SOI             -28.0;
            massTotal       3.73242E-06;//7.89815E-06;//4.208e-6;
            parcelBasisType mass;
	        nParticle	    10;
            injectionMethod disc;
            flowType        constantVelocity;
			Umag            #include "$FOAM_CASE/constant/injetionParameter/velocity";
            Pinj	        800e+5;
            dOuter   230e-6;
            dInner    0;
            duration        #include "$FOAM_CASE/constant/injetionParameter/duration";
	        position        (0.000 0.002 0.0084);
	        direction       (0.000 0.002 -0.0011547);
		    umbreangle   120.0;
            parcelsPerSecond	#include "$FOAM_CASE/constant/injetionParameter/parcelsPerSecond";
            flowRateProfile  #include "$FOAM_CASE/constant/injetionParameter/flowRateProfile";
            Cd              0.8;//#include "$FOAM_CASE/constant/injetionParameter/discd";//0.8;
            thetaInner      constant 0.0;
            thetaOuter      constant 10.0;

            sizeDistribution
            {
                type        RosinRammler;

                RosinRammlerDistribution
                {
                    minValue        #include "$FOAM_CASE/constant/injetionParameter/minValue";
                    maxValue        #include "$FOAM_CASE/constant/injetionParameter/maxValue";
                    d               #include "$FOAM_CASE/constant/injetionParameter/meanValue";
                    n               3;
                }
            }
        }
    }
```
## ------------Use this model----------------
Run the solver in your case folder:injectionProfileGenerator

After that a folder named "injetionParameter" will be created in the folder of "constant". 

Four files are in this folder:

"Duration":injection duration 

"flowRateProfile":

"velocity": parcels initial velocity 

"discd": the discharge coefficient

## ------------Peport the bug----------------
If you have any question, you can send the email to: xflyhigh@qq.com.



