# COMSOL Tutorial: Setup and Simulation Guide

This tutorial is designed for individuals with no prior experience in COMSOL. We've included detailed instructions to ensure a smooth learning process. If you are already familiar with COMSOL, you may want to skip directly to the [**Detailed Parameter Settings**](#detailed-parameter-settings).

## Table of Contents

1. [Introduction](#introduction)
2. [Global Definitions and Material Settings](#global-definitions-and-material-settings)
3. [Geometry](#geometry)
4. [Material](#material)
5. [Multiphysics and Thermal Modules](#multiphysics-and-thermal-modules)
6. [Meshing](#meshing)
7. [Detailed Parameter Settings](#detailed-parameter-settings)

## Introduction

In this tutorial, you will learn how to set up and run a thermal simulation in COMSOL, focusing on the **Heat Transfer in Solids** and **Surface-to-Surface Radiation** modules.

## Global Definitions and Material Settings

In the **Global Definitions**, you will define parameters that typically depend on temperature, such as thermal conductivity (\( k \)), heat capacity (\( C \)), and emissivity (\( \epsilon \)). These are defined as functions, often represented by data points that are interpolated and extrapolated. You can plot these functions to visualize the curves.

<p align="center">
  <img src="https://github.com/user-attachments/assets/b174dde6-5041-4ece-a453-7dac253ba1a8" alt="Global Definitions and Material Settings" width="1000"/>
</p>

Additionally, the PTC power functions (P1, P2) consist of two functions that take the temperature from the 40K and 4K PT heads. These functions read points from an external file, then interpolate and extrapolate within COMSOL. We will reference these functions later to demonstrate how to utilize them effectively.

COMSOL provides a built-in **Material Library**; however, if you do not have access to this library, you can use our material table [here](link). Most components in our simulation are made of **OFHC copper**.

## Probes

In the **Component 1** tab, you can set up probes that will record the temperature data and store it in the "Study" section for easier plotting. You can also modify the output method in the settings. As an example, we will use the PTC probe.

![image](https://github.com/user-attachments/assets/99296d6b-29aa-4bdd-ab79-ea7002e98464)

We use the functions defined in the **Global Definitions** and take the temperature from the probes \( T_{40K\_ptc} \) and \( T_{4K\_ptc} \). The functions will return the PTC power, which will be useful when defining the heat flux.

## Geometry

We start by importing the **SolidWorks file** into COMSOL. It's crucial to understand the **simulation scale** so you can decide which parts to omit or simplify, especially for large-scale simulations. For example, in our model, we simplified the **thermal interface between PT and Shell** into a plain slab to significantly reduce simulation time. This simplification will also be advantageous during the meshing process.

To achieve this, use the "Delete Entity" tool to select the parts or surfaces you want to remove from the model. Afterward, you can assign materials to the parts in the **Material** tab.

## Multiphysics and Thermal Modules

For this thermal study, focus on two COMSOL modules: **Heat Transfer in Solids** and **Surface-to-Surface Radiation**. Select these modules when creating a new simulation.

### Heat Transfer in Solids

![image](https://github.com/user-attachments/assets/5d87ce7b-9bcb-4f49-8b24-efb2d6c230fd)

It's important to define the **Initial Value**, which is typically set to the ambient temperature. We will also define the PT 4K and 40K head temperatures as constant temperatures. Next, define the **Heat Flux** using the P1 and P2 functions that we established in the **Global Definitions**.

### Surface-to-Surface Radiation

To reduce the simulation time, select only the diffuse surfaces you want to study. In some cases, it may be helpful to restrict the surface diffusion to one direction. Additionally, the **Opacity** parameter can be tricky; setting a domain as opaque means it will have no absorption, only reflection.


## Meshing

Meshing can be very tricky, and you may encounter errors related to "Domain," "Surface," or "Edge." Adjust the **Element Size** from **Extremely Coarse** to **Extremely Fine** based on the complexity of the components. For detailed parts with many edges or sharp corners, group them and apply a finer mesh. For other domains, use a normal or coarser mesh. If errors persist, try different meshing generators by right-clicking on the **Mesh** tab and selecting options like **Free Tetrahedral**, **Free Triangle**, or **Free Quad**. The choice of meshing generator is flexible as long as no errors occur.

## Study
Finally, we are going to run our simulation here.

A lot of odd thing could happen, for example, trying to avoid odd number when you set the study time, (0,1,3)h could cause the unconverged initial value. It is always good to run a stationary study first then the time dependent study and you could also set the stationary study as your initial value to avoid unconverged initial value error. 
## Detailed Parameter Settings

For advanced users, refer to the **Detailed Parameter Settings** section, where all parameters that need tuning or definition from scratch are highlighted in **bold**.


