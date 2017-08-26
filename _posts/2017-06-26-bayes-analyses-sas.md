---
layout: default
title: "bayes analyses (SAS) class notes, well, call it notes"
date: 2017-06-26 07:26:27 -0700
---
/*Chapter I*/  
/*Demo #1: GENMOD non informative prior*/  
```proc genmod data=sasuser.birth desc;
    model low = alcohol hist_hyp mother_wt prev_pretrm
                / dist=binomial link=logit;
	bayes seed=90210 outpost=out_birth stats=all;
    title 'Bayesian Analysis of Low Birth Weight Model with non informative prior';
run;

/*autocall macros*/
/*gelman is used to compare chains*/
/*%gelman(chains); */

%tadplot(data=out_birth, var=loglike logpost intercept alcohol);
%geweke(data=out_birth);
%heidel(data=out_birth);
%raftery(data=out_birth);
%mcse(data=out_birth);
%ess(data=out_birth);
%postcov(data=out_birth);
%postcor(data=out_birth);
%postint(data=out_birth);
%postsum(data=out_birth);
%cater(data=out_birth, var=intercept alcohol);

proc print data=pred(obs=50);
run;
proc means data=pred clm var mean n std;
run;
```
/*Demo #2: Informative Prior*/  
```data prior_birth;
   input _TYPE_ $ alcohol1 hist_hyp mother_wt prev_pretrm;
datalines;
Mean 1.0986 0 0 0
Var 0.00116 1e6 1e6 1e6 
;
run;
proc genmod data=sasuser.birth desc;
    class alcohol(desc);
    model low = alcohol hist_hyp mother_wt prev_pretrm
                / dist=binomial link=logit;
	lsmeans alcohol / diff oddsratio plots=all cl;
    bayes seed=27513 coeffprior=normal(input=prior_birth) sampling=arms  
          outpost=out_birth2 plots(smooth)=all diag=all nmc=25000;
    title 'Bayesian Analysis of Low Birth Weight Model with informative prior for alcohol1';
run;
```
/*Demo #3: PHREG .. what is survival analysis? how that link to telco? churn analysis, time to call, time to device burnout etc. */
```data prior_methadone;
   input _TYPE_ $ dose clinic1 prison;
datalines;
Mean -0.034160 0 0
Var .0003217 1e6 1e6 
;
run;

proc phreg data=sasuser.methadone;
   class clinic (param=ref ref='2');
   model time*status(0)=clinic dose prison / ties=exact;
   bayes seed=27513 coeffprior=normal(input=prior_methadone) diag=all 
   plots(smooth)=all sampling=rwm thin=10 nmc=200000 statistics=all;
   hazardratio "HR1" clinic;
   hazardratio "HR2" dose / units=10;
   hazardratio "HR3" prison;
   title "Bayesian Analysis with Informative Prior for Methadone Data";
run;
```
/*Chapter II*/  
/*Demo #1: Logistic Regression*/  
	/*--> see above birth example*/  
	/*    and take time to implement it in R? */  
/*Demo #2: PREDDIST*/  
	/* --> see above to output in genmod ? nop, pre-existing procs does not support PREDDIST */  
	/* hand calc required on posterior using IML */  
/*Demo #3: Mixed Model, random effect  
	.. hierarchical model is considered a particular type of bayesian network,   
	not to be confused with mixture (mixing) model?  
	[reference](http://support.sas.com/documentation/cdl/en/statug/63962/HTML/default/viewer.htm#statug_fmm_a0000000343.htm)  

	mixed model  
	y = f + gamma  
	mixing model (mixture)  
	y = f * pr(U)  
*/  
/*proc hpbnet*/  
```proc genmod data=sasuser.toy;
	class adhesive toy;
	model pressure = adhesive;
	repeated subject = toy;
run;
proc glimmix data=sasuser.toy;
	class adhesive toy;
	model pressure = adhesive;
	random int  /subject=toy residual;
run;
proc fmm data=sasuser.toy;
	class adhesive toy;
	model pressure = adhesive;
	model + toy;
	bayes;
run;

proc sgplot data=sasuser.toy;
	series x=adhesive y=pressure;
run;

proc mcmc data=sasuser.toy plots=all stats=all;
	parm beta0 beta1 beta2 sigma2;
	prior beta : N(0, var=1e6);
	prior sigma2 ~ igamma(2.001, 1.001)
	mu = beta0 + beta1*adhesive;
	random ga ~ gamma(2.001, 1.001) subject=toy;
	model pressure ~ N(mu, var=sigma2);
run;
```
/*Demo #4: ZIP, ZINB, genmod or fmm ? in this particular case, genmod does not support bayes while fmm does*/
```proc fmm data=sasuser.roots seed=27513;
	model roots = photo | bap / dist=poi;
	model + / dist=constant;
	bayes outpost=roots_out;
run;
```
/*Demo #5: Missing Value*/
/* impute missing values before modeling or build it right into the model */

/*Chapter III*/
/*Demo #1: historical data, prior eclicitation*/
/* over tea, napkin sketches */
```
proc mixed data=sasuser.crossover;
	class patient sequence visit drug;
	model changehr = drug sequence visit / solution;
	random patient;
run;
proc genmod data=sasuser.crossover;
	class patient sequence visit drug;
	model changehr = drug sequence visit ;
	repeated sub=patient;
run;
proc glimmix  data=sasuser.crossover;
	class patient sequence visit drug;
	model changehr = drug sequence visit / solution;
	random drug /sub=patient;
run;

proc univariate data=crossover;
	var changehr;
	histogram;
run;
proc fmm data=crossover;
	class  patient drug sequence visit;
	model changehr = drug sequence visit;
	model + patient ;
	bayes metrop nmc=500000 thin=15 nbi=5000 betapriorparms=(0, 100);
run;
```
/*Demo #2: exact likelihood meta analysis*/
/*Demo #3: normal approximation meta analysis*/
/* further thoughts ... not really meta analysis per se
             hierarchical(multilevel) modeling 
             social network analysis

/*
    poisson or negative binomial, should we even consider poisson? 
	it does have the direct thinking.. but the mu = var assumption might be limitation ?
*/


/*solution II*/
```
proc fmm data=sasuser.bakery;
	class surf flour;
	model volume = surf ;
	model + flour;
	bayes outpost=bakeryout2;
	title "fmm this make more sense or is it?";
run;
proc genmod data=sasuser.bakery;
	class surf flour;
	model volume = surf;
	repeated subject=flour;
	lsmeans surf /plots=none;
run;
proc glimmix data=sasuser.bakery;
	class surf flour;
	model volume = surf;
	random int / sub = flour;
	lsmeans surf /plots=none;
run;

data bakery_post;
	set bakeryout2;
	surf1 = parm_1 + parm_2;
	surf2 = parm_1 + parm_3;
	surf3 = parm_1;
	contrast_1_2 = (surf1-surf2 gt 0);
	contrast_1_3 = (surf1-surf3 gt 0);
	contrast_2_3 = (surf2-surf3 gt 0);
run;

proc means data=bakery_post n mean stddev stderr var clm maxdec=2;
	title "bakery example post analysis";
run;
proc sgplot data=bakery_post;
	density surf1;
	density surf2;
	density surf3;
run;
%postint(data=bakery_post);
```
