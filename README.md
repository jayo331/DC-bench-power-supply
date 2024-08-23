# Multichannel linear bench power supply

Work in progress. At the start, i planned to add a switching pre-regulator and constant current control to an all-in-one linear regulator like lm350,lm317... The advantage of this solution is that since this regulator already comes with good line/load regulation i don't have to deal with extra stabilization. The problem is that those types of regulators also come with some big limits, some can not output voltages around zero, others can not handle the high current, and others are just too expensive for what they give, in general for all of the integrated solution voltage control (using DAC and MCU) is not as simple as i initially thought. Some regulators like 317 can be tweaked to output ~0V however the output is still limited to 1.5A in the case of the 317. I want to maintain the initial goals as much as possible (~0-25V, 5A per channel, simple) however commercial integrated linear regulators will not work without modifications. At this point, the only alternatives that come to mind are: 1) Tweak cheap regulators to reach voltages below 1.25V and boost the output current by adding an external pass transistor. 2) Build discretely a linear regulator that can handle these specs. For both solutions, extensive spice simulations are required to see which one performs better in dynamic load, transient, etc., and which one offers more performance at a price.

The regulators that i considered so far (without mod):

|                 | LM317         | LM350         | MIC29752      | LT3080        | LT3083        |
| --------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| 0V Capable      | &cross;       | &cross;       | &cross;       | &check;       | &check;       |
| 25V             | &check;       | &check;       | &check;       | &check;       | &cross;       |
| >/=5A           | &cross;       | &cross;       | &check;       | &cross;       | &cross;       |
| Active/In stock | &check;       | &check;       | &check;       | &check;       | &check;       |
| Cheap?          |Very inexpensive| Affordable   | Very expensive| Affordable    | Expensive     |
| Easy to mod?    | Easy          | Easy          | Difficult     | Very easy     | Easy          |

After some simulations, i ended up considering the discrete linear topology, which shows good results even in dynamic load. The main advantages of this solution are price and flexibility, also a good side effect is that since no mysterious pre-made ic are involved it should be easy to tweak in case of future updates.
