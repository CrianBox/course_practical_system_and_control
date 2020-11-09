# Regeltechniek
Regeltechniek omvat hoofdzakelijk de volgende onderwerpen:
* regelaarontwerp
* inzicht van systeemtheorie gebruiken
* inzicht van de performantiecriteria voor het gesloten lus gedrag gebruiken
* verschillende ontwerpmethodes 

## Basis

### Voorwaardse koppeling (feedforward)



### Achterwaardse koppeling (feedback)


### Weerstand tegen storing
Storing kunnen zowel ruis als externe krachten zijn. 

![Model van een voeding \cite{Control system design guide book}](images/powersupply_model.jpg)

$$\frac{U_F(s)}{I_{LOAD}(s)} = \frac{1/Cs}{1+(1/Cs) (1+K_I/s) K_P LPF(s)}$$  

In het mid-frequent domein is de weerstand tegen storing het slechtste.

![Transferfunctie van verstoringsignaal \cite{Control system design guide book}](images/disturbance_rejection.jpg)
![Invloed van parametervariatie op het verstoringssignaal \cite{Control system design guide book}](images/disturbance_rejection_illustration.jpg)

## PID architecturen

## Dode tijd compensatie 

### Smith predictor

![output Smith predictor](images/output_and_control_action_matlab.jpg)

## Anti-aliasing
## Integrator anti-windup
## Derivative filtering
## Digital implementation
## Energie-verbruik
## Prefiltering
## Notch filtering