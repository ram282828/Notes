
**Power Curve Ice Detection (PCID)**

Each turbine has defined a reference power production for given weather conditions. The line emerging from this set of data points is named a Power Curve.

When turbine is operational, environmental condition are current power production is being checked. When ice appears on Turbine blades, power production drops. If power productions fall below configured threshold of reference power production for given conditions, ice detection is being raised.


An algorithm of comparing the reference power curve with current power production is named PCID.

The biggest advantage of PCID is, **that it doesn’t require any additional hardware**. All the ice detection is based on data collection and analysis.

The biggest disadvantage of PCID is, that it can detect ice only when operational. When Turbine is stationary, **it’s impossible to check if ice is still on the blades or not**.
