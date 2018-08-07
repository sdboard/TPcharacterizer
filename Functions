# Libraries
import numpy
import matplotlib.pyplot
import pandas
import os

# Constants
ETA = 376.730313

# Functions

##############################################################################
# Function Name: Zo
#
# Description: This function calculates the impedance of a shielded twisted
#              pair while incorporate the lay length by utilizing a formaula 
#              developed by Lefferson [see citations]
#
# Parameters:
#       d    --> Outer Diameter of a single wire in a twisted pair 
#       D    --> Either the spacing between the center of the wires OR the 
#                total OD of the single wire after insulation
#       er1  --> relative permittivity of material outside of twisted pair
#       er2  --> relative permittivity of wire insulation
#       Tint --> Lay Length in centimeters
#
##############################################################################
def Zo(d, D, er1, er2, Tint):
    T = 100/Tint
    theta = numpy.arctan(T * numpy.pi * D)
    q = 0.25 + 0.0004*(theta**2)
    Eeff = er1 + (q*(er2 - er1))
    return (ETA/(numpy.pi*numpy.sqrt(Eeff)))*numpy.arccosh(D/d)

##############################################################################
# Function Name: Tpi
#
# Description: This function calculates the number of twists per unit length
#
# Parameters:
#       theta--> The Pitch Angle
#       D    --> Either the spacing between the center of the wires OR the 
#                total OD of the single wire after insulation
#
##############################################################################
def Tpi(theta, D):
    return numpy.tan(theta*numpy.pi/180)/(numpy.pi*D)

##############################################################################
# Function Name: pitch
#
# Description: The inverse of Tpi, this function calculates the pitch angle
#              based on the number of twists per unit length
#
# Parameters:
#       T    --> Twists per Length
#       D    --> Either the spacing between the center of the wires OR the 
#                total OD of the single wire after insulation
#
# Note:
#      The Pitch can be commonly understood as follows: 
#      the angle from the normal (the direction of the cable) that an 
#      individual wire makes while revolving around the other. To maintain
#      forward propagation of the cable, the angle cannot exceed 90 degrees
#
##############################################################################
def pitch(T,D):
    return (180/numpy.pi)*(numpy.arctan(numpy.pi*D*T))

##############################################################################
# Function Name: ZoCoax
#
# Description: Calculates the characteristic impedance of a coaxial
#              transmission line
#
# Parameters:
#       er   --> the dielectric's relative permittivity
#       D    --> the inner diameter of the outer conductor OR the outer 
#                diameter of the dielectric
#       d    --> the outer diameter of the inner conductor
#############################################################################
def ZoCoax(er,D,d):
    return (60/numpy.sqrt(er))*numpy.log(D/d)

##############################################################################
# Function Name: ZoSPo
#
# Description: Calculates the characteristic impedance of a shielded twinax
#
# Parameters:
#       er   --> the dielectric's relative permittivity
#       s    --> Either the spacing between the center of the wires 
#       d    --> the outer diameter of a signal wire
#       D    --> the inner diameter of the shield (circular)
#
# Note:
#      This gives the odd modes.  And we only care about the odd modes for
#      differential signaling.
#
#############################################################################
def ZoSPo(d,s,D,er):
    return (ETA/numpy.pi/numpy.sqrt(er))*(numpy.log((2*s/d)*(1.0-(s/D)*2)/(1.0+(s/D)**2))-((1.0+4*(s/d)**2)*(1.0-4*(s/d)**2)/(16*(s/d)**4)))

##############################################################################
# Function Name: ZoSPe
#
# Description: Calculates the characteristic impedance of a shielded twinax
#
# Parameters:
#       er   --> the dielectric's relative permittivity
#       s    --> Either the spacing between the center of the wires 
#       d    --> the outer diameter of a signal wire
#       D    --> the inner diameter of the shield (circular)
#
# Note:
#      This gives the even modes.
#
#############################################################################
def ZoSPe(d,s,D,er):
    return (ETA/numpy.pi/numpy.sqrt(er))*numpy.log(((s/d)/(2*(s/D)**2))*(1.0-(s/D)**4))
    
