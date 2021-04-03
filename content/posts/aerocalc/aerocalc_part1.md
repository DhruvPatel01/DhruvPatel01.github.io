---
title: "AeroCalc Part 1: What is AeroCalc and how to use it?"
date: 2021-04-03T18:04:02+05:30
tags: ["science", "aero", "physics", "python", "ply", "yacc", "lex"]
---


I am a Computer Engineer by education and by training. Luckily, we computer engineers do not have to deal with different units. All our units are power of 2. We have sensible names, Kilo, Mega, Giga, you get it. When we get unlucky, there could be a confusion of whether Kilo in the context is $ 2^{10} $ or $ 10^3 $. But that is it.

But in other engineering (and science) branches this is not the case. A while ago I was taking a course "Introduction Aeronautical Engineering" on edX (the course is from TUDelft). Honestly, the homework problems there were annoying, at least for me. I can understand that students in the Aero department might need to practice the conversion process.

There is a `Newton`, which is also $\frac{kg * m}{s^2}$. There is an imperial unit for length called `foot`, but you __have to__ convert that into SI units to be compatible with other units in the formula, because the constants in the formula use `m`. Then there is `Celsius` to `Kelvin` mapping. You either have to memorize the conversion factors, or you have to make a long list of the conversion factors.

Something had to be done. And I was also looking for something to do on the weekends. So I am working on [AeroCalc](https://github.com/DhruvPatel01/AeroCalc/). Don't go on the name, I gave Aero prefix because my primary aim is to expedite solving homework problems in that course. But many parts of the app are general and should be usable outside Aerospace engineering. 

Rather than explaining what AeroCalc does, let me show you it in action.


{{<asciinema sYPyE91MGr9QOamVwnYThzlZN>}}

You might have noticed a few things. First there is a need for `*` between quantity and its unit. I designed it this way because it simplifies the grammar. Another thing is that units are not pluralized, e.g. it is `32000 foot` and not `32000 feet`. If you need your answer in SI units just use `expression in si`.


In the backend I am using an amazing Python library called [Astropy](https://www.astropy.org/) for conversion and [Ply](https://github.com/dabeaz/ply) for parsing. You can use all the units available in Astropy, the list can be found [here](https://docs.astropy.org/en/stable/units/).


You can also use math constants like `pi` and `e`. Internally AeroCalc looks for unresolved names in `math` library in Python. So if you haven't created a `pi` variable, `math.pi` will be used.

## Commands in AeroCalc
`del x`
: deletes the variable named `x` if defined. If not defined ignores the command.

`variables`
: lists all the variables defined in the current session.


## Problem Solving with AeroCalc

Let's try to solve one problem using AeroCalc. Below is one of the homework problems from the course.

```
An aircraft flies at an altitude of 30,000 feet. 
Determine the air temperature (in [K]), 
air pressure (in [Pa]) and air density (in [kg/m3]) 
at this altitude, according to the standard atmosphere.
```

Following are the variables given.
```
g = 9.80665 * m/s/s
T0 = 15*Celsius in Kelvin
P0 = 1013.25 * hectopascal
h = 30000 * foot in m
a = -6.5 * Kelvin/km
rho0 = 1.225 * kg/m^3
```

Notice that some variables are given in `m` whereas others are in `km`. A good thing about using AeroCalc is that generally you do not need to worry about this discrepancy. However you can always use `expr in si` to have unified values.

Since 30,000 foot is in troposphere, we can use $ T_1 = T_0 + a*h $ formula to compute the temperature at 32000 foot.

Once we know the temperature, we can use the following formula to compute the air density.

$$
    \frac{\rho_0}{\rho_1} = {\left( \frac{T_1}{T_0} \right)} ^{\frac{g}{R * a} - 1}
$$

There are few things about `^` operator in AeroCalc that you should keep in mind.
- In `a^b`, `b` has to be unit less. So expression like  `2^(3*m/(3*m))` is allowed, but `2^(3*m/3*m)` is not, as it simplifies to `2^(1*m^2)`.
- By default the units are not simplified, you might have to use `a^(b in si)` if units in b cancel out.
- `2^((3*m)/(300*cm))` will give you an error. Use `2^((3*m)/(300*cm) in si)` for now. I might fix this later.
- If `a` has units, `b` has to be like an integer. `b = 3.0` is allowed, but `b = 3.14` is not. So `(3*m)^2.0` evaluates to `9*m^2`.
- Finally, if `a` does not have units, any power is allowed.

In the above density formula, the exponent is actually unit less. So everything works out.

See the following recording for the whole solution.

{{<asciinema oTGxU3t8WOPyI6orh3W0TBMfh>}}


## What is next?
As far as blogging goes, I plan to write the details of how AeroCalc was implemented, the nitty gritty details of Lex and Yacc, in the next part. It is not that difficult really.

In the AeroCalc itself, I plan to add some features like having a database of formulas, and solving for a particular variables using other user defined variables.

GitHub repository for this project can be found [here](https://github.com/DhruvPatel01/AeroCalc/).