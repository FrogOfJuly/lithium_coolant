# Adjustable RTG

The primary issue with polonium design is that it is impossible to turn it off or adjust its thermal output. 

The only way to be adjustable is to be a nuclear reactor. Unfortunately, they are even bulkier, require at least some infrastructure, and have many moving parts. 

Below I will describe a borderline design between a reactor and an RTG. 

The idea is to replace the polonide heat source with fissile plutonium and a neutron source. Neutron source could be moderated and this permits variability in output power. 

The method of power generation stays the same, while heat production changes. 

This idea exists in real life as a [subcritical reactor](https://en.wikipedia.org/wiki/Subcritical_reactor) design. However, it uses particle accelerators to supply neutrons.


## Plutonium fission

There are different isotopes of plutonium and some of them are better than others. The typical fission fuel is $^{239}\text{Pu}$, its [half-life](https://en.wikipedia.org/wiki/Plutonium-239) is around $24.1$ *thousand years* compared with $^{238}\text{Pu}$ which is typically used in RTGs with its [half-life](https://en.wikipedia.org/wiki/Plutonium-238) of $87$ years. Below the plutonium is assumed to be of the fissile variety.


First, let's consider its thermal output. It is an alpha emitter and the energy of an alpha particle is $5.156 \text{ MeV}$. Which [amounts](https://www.sciencedirect.com/topics/pharmacology-toxicology-and-pharmaceutical-science/plutonium-239) to decay heat of $1.9 \cdot 10^{-3} \frac{W}{g}$. To provide some reference, decay heat of $^{238}\text{Pu}$ is $0.57 \frac{W}{g}$. So, for sure, fissile plutonium isotope is unfit for an RTG and it seems safe to disregard its decay heat.

However, if this isotope fissions it is a whole other story. This [handy table](https://en.wikipedia.org/wiki/Plutonium-239#Nuclear_properties) provides much-needed information about thermal energies carried by different components of the fission reaction. If one excludes $\gamma$ emission, antineutrinos, and $\beta$-particles, the resulting energy per fission event would be as follows.

$$
E\_{\text{fission}} = 193.2 \text{ MeV} = 309.5 \cdot 10^{-13} \text{ J}
$$

Thus, if one wants to supply a single kilowatt of power the following number of fission events must take place per second.

$$
\text{rate\_of\_fission} = \frac{10^3 \frac{J}{s}}{309.5 \cdot 10^{-13} \text{ J} \cdot 1 \text{ kW}} = 82.9 \cdot 10^{12}\ \frac{1}{s \cdot \text{kW}}
$$

The fission probability of the capture event is $f = 73\%$. Otherwise, neutron is captured and $^{240}\text{Pu}$ is created alongside $\gamma$ emission. 

The decay chain goes further into the [abyss](https://periodictable.com/Isotopes/094.239/index.html) of nuclear waste, which is too hard to analyze. Thermal emission of those decay elements is accounted for in the fission energy value; however, precise radiation composition is hard to determine. This would surely need shielding. Also, in case of rapture, it will be very hard to decontaminate. 

With known molar mass it is possible to compute how much pure plutonium must be consumed per kilowatt of thermal power.

$$
m_{\text{fuel}} = \frac{1}{f} \cdot \frac{\text{rate\_of\_fission}}{N_A} \cdot \mu_{\text{Pu}} = 3275.18 \cdot 10^{-11} \frac{\text{g}}{s \cdot \text{kW}} = 105.2\ \frac{\text{g}}{\text{year} \cdot \text{kW}}
$$


This is a very effective fuel. However, it is hard to isolate pure fissile isotope and it is [never](https://en.wikipedia.org/wiki/Neutron_poison) possible to burn all the fuel.

The calculations above assume that the fuel captures neutrons and undergoes fission. If this process is able to sustain itself then it is [critical](https://en.wikipedia.org/wiki/Critical_mass). For a reactor, it is the desired state, but for a compact power source that is deployed in a combat environment, it is a very fragile state of affairs. One must carefully adjust the components of the system to ensure that no mechanical impact will derail the power supply into a shutdown or supercritical state. 

## Criticality

Here is a nice [entry point](https://www.nuclear-power.com/nuclear-power/reactor-physics/nuclear-fission-chain-reaction/six-factor-formula-effective-multiplication-factor/) to the rabbit hole of reactor criticality.

The bottom line is that not all neutrons participate in fission, part escapes, part is captured without fusion, part fails to [slow down](https://en.wikipedia.org/wiki/Neutron_moderator) to thermal energies, and so on. The ratio between generations is defined by [effective neutron multiplication factor](https://en.wikipedia.org/wiki/Nuclear_chain_reaction#Effective_neutron_multiplication_factor), $k$ and it is the most important value in the whole process. Its relation to one determines the criticality of the reactor. 

These neutron generations could be accounted for by scaling the initial neutron population by a sum of an infinite geometric series.

$$
n = n_0 \cdot \underset{i = 0}{\overset{\infty}{\Sigma}}\ k^i = \frac{n_0}{1 - k}
$$

The problem is that to even estimate the $k$ one needs to do a complex modeling for a chosen reactor configuration. This is quite extensive for any worldbuilding application.

However, [this paper](https://www.tandfonline.com/doi/pdf/10.1080/00223131.2000.10874904) provides a value that is considered "safe" for a storage configuration: $k^{\text{max}} = 0.95$. 

$$
\text{scale}_{\text{ k}} = \frac{1}{1 - k} \implies \text{scale}_{\text{ k}}^{\text{max}} = 20
$$


## Neutron source

This design aims to be perpetually subcritical, thus it needs an external [neutron source](https://en.wikipedia.org/wiki/Neutron_source).

### Polonium

The first thing to consider is that $^{210}\text{Po}$ in tandem with $\text{Be}$ could be used as a neutron source. Its specific activity is $166 \cdot 10^{12} \frac{\text{Bq}}{g}$. Today it is very doubtful that all this activity can be harvested as alpha particles are very easily absorbed by matter. The main advantage of polonium is that it could be [bread](https://hal.science/hal-04196973/file/Report%20210.pdf) out of stable elements with little effort. The required layered structure which will allow beryllium to effectively absorb a big fraction of alpha particles is surely outside of the "little effort" zone.

However, let's assume the best case to analyze how good $\text{PoBe}$ neutron source could be. The reference value for alpha-particle-to-neutron conversion ratio for $\text{Be}$ [is]((https://en.wikipedia.org/wiki/Neutron_source)) $3\cdot 10^{-5} \frac{\text{n}}{\alpha}$, so in the best case neutron emission will be as follows.


$$
\text{neutron\_emission\_rate} = 4.98 \cdot 10^9\ \frac{\text{Bq}}{\text{g}^{\text{Po}}}
$$


The overall mass to sustain the required amount of fission events in plutonium per kilowatt is as follows.


$$
m_\text{\text{ source}} = \frac{1}{f} \cdot \frac{\text{rate\_of\_fission}}{\text{neutron\_emission\_rate}} = \frac{1}{0.73} \cdot \frac{82.9}{4.98} \cdot 10^3 = 16.65 \cdot 10^3\ \frac{\text{g}^{\text{Po}}}{\text{kW}}
$$

This is too much, as only $m_\text{\text{ decay}} \approx 100\text{g}$ of $\text{Po}$ is needed to supply the required kilowatt of thermal power just by decay. In order to match the thermal energy of $\text{Po}$ decay by $\text{Po}$ neutron source. The neutron multiplication factor should be as follows.

$$
\frac{1}{\text{scale}_{\text{ k}}} \cdot m_\text{\text{ source}} = m_\text{\text{ decay}} \iff k = 1 - \frac{m_\text{ decay}}{m_\text{\text{ source}}} = 1 - \frac{100}{16.64 \cdot 10^3} = 0.994 > k^{\text{max}}
$$

This does not comply with the safety threshold. Thus, polonium neutron source is out.


### Californium

A very compact and strong neutron source that is used today is [californium](https://en.wikipedia.org/wiki/Californium), more precisely  $^{252}\text{Cf}$. It is a synthetic element and it does not occur in nature. The half-life of this isotope is $2.645 \text{ years}$, which is about seven times longer than one of polonium.

It is hard to make, but even today it is [possible](https://www.sciencedirect.com/science/article/abs/pii/S0969804300002141) to produce it as a byproduct in fission reactors.

It does not need a complex beryllium setup and just emits $2.314 \cdot 10^6 \frac{\text{neutron}}{\mu\text{g} \cdot \text{s}}$. 

$$
m_\text{\text{ source}} = \frac{1}{f} \cdot \frac{\text{rate\_of\_fission}}{\text{neutron\_emission\_rate}} = \frac{1}{0.73} \cdot \frac{82.9}{2.314} = 35.82\ \frac{\text{g}^{\text{Cf}}}{\text{kW}}
$$


Assuming all neutrons are consumed for the first generation to produce a kilowatt of thermal power one needs the following amount of californium. After scaling this thing by a neutron multiplication factor, the desired californium amount is as follows.

$$
m_\text{\text{ source}} = 1.79\ \frac{\text{g}^{\text{Cf}}}{\text{kW}}
$$

Which is a satisfactory number. 

However, as californium rapidly decays it [emits](https://inis.iaea.org/collection/NCLCollectionStore/_Public/01/001/1001697.pdf) $39 \frac{W}{g}$ of heat.

$$
W_{\text{source}} = 1.79 \cdot 39 = 69.8 \frac{W}{\text{kW}} \approx 7\%
$$


## Power armour configuration


Shielding is a must for this setup, plutonium emits many nasty things while it fissions. Also cleanup would be substantially more troublesome than in the case of polonium. It is not pure alpha emitter, but rather a fully fledged nuclear waste. 

The existence of neutrons permits moderator usage to slow neutrons down or discard them into the shielding. This means that the only thing that needs to be cooled down perpetually is decaying californium. 

$$
W_{exo} = 5kW
$$

The effectiveness value for $\text{LiH}$ coolant is as follows.

$$
\eta\_{\text{LiH}}^{\text{all}} = 11.73 \\%
$$

Thus at full and minimal utilisations the heat powers will be as follows. 

$$
W^{\text{thermal}}_{\text{exo active}} = 42.6 \text{kW}
$$

$$
W^{\text{thermal}}_{\text{exo stored}} = 2.98 \text{kW}
$$

The respected coolant losses per day are as follows.


$$
m^{\text{stored}}_{\text{loss}} = 1.67 \cdot 2.98 = 4.98 \ \frac{\text{kg}}{\text{day}}
$$

$$
m^{\text{active}}_{\text{loss}} = 73.21\ \frac{\text{kg}}{\text{day}} 
$$

The component masses.

$$
M_{\text{Cf}} = 8.95 \text{ gram}
$$

$$
M_{\text{Pu}} = 0.526\ \frac{\text{g}}{\text{yaer}}
$$

$$
M_{\text{moderator}} = \text{???}
$$

$$
M_{\text{shielding}} = \text{???}
$$


## Conclusion


While maximum coolant usage stays the same this setup provides tools to change the thermal output of the power source. This can dramatically increase the efficiency of coolant usage as, depending on the amount of action it could be as low as 7% of its maximum loss. 

There are severe drawbacks to this approach compared with the polonium setup.

* Rapture events are truly catastrophic now
* Cleanup is very hard
* Moderator is a moving part
* Shielding is an obligation


There are ways to improve this analysis. 

* Plutonium fuel after fission would emit significant heat from fission products, so shelf heat would be somewhat bigger.
* Moderator or fuel would need to be replaced occasionally as poison elements build up.
* Shielding mass and moderator mass need to be calculated severalty, but it is unlikely they are a significant fraction of coolant weight.


Here are some more depictions of power that I find compelling.












































