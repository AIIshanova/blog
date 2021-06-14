---
title: Projet de groupe
summary: Projet № 5 "l'épidémie"
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

Co-auteurs: Smorodova D., Shutenko V., Surtzov S. and Firtsov I.

## Description

Un petit projet à l'université.

## Model

### Model SIR

Les modèles mathématiques de maladies infectieuses, d'abord outils purement théoriques, ont commencé à être mis en pratique avec le problème du SIDA dans les années 1980. Lors de la pandémie Covid 19, les modélisations mathématiques ont connu un essor lors de la prise de décision relatives aux politiques de santé publique et a également contribué à l'épidémiosurveillance de la maladie.

Bien avant cela, depuis la pandémie de grippe espagnole, des modèles compartimentaux sont utilisés pour faciliter les calculs de probabilité de contagion. Ces modèles divisent la population en classes épidémiologiques.

Un modèle épidémiologique se fonde sur deux concepts : les compartiments et les règles. Les compartiments divisent la population en divers états possibles par rapport à la maladie. Par exemple, William Ogilvy Kermack et Anderson Gray McKendrick proposèrent un modèle fondateur dans lequel la population était divisée entre les individus susceptibles de contracter la maladie (compartiment {\displaystyle S}S), et les individus infectieux (compartiment {\displaystyle I}I)B 1. Les règles spécifient la proportion des individus passant d'un compartiment à un autre. Ainsi, dans un cas à deux compartiments, il existe une proportion {\displaystyle p(S\to I)}{\displaystyle p(S\to I)} d'individus sains devenant infectés et, selon les maladies, il peut aussi exister une proportion {\displaystyle p(I\to S)}{\displaystyle p(I\to S)} d'individus infectieux étant guéris. L'acronyme utilisé pour un modèle est généralement fondé sur l'ordre de ses règles. Dans le modèle {\displaystyle SIR}{\displaystyle SIR}, un individu est initialement sain ({\displaystyle S}S), peut devenir infecté ({\displaystyle I}I) puis être guéri ({\displaystyle R}R) ; si la guérison n'était pas possible, alors il s'agirait d'un modèle {\displaystyle SI}{\displaystyle SI}C 2.

Un individu infecté par le VIH est plus infectieux durant la 1re phase, lorsque sa charge virale (rouge) atteint un pic. L'infectivité par contact serait de l'ordre de 0,05, tandis qu'une infectivité de 0,003 représenterait une phase plus tardive de la maladieA 1.
Sept compartiments sont couramment utilisés : {\displaystyle S}S, {\displaystyle I}I, {\displaystyle E}E, {\displaystyle D}D, {\displaystyle R}R, {\displaystyle M}M et {\displaystyle C}C. Le compartiment {\displaystyle S}S est nécessaire, puisqu'il doit initialement exister des individus n'ayant pas encore été infectés. Lorsqu'un individu du compartiment {\displaystyle S}S est exposé à la maladie, il ne devient pas nécessairement capable de la transmettre immédiatement, selon l'échelle de temps considérée dans le modèle. Par exemple, si la maladie nécessite deux semaines pour rendre l'individu infectieux (ce qui est appelé une période de latence de deux semaines) et que le modèle représente l'évolution journalière de la population, alors l'individu ne va pas directement dans le compartiment {\displaystyle I}I (infectieux) mais doit passer par un compartiment intermédiaire. Un tel compartiment est noté {\displaystyle E}E, pour les individus exposés.

Selon les maladies, il peut être utile de distinguer les individus infectés. Si la maladie est causée par des organismes parasites tel le ver parasite ou les tiques, alors la concentration de ces organismes peut justifier de diviser la classe {\displaystyle I}I en plusieurs classes représentant plusieurs niveaux de concentration. Lorsque la maladie est causée par des virus ou des bactéries, un grand nombre de modèles ne divisent pas la classe {\displaystyle I}I : ils considèrent que l'individu est infecté ou ne l'est pasC 3. Cependant, dans le cas d'un virus, il existe un analogue à la concentration en organismes parasitaires : il s'agit de la charge virale, qui exprime la concentration du virus dans un volume donné tel que le sang. Les individus peuvent donc être distingués selon leur charge, puisque celle-ci les rend infectieux à des niveaux différents, ainsi qu'illustré ci-contre dans le cas du VIH.

Après qu'un individu a été infecté, trois cas de figure peuvent se produire. Premièrement, l'individu peut décéder, auquel cas il relève du compartiment {\displaystyle D}D. Deuxièmement, la maladie peut se terminer d'elle-même et conférer à l'individu une immunisation contre la réinfection, et il est assigné à un compartiment {\displaystyle R}R. Enfin, l'individu peut toujours être infectieux mais il se retrouve isolé de la population par politique de quarantaine, correspond à un compartiment {\displaystyle Q}QE 1. Séparer les individus morts des individus en quarantaine permet également de tenir compte du fait que ces derniers peuvent éventuellement guérir et réintégrer le compartiment {\displaystyle S}S. Outre les compartiments cités, {\displaystyle M}M représente les individus disposant d'une immunité à la naissance (par voie maternelle), et {\displaystyle C}C représente les individus porteurs de la maladie (carriers) mais qui n'en expriment pas les symptômes.

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

## Les sources

1. Compartmental models in epidemiology - https://en.wikipedia.org/wiki/Compartmental_models_in_epidemiology
2. *А.В. Гаврилина , С.В. Соколов* - Анализ SIR-модели распространения заболеваний, pp 229-232, 2018.
