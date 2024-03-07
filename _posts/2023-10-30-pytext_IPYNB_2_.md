---
toc: True
comments: True
layout: post
title: Personal Project - Asteroid Generator
description: SpaceEngine script generator using Python with numpy, pandas, and scipy
type: hacks
courses: {'csp': {'week': 10, 'categories': ['4.A']}}
categories: ['C1.4']
---

```python
import numpy as np
import pandas as pd
from scipy.stats import halfnorm
from scipy.stats import skewnorm
```

<p>This work-in-progress code is an experiment in writing data to a text file with Python. I was trying to generate a few thousand asteroids in the planetarium program SpaceEngine for a lesson in my personal astronomy class. The reason for this relatively complex code is to ensure that asteroid distributions are accurate to reality while allowing each asteroid to be scripted properly. However, it was not completed before the end of T1.</p>

<p>The script format we need to generate is:</p>
<p>[Object_Type] "Object Name"</p>
<p>{</p>
<p>ParentBody "Parent Body Name"</p>
<p>Class "Object Class"</p>
<p>Mass [Object Mass]</p>
<p>Orbit</p>
<p>{</p>
<p>PeriodDays [Period of orbit in days]</p>
<p>SemiMajorAxisKm [Semimajor Axis in km]</p>
<p>Eccentricity [Eccentricity of the orbit]</p>
<p>Inclination [Inclination of the orbit]</p>
<p>}</p>
<p>}</p>


```python
def gen_asteroids(txtname, base_data):

  #Needed functionality
  #Some objects are replaced by asteroid families with shared orbital parameters, spread is controlled by a time-variant parameter
  #Objects in a main-belt population avoid unstable resonances
  #Objects have pi < 1 so they do not clear their orbits
  #Belts/minor moons do not approach major planets/moons within specified limits
  #eccentricity and inclination occupy normal distributions around specified centres

  obj_dict = {"mass":[], "parent":[], "sma":[], "period":[], "e":[], "i":[]}

  for index, row in base_data.iterrows():
      n_present = 0
      #Count number of objects created to date
      
      while n_present < row["num"]:
        group_attempt = np.random.uniform(0,1)

        #Generating asteroid families (Multiple related objects) if probability is exceeded
        if group_attempt < row["groupfrac"]:
          group_num = skewnorm.rvs() #WIP - Add skew normal distribution of group sizes
          i = 0
          while i < group_num:
            #WIP - Verify every asteroid in the group using mode and sma_gen
            n_present += 1

        #Generate ONE asteroid
        else:
          
          #Randomly draw samples from various scipy data distributions (half normal, skewed) with the passed parameters
          e_instance = halfnorm.rvs(loc=row['e_center'], scale=row['e_rad'], size=1)[0]
          i_instance = np.random.normal(row['i_center'], row['i_rad'])
          mass_instance = skewnorm.rvs(scale=row['mass_skew'], size=1)[0] * row['mass_center']
          #WIP - verify with sma_gen

          #Adds reported parameters to the obj_dict dictionary
          obj_dict['mass'].append(mass_instance)
          obj_dict['parent'].append(row["parentname"])
          obj_dict['e'].append(e_instance)
          obj_dict['i'].append(i_instance)
          obj_dict['sma'].append()
          obj_dict['period'].append()

          #Increases asteroid count by 1
          n_present += 1

  return obj_dict

def sma_gen(mode, parentmass, e_inst, in_mass=None, out_mass=None, inlim=None, outlim=None, in_apo=None, out_peri=None, in_tol=None, out_tol=None,
               in_res=None, out_res=None, res_arr=None):
  
  if mode == 'main':
    sma_instance = np.random.uniform(in_apo, out_peri)
    #Check for stability with this formula
    if (sma_instance*(1-e_inst) - in_apo) / ((in_apo+sma_instance)/2 * (in_mass/(3*parentmass))**(1/3)) <= in_tol:
      return sma_instance, p_instance
    
  if mode == 'res':
    for resonance in res_arr:
        sma_instance = resonance
    #WIP - Ensure falls in resonance
    
    return sma_instance, p_instance
    #WIP - Return parameters straight since stability is guaranteed
    
  if mode == 'trans':
    sma_instance = np.random.uniform(inlim, outlim)
    p_instance = 2 * np.pi * (sma_instance**3 / parentmass / 6.674E-11)**0.5
    #WIP - somewhat closer to the stability limits
    
    return sma_instance, p_instance
  if mode == 'irr':
    #Unstable objects which are just totally random
    sma_instance = np.random.uniform(in_apo, outlim)

    return sma_instance, p_instance
```


```python
# A sample test dictionary with needed parameters
objstatstest = {

    #Base properties (kg)
    "popname":['OID'],
    "num":[200],
    "groupfrac":[0.05],
    "mode":['main'], #Modes 'main', 'trans', 'irr'
    "parentname":['Olindias'],
    "parentmass":[6.11452E+26],
    "mass_center":[4.19E+12],
    "mass_skew":[5],
    "e_rad":[0.05],
    "e_center":[0.0],
    "i_rad":[1.0],
    "i_center":[0.0],

    #Limit properties (kg, m)
    "in_mass":[3.24659E+21],
    "out_mass":[3.14694E+21],
    "innerlimit":[None],
    "outerlimit":[None],
    "in_apocenter":[184770312.8],
    "out_pericenter":[252086941.2],
    "in_tolerance":[6.5],
    "out_tolerance":[6.5],
    "in_period":[],
    "out_period":[],
    "in_resonance_tolerance":[[2/3,3/4,4/5,5/6,6/7,7/9]],
    "out_resonance_tolerance":[[2/3,3/4,4/5,5/6]]
    }


os_format = pd.DataFrame(data=objstatstest)
```

## August 20 Prototype

<p>This earlier functional model did not attempt to account for the various peculiarities of asteroid distribution but successfully wrote a script for a given number of asteroids.</p>


```python
def gen_asteroids(txtname, num, parentname, parentmass,
                  limit_low, limit_high,
                  objtype, e_range, i_range, masscenter):
    with open(f"{txtname}.txt", mode="wt") as f:
        j = 1
        while j <num:
            
            #Generate parameters within passed limits using numpy
            sma = np.random.uniform(low=limit_low,high=limit_high)
            e = np.random.uniform(low=0.0,high=e_range)
            i = np.random.uniform(low=-i_range,high=i_range)
            mass = np.random.normal(loc=masscenter)

            if mass/(parentmass/1.9885E+30)**2.5/(sma/149600000)**1.125 * 807 < 1:
                
                #Write the script into file {textname}.txt with the generated parameters
                f.write(f"{objtype} \"RA_{parentname}_{j}\"\n")
                f.write("{\n")
                f.write(f"ParentBody \"{parentname}\"\n")
                f.write(f"Class \"Asteroid\"\n")
                f.write(f"Mass {mass}\n")
                f.write("Orbit\n")
                f.write("{\n")
                f.write(f"PeriodDays {(4*np.pi**2*(sma*1000)**3 / (6.67408E-11*(parentmass)))**0.5 / 86400}\n")
                f.write(f"SemiMajorAxisKm {sma}\n")
                f.write(f"Eccentricity {e}\n")
                f.write(f"Inclination {i}\n")
                f.write("}\n")
                f.write("}\n")

                j += 1
```
