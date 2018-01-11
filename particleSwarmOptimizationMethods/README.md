# Particle Swarm Optimization

Implements three different forms of particle swarm optimization for solving optimization problems of 
the general form 

    min f(x,y)=min f(x) or max f(x,y) = max f(x) where y are inputs with known values
     x          x           x            x

with arbitrary constraints. The versions of particle swarm optimization are
  1) Standard particle swarm optimization (PSO)
  2) Constricted particle swarm optimization (GCPSO)
  3) Non-parameteric particle swarm optimization. 
All of these methods are explained in detail in 

[1] Behesti et al., "Non-parametric particle swarm optimization for global optimization",Applied Soft. Computing. 2015
    http://www.sciencedirect.com/science/article/pii/S1568494614006474

# Running Tests

This file contains a file, testCode, that tests the different forms of Particle Swarm Optimization. The python arguments into the terminal are as follows:

    testUse = sys.argv[1]; methodUse = sys.argv[2]; optimType = sys.argv[3]; nDim = int(sys.argv[4]); numIters = int(sys.argv[5])

The valid inputs for testUse (function to be tested), methodUse (the PSO method), and the optimType are the following string arrays simultaneously.

    testString = ['sphere','ackleys','mccormic','beales','rastrigin'] 
    methodString = ['PSO','GCPSO','NPSO'];
    optimTypeString = ['max','min']

The PSO parameters are defined in the following block of code:

    #Define PSO Parameters
    numParticles=40;
    neighborSize = 2#NPSO Parameter
    w=1.0;
    tol=1e-3;
    #numIters=1000#nFeatures*15;
    numEvalState=2;
    kappa = 0.5;
    mult=1;
    c1=2.0
    c2 = c1*mult;
    constrict=1.0
    optimType='Min';
    
Finally, the PSO algorithm is executed in the following block.

    #Execute PSO
    if (methodUse == 'PSO'):
       output=pso.executePSO(c1,c2,w,posMin,posMax,velMin,velMax,numIters,numParticles,psoParticle,optimType,numEvalState,funcUsed,evaluateFitnessFunctions)
    elif (methodUse == 'GCPSO'):
        c1=2.05; c2=c1;
        output=pso.executeGCPSO(constrict,c1,c2,w,posMin,posMax,velMin,velMax,numIters,numParticles,psoParticle,optimType,numEvalState,funcUsed,evaluateFitnessFunctions)
    elif (methodUse == 'NPSO'):
        output=pso.executeNPSO(neighborSize,w,posMin,posMax,velMin,velMax,numIters,numParticles,npsoParticle,optimType,numEvalState,funcUsed,evaluateFitnessFunctions,npsoInterpFunc)
