---
title: Group project
summary: Project № 5 "Epidemic"
tags:
- Group project
date: "2021-05-08T00:00:00Z"

# Optional external URL for project (replaces project detail page).
#external_link: ""

#image:
#  caption: Photo by rawpixel on Unsplash
#  focal_point: Smart

#links:
#- icon: twitter
#  icon_pack: fab
#  name: Follow
#  url: https://twitter.com/georgecushen
#url_code: ""
#url_pdf: ""
#url_slides: ""
#url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
#slides: content/slides
---

Co-authors: Smorodova D., Shutenko V., Surtzov S. and Firtsov I.

## Description

A small university project.

## Model

### Model SIR

Compartmental models simplify the mathematical modelling of infectious diseases. The population is assigned to compartments with labels – for example, S, I, or R, (Susceptible, Infectious, or Recovered). People may progress between compartments. The order of the labels usually shows the flow patterns between the compartments; for example SEIS means susceptible, exposed, infectious, then susceptible again.

The origin of such models is the early 20th century, with important works being that of Ross in 1916, Ross and Hudson in 1917, Kermack and McKendrick in 1927 and Kendall in 1956.

The models are most often run with ordinary differential equations (which are deterministic), but can also be used with a stochastic (random) framework, which is more realistic but much more complicated to analyze.

Models try to predict things such as how a disease spreads, or the total number infected, or the duration of an epidemic, and to estimate various epidemiological parameters such as the reproductive number. Such models can show how different public health interventions may affect the outcome of the epidemic, e.g., what the most efficient technique is for issuing a limited number of vaccines in a given population.

The SIR model is one of the simplest compartmental models, and many models are derivatives of this basic form. The model consists of three compartments:

- S: The number of susceptible individuals. When a susceptible and an infectious individual come into "infectious contact", the susceptible individual contracts the disease and transitions to the infectious compartment.
- I: The number of infectious individuals. These are individuals who have been infected and are capable of infecting susceptible individuals.
- R for the number of removed (and immune) or deceased individuals. These are individuals who have been infected and have either recovered from the disease and entered the removed compartment, or died. It is assumed that the number of deaths is negligible with respect to the total population. This compartment may also be called "recovered" or "resistant".
This model is reasonably predictive for infectious diseases that are transmitted from human to human, and where recovery confers lasting resistance, such as measles, mumps and rubella.

Spatial SIR model simulation. Each cell can infect its eight immediate neighbors.
These variables (S, I, and R) represent the number of people in each compartment at a particular time. To represent that the number of susceptible, infectious and removed individuals may vary over time (even if the total population size remains constant), we make the precise numbers a function of t (time): S(t), I(t) and R(t). For a specific disease in a specific population, these functions may be worked out in order to predict possible outbreaks and bring them under control.

As implied by the variable function of t, the model is dynamic in that the numbers in each compartment may fluctuate over time. The importance of this dynamic aspect is most obvious in an endemic disease with a short infectious period, such as measles in the UK prior to the introduction of a vaccine in 1968. Such diseases tend to occur in cycles of outbreaks due to the variation in number of susceptibles (S(t)) over time. During an epidemic, the number of susceptible individuals falls rapidly as more of them are infected and thus enter the infectious and removed compartments. The disease cannot break out again until the number of susceptibles has built back up, e.g. as a result of offspring being born into the susceptible compartment.

Each member of the population typically progresses from susceptible to infectious to recovered. This can be shown as a flow diagram in which the boxes represent the different compartments and the arrows the transition between compartments, i.e.

## Octave code

### if-else

>>
    function res = SIR(S0,I0,Ik,R0,a,b,tk)
         # getting parameters in ODE
        rate2 = @(t,state) rate(t,state,Ik,a,b);
    
        # solving ODE system
        [T,state] = ode23(rate2,[0,tk],[S0,I0,R0]); #soulving Cauchy problem

        # extracting separate system parameters
        S = state(:,1);
        I = state(:,2);
        R = state(:,3);

       # drawing a graph
        hold on
        plot(T,S,'b')
        plot(T,I,'r')
        plot(T,R,'g')
        xlabel('Time')
        ylabel('Number of people')
        legend('S - Susceptible', 'I - Infectious', 'R - Recovered')
        title("SIR-model")
    end

     `# ODE system
    function res = rate(t,state,Ik,a,b)
        #getting all initial stages
        s = state(1);
        i = state(2);
        r = state(3);
    
        # ODE system
        if (i > Ik)
              dsdt = -a*s;
              didt = a*s-b*i;
              drdt = b*i;
          else dsdt = 0;
               didt = -b*i;
               drdt = b*i;
         endif
        #
        # packing up everything
        res = [dsdt;didt;drdt];
    end
>>

### heaviside

>>
    function res = SIR(S0,I0,Ik,R0,a,b,tk)
        # getting parameters in ODE
        rate2 = @(t,state) rate(t,state,Ik,a,b);
    
        # solving ODE system
        [T,state] = ode23(rate2,[0,tk],[S0,I0,R0]); #soulving Cauchy problem

        # extracting separate system parameters
       S = state(:,1);
       I = state(:,2);
       R = state(:,3);

        # drawing a graph
        hold on
        plot(T,S,'b')
        plot(T,I,'r')
        plot(T,R,'g')
        xlabel('Time')
        ylabel('Number of people')
        legend('S - Susceptible', 'I - Infectious', 'R - Recovered')
        title("SIR-model")
    end

     `# ODE system
    function res = rate(t,state,Ik,a,b)
        #getting all initial stages
        s = state(1);
        i = state(2);
        r = state(3);
    
        # 
        dsdt = heaviside(i-Ik)*(-a*s);
        didt = heaviside(i-Ik)*(a*s)-b*i;
        drdt = b*i;
        #
        # packing up everything
        res = [dsdt;didt;drdt];
    end
>>

## Sources

1. Compartmental models in epidemiology - https://en.wikipedia.org/wiki/Compartmental_models_in_epidemiology
2. *А.В. Гаврилина , С.В. Соколов* - Анализ SIR-модели распространения заболеваний, pp 229-232, 2018.
