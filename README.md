# The purpose of this code is to create a generalized chess knight, which moves a cells in one direction and b in a perpendicular direction. For example, a regular kight moves 1 unit in a direction and 2 in another.
# Then, the idea is to find how many moves this knight takes to get from the center (0,0) to any poiont (x,y) in an infinite grid.
# The code creates a color-coded grid, where each cell is colored according to the amount of moves it takes.
import matplotlib as mpl
from matplotlib import pyplot as plt
from matplotlib import colors
import numpy as np

# a and b are the amount of squares the knight moves in each direction. The following code ensures that ais greater than or equal to b, which is important later.
# m is the maximum amount of moves that will be displayed.
a=3
b=4
m=13
if b>a:
    temp=a
    a=b
    b=temp

# For some integer point in the plane (x,y), f1, f2, ..., f8 are the eight possible positions reachable by the generalized a,b-knight  
def f1(x,y):
    return [x-a,y-b]
def f2(x,y):
    return [x-a,y+b]
def f3(x,y):
    return [x+a,y-b]
def f4(x,y):
    return [x+a,y+b]
def f5(x,y):
    return [x-b,y-a]
def f6(x,y):
    return [x-b,y+a]
def f7(x,y):
    return [x+b,y-a]
def f8(x,y):
    return [x+b,y+a]

# c is the sum of a and b. We assume that the board is coloured as a chessboard. So if the origin (0,0) is black, a square (x,y) is black if x+y is even and white otherwise.  
# If c is odd, then the knight changes color after every move (eg. regular change knights change cllor after any move). That means that black sqaures can only be reached after an even amount of moves.
# This can be used to check less cases.
# Since we chose m to be 13, we are checking the squares that are reachable in 13 moves or less.
c=a+b

# For an integer n, Sn will be the set of squares that can be reachable in n moves. S0 is only the square at center, where the knight starts.
S0=[[0,0]]

# Only squares with c and y coordiantes a distance of maximum a from the origin can be reached in one move. (Hence, it is important that a>=b)
S1=[]
for x in range(-a,a+1):
    for y in range(-a,a+1):
        # Only white squares can be reached if c is odd. If c is even we check all the cases.
        if (x+y)%2==1 or c%2==0:
            # If a point in reachable in 1 move from a point in S0, then S0 is also reachable in 1 move from the point, since the moves are reversible.)
            if f1(x,y) in S0 or f2(x,y) in S0 or f3(x,y) in S0 or f4(x,y) in S0 or f5(x,y) in S0 or f6(x,y) in S0 or f7(x,y) in S0 or f8(x,y) in S0:
                S1.append ([x,y])
S2=[]
for x in range(-2*a,2*a+1):
    for y in range(-2*a,2*a+1):
        if (x+y)%2==0 or c%2==0:
            if f1(x,y) in S1 or f2(x,y) in S1 or f3(x,y) in S1 or f4(x,y) in S1 or f5(x,y) in S1 or f6(x,y) in S1 or f7(x,y) in S1 or f8(x,y) in S1:
                S2.append ([x,y])
S3=[]
for x in range(-3*a,3*a+1):
    for y in range(-3*a,3*a+1):
        if (x+y)%2==1 or c%2==0:
            if f1(x,y) in S2 or f2(x,y) in S2 or f3(x,y) in S2 or f4(x,y) in S2 or f5(x,y) in S2 or f6(x,y) in S2 or f7(x,y) in S2 or f8(x,y) in S2:
                S3.append ([x,y])            
S4=[]
for x in range(-4*a,4*a+1):
    for y in range(-4*a,4*a+1):
        if (x+y)%2==0 or c%2==0:
            if f1(x,y) in S3 or f2(x,y) in S3 or f3(x,y) in S3 or f4(x,y) in S3 or f5(x,y) in S3 or f6(x,y) in S3 or f7(x,y) in S3 or f8(x,y) in S3:
                S4.append ([x,y])
S5=[]
for x in range(-5*a,5*a+1):
    for y in range(-5*a,5*a+1):
        if (x+y)%2==1 or c%2==0:
            if f1(x,y) in S4 or f2(x,y) in S4 or f3(x,y) in S4 or f4(x,y) in S4 or f5(x,y) in S4 or f6(x,y) in S4 or f7(x,y) in S4 or f8(x,y) in S4:
                S5.append ([x,y])

S6=[]
for x in range(-6*a,6*a+1):
    for y in range(-6*a,6*a+1):
        if (x+y)%2==0 or c%2==0:
            if f1(x,y) in S5 or f2(x,y) in S5 or f3(x,y) in S5 or f4(x,y) in S5 or f5(x,y) in S5 or f6(x,y) in S5 or f7(x,y) in S5 or f8(x,y) in S5:
                S6.append ([x,y])
S7=[]
for x in range(-7*a,7*a+1):
    for y in range(-7*a,7*a+1):
        if (x+y)%2==1 or c%2==0:
            if f1(x,y) in S6 or f2(x,y) in S6 or f3(x,y) in S6 or f4(x,y) in S6 or f5(x,y) in S6 or f6(x,y) in S6 or f7(x,y) in S6 or f8(x,y) in S6:
                S7.append ([x,y])            
S8=[]
for x in range(-8*a,8*a+1):
    for y in range(-8*a,8*a+1):
        if (x+y)%2==0 or c%2==0:
            if f1(x,y) in S7 or f2(x,y) in S7 or f3(x,y) in S7 or f4(x,y) in S7 or f5(x,y) in S7 or f6(x,y) in S7 or f7(x,y) in S7 or f8(x,y) in S7:
                S8.append ([x,y])           
S9=[]
for x in range(-9*a,9*a+1):
    for y in range(-9*a,9*a+1):
        if (x+y)%2==1 or c%2==0:
            if f1(x,y) in S8 or f2(x,y) in S8 or f3(x,y) in S8 or f4(x,y) in S8 or f5(x,y) in S8 or f6(x,y) in S8 or f7(x,y) in S8 or f8(x,y) in S8:
                S9.append ([x,y])            
S10=[]
for x in range(-10*a,10*a+1):
    for y in range(-10*a,10*a+1):
        if (x+y)%2==0 or c%2==0:
            if f1(x,y) in S9 or f2(x,y) in S9 or f3(x,y) in S9 or f4(x,y) in S9 or f5(x,y) in S9 or f6(x,y) in S9 or f7(x,y) in S9 or f8(x,y) in S9:
                S10.append ([x,y])                  
S11=[]
for x in range(-11*a,11*a+1):
    for y in range(-11*a,11*a+1):
        if (x+y)%2==1 or c%2==0:
            if f1(x,y) in S10 or f2(x,y) in S10 or f3(x,y) in S10 or f4(x,y) in S10 or f5(x,y) in S10 or f6(x,y) in S10 or f7(x,y) in S10 or f8(x,y) in S10:
                S11.append ([x,y]) 
S12=[]
for x in range(-12*a,12*a+1):
    for y in range(-12*a,12*a+1):
        if (x+y)%2==0 or c%2==0:
            if f1(x,y) in S11 or f2(x,y) in S11 or f3(x,y) in S11 or f4(x,y) in S11 or f5(x,y) in S11 or f6(x,y) in S11 or f7(x,y) in S11 or f8(x,y) in S11:
                S12.append ([x,y])
            
S13=[]
for x in range(-13*a,13*a+1):
    for y in range(-13*a,13*a+1):
        if (x+y)%2==1 or c%2==0:
            if f1(x,y) in S12 or f2(x,y) in S12 or f3(x,y) in S12 or f4(x,y) in S12 or f5(x,y) in S12 or f6(x,y) in S12 or f7(x,y) in S12 or f8(x,y) in S12:
                S13.append ([x,y])
                
# f(x,y) is the minimum points needed to reach (x,y). A point may appear in more than one list, hence the following code finds the mimimum. There could be points which haven't appeared yet, therefore the value m+1 (In this case 14) is assigned to them.               
def f(x,y):
    n=[x,y]
    if n in S0:
        return 0
    elif n in S1:
        return 1
    elif n in S2:
        return 2
    elif n in S3:
        return 3
    elif n in S4:
        return 4
    elif n in S5:
        return 5
    elif n in S6:
        return 6
    elif n in S7:
        return 7
    elif n in S8:
        return 8
    elif n in S9:
        return 9
    elif n in S10:
        return 10
    elif n in S11:
        return 11
    elif n in S12:
        return 12
    elif n in S13:
        return 13
    else:
        return m+1
    
# Creates an array with all the pairs and their f value
arr=[]
for i in range (-a*m,a*m+1):
    l=[]
    for j in range (-a*m,a*m+1):
        l.append(f(i,j))
    arr.append(l)

# Creates a grid with every square and a color assigned depending on the amount of moves it takes. The colors are chosen to roughly represent the colors of a rainbow, with the origin black and white if it is not reachable in 13 moves or less.
fig = plt.figure(figsize=(40,40))
colormap = mpl.colors.ListedColormap(["#000000","#FF0000","#FF8000","#FFBF00","#FFFF00","#00FF00","#33FFA2","#00FFFF","#00BFFF","#0080FF","#0000FF", "#8000FF","#BF00FF","#FF00FF","#FFFFFF"])
plt.imshow(arr,
             cmap=colormap)

ax = plt.gca();
bar=plt.colorbar()
ax.grid(which='major', axis='both', linestyle='-', color='k', linewidth=0.5)
ax.set_xticks(np.arange(-0.5, 2*a*m+1.5, 1));
ax.set_yticks(np.arange(-0.5, 2*a*m+1.5, 1));\

plt.show()
