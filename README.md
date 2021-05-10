from math import *
import matplotlib.pyplot as plt


epsilon = 1e-6
Nitermax = 5e4

print("POINT FIXE",)
def Point_Fixe(g,x0,epsilon,Nintermax,alpha):

    xold = x0
    xnew = g(xold)
    n = 1
    L_n=[]
    L_xn=[]
    L_en=[]
    
    
    while abs(xnew-xold) > epsilon and n < Nitermax : 
        xold = xnew
        xnew = g(xold)
        n = n + 1
        L_n.append(n)
        L_xn.append(xnew) #xold ou xnew?
        L_en.append(xnew-alpha) #pour xn : xold ou xnew?
    return (L_n,L_xn,L_en)
   

print("FONCTION ZERO point fixe")

def g0(x):
    return (1 + sin (x))/2

print(Point_Fixe(g0,0,epsilon,Nitermax,0.8878620474343383))


plt.plot('L_en')
plt.xlabel('L_n')
plt.ylabel('l_xn')
plt.show()



# 2. x = 3*cos(x)-2
print("PREMIERE FONCTION")

def g2(x) :
    return acos((x+2)/3)

print(Point_Fixe(g2,0.5,epsilon,Nitermax,0.553))

def g2bis(x) :
    return -acos((x+2)/3)

print(Point_Fixe(g2bis,-1.4,epsilon,Nitermax,1.354))

def g2_bis(x):
    return acos((x+2)/3)-(2*pi)

print(Point_Fixe(g2_bis,-4.1,epsilon,Nitermax,-3.988))

# 3  x*exp(x)-7 = 0
print("SECONDE FONCTION")

def g3(x) :
    return log(7/x)

print(Point_Fixe(g3,1.5,epsilon,Nitermax,1.524345))



# 8   x**4- 2*x**2 + 4*x - 17 = 0
print("TROISIEME FONCTION")

def g8(x) :
    return ((17-4*x)/((x**2)-2))**(1/2)

print(Point_Fixe(g8,2,epsilon,Nitermax,2.0345))

def g8bis(x) :
    return -((17-4*x)/((x**2)-2))**(1/2)

print(Point_Fixe(g8bis,-2.5,epsilon,Nitermax,-2.509))



print("NEWTON")


def Newton(f,fder,x0,epsilon,Nitermax,alpha):
     xold = x0
     xnew = xold - (f(xold)/fder(xold))
     n= 1
     Nitermax = 0 
     L_n=[]
     L_xn=[]
     L_en=[]
     
     while abs(xnew - xold) > epsilon and n < Nitermax :
         xold = xnew
         xnew = x0 - (f(xold)/fder(xold))
         n = n + 1
         L_n.append(n)
         L_xn.append(xnew) #xold ou xnew?
         L_en.append(xnew-alpha) #pour xn : xold ou xnew?
     return (L_n,L_xn,L_en)
 
print ("FONCTION ZERO")

def f(x):
    return 2*x-(1 + sin (x))


def fder(x):
    return 2-cos(x)

print(Newton(f,fder,0,epsilon,Nitermax,0.8878620474343383))
plt.plot('L_en')
plt.xlabel('L_n')
plt.ylabel('l_xn')
plt.show()



# 2    x = 3*cos(x)-2
print("PREMIERE FONCTION")

def f2(x):
    return 3*cos(x)-2-x

def fder2(x):
    return -3*sin(x)-1

print (Newton(f2, fder2, 0.5, epsilon, Nitermax,0.553))

print (Newton(f2, fder2, -1.4, epsilon, Nitermax,-1.354))

print (Newton(f2, fder2, -4.1, epsilon, Nitermax,-3.988))

# 3  x*exp(x)-7 = 0
print("SECONDE FONCTION")

def f3(x):
    return x*exp(x)-7

def fder3(x):
    return x*exp(x)*(x + 1)

print (Newton(f3, fder3, 1.5, epsilon, Nitermax,1.524345))


# 8   x**4- 2*x**2 + 4*x - 17 = 0
print("TROISIEME FONCTION")

def f8(x):
    return x**4 - 2*x**2 + x -17

def fder8(x):
    return 4*x**3 - 4*x + 1

print (Newton(f8, fder8, 2, epsilon, Nitermax,2.0345))

print (Newton(f8, fder8, -2.5, epsilon, Nitermax,-2.509))



print("dichotomie et secante")

def Dichotomie(f, a0, b0, epsilon, Nitermax,alpha):

    n = 1
    L_n=[]
    L_an=[]
    L_en=[]
   
    while abs(b0 - a0) > epsilon and n < Nitermax :

        m = (a0 + b0)/2
        
        if (f(a0) * f(m) <= 0):
            b0 = m
            L_an.append(m) 
            L_en.append(m-alpha) 

        else :
            a0 = m
            L_an.append(m) 
            L_en.append(m-alpha) 

        n = n + 1
        L_n.append(n)
        
        
        return(L_n,L_an,L_en)
        
def Secante(f, x0, x1, epsilon, Nitermax,alpha):

    n = 1
    L_n=[]
    L_xn=[]
    L_en=[]

    while abs(x1 - x0) > epsilon and n < Nitermax :
        x2 = (x0 * f(x1) - x1 * f(x0))/(f(x1)-f(x0))
        x0,x1 = x1,x2
        n = n + 1
        L_n.append(n)
        L_xn.append(x2) #xold ou xnew?
        L_en.append(x2-alpha) #pour xn : xold ou xnew?
    return (L_n,L_xn,L_en)
 
print("FONCTION ZERO")

def f(x):
    return 2*x-(1 + sin (x))
print(Dichotomie(f, 0, 1, epsilon, Nitermax,0.8878620474343383))
plt.plot('L_en')
plt.xlabel('L_n')
plt.ylabel('l_an')
plt.show()

print(Secante(f, 0, 1, epsilon, Nitermax,0.8878620474343383))
plt.plot('L_en')
plt.xlabel('L_n')
plt.ylabel('l_xn')
plt.show()



#2  x = 3*cos(x)-2
print("PREMIERE FONCTION")
def f3(x):
    return x - 3 * cos(x) + 2  # 3 solutions 

print (Dichotomie(f3, 0, 1, epsilon, Nitermax,0.553))
print (Dichotomie(f3, -1.5, -1, epsilon, Nitermax,-1.354))
print (Dichotomie(f3, -4.5, -3.5, epsilon, Nitermax,-3.988), '\n'*3)

print (Secante(f3, 0, 1, epsilon, Nitermax,0.553))
print (Secante(f3, -1.5, -1, epsilon, Nitermax,-1.354))
print (Secante(f3, -4.5, -3.5, epsilon, Nitermax,-3.988))



# 3  x*exp(x)-7 = 0

print("SECONDE FONCTION")

def f2(x):
    return x * exp(x) - 7    # 1 solution

print (Dichotomie(f2, 1.25, 2, epsilon, Nitermax,1.524345),'\n'*3)

print (Secante(f2, 1.25, 2, epsilon, Nitermax,1.524345), '\n'*3)




# 8   x**4- 2*x**2 + 4*x - 17 = 0
print("TROISIEME FONCTION")

def f1(x):
    return x**4 - 2*x**2 + 4*x - 17   # 2 solutions

print(Dichotomie(f1, 2, 2.5, epsilon, Nitermax,2.0345))
print(Dichotomie(f1, -2.6, -2.4, epsilon, Nitermax,-2.509),'\n'*3)

print(Secante(f1, 2, 2.5, epsilon, Nitermax,2.0345))
print(Secante(f1, -2.6, -2.4, epsilon, Nitermax,-2.509), '\n'*3)














    
 
    
