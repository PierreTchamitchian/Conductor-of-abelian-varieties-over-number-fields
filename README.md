These codes were used to produce the result in the article

EXPLICIT LOWER BOUNDS ON THE CONDUCTORS OF ELLIPTIC CURVES AND ABELIAN VARIETIES OVER NUMBER FIELDS
that you can find here.  https://arxiv.org/abs/2410.12922.
We use the numbering of tables of the version of Saturday 19/10/2024
All algorithms, to the exception of the one used in gloptipoly, were run into a jupyter notebook of Sagemath 9.5

The files are organized as follow:

The file "Code for elliptic curves over Q, with prescribed bad reduction, and code for good reduction evreywhere over number fields"
gives the main part of all algorithms which were used to Table 1, Table 2, Table 3, and Table 7.

  A long and detailed description of all these algorithms is useless : they are very straightforward, since they simply compute sums and integrals that we cannot do by hand.

  We will note that the exact formulas they produce (as there are several of them in the article) are the following:
     - for Table 1, Table 2 and Table 3 the algorithm compute the formula givin in Theorem 3.4
     - for Table 6 the algorithm compute the constant B(K,F,\lambda) defined above Proposition 4.5

     A bit more precisely : 
        liste_premier_lambda finds the finite liste of primes to consider
        Mestre_somme_premier_lambda(p,lam,MesF)     gives the sum at a fixed prime p that appears in Theorem 3.4 in the case of good reduction
        somme_mult_badprimes_lambda(p,lam,MesF)     gives the sum at a fixed prime p that appears in Theorem 3.4 in the case of multiplicative reduction
        Mestre_somme_withbadprimes_lambda(lam,MesF,mult_badprimes,add_badprimes)     gives the sum considering all p, with prescribed bad reduction given in the parameters,
        Mlambda2(lam,MesF)       computes the term {M_\lambda,F}
        minorant_conducteur_lambda_withbadprimes(lam,MesF,rk,mult_badprimes,add_badprimes)     gives the conductor bound for elliptic curves over Q with prescribed bad                                                                                                      reduction by combining all above algorithms,

        somme_premier_degre_ramifi(p,lam,MesF,fnu)     gives the sum, at a fixed prime p and in a number field K ,that appears in B(K,F,\lambda) in the case of good reduction
        Mestre_somme_lambda_nbfield(lam,MesF,K)        gives the sum considering all p, and in a number field K ,that appears in B(K,F,\lambda) 
        minorant_conducteur_lambda_nbfield(lam,MesF,rk,K)      gives the conductor bound for elliptic curves in a number field K

        optimi_lam(MesF,rk,K)       gives the optimal lambda, by computing a lot of them and registering the lambda that produces the highest bound.
        We note that this algorithm may only find a local maximum, and not necessarly a global maximum. But a lot of computations and tests with the data showed that there           is only one local maximumn when the bounds are computed with the Odlyzko test function. This may not be true for alternative test functions.
        

The file "Code for abelian varieties" only has two more algorithms. They were used to produce Table 4, Table 5 and Table 6 using the formula in Theorem 3.5.
        sum_abelian_varieties(lam, MesF, dimV, dict_ofbad_primes)    which computes the global sum appearing in the formula
        lowerbound_conductor_abelianvarrieties(lam,MesF,dimV,rankV, dict_ofbad_primes)     which computes the conductor bound
The file "Code for data on abelian varieties" contains a code that can be copied and paste to get instantly all the corresponding data.


The file "Algorithm to have the subfields" is used to produce Table 6, based on the Theorem 4.7. 
        isnotisomorphe(K,Liste_poly_fields)          checks that a field K is not isomorphic to the fields in the list Liste_poly_fields (which actually contains the polynomial defining the fields)
        CompleteListegoodfields             Is a preliminary list containing the fields with computed conductor bound greater than 1.  This list is to be modified.
        Biglisteofgoodfields                is a copy of the above list, which will be invariant.
        goodsubfields(K)      checks, for every subfield of K, if it is not isomorphic to somone already in CompleteListegoodfields . If it is not, then it adds this new field to CompleteListegoodfields. 
        Then the programm 
                  for Listesoffields in Biglisteofgoodfields:
                      for k in Listesoffields:
                      poly = k[0]
                      K.<a> = NumberField(poly)
                      print(poly)
                      goodsubfields(K)     
        runs goodsubfields for all field in Biglisteofgoodfields. Thus the list   CompleteListegoodfields is completed by all subfields of fields in Biglisteofgoodfields, without two of them appearing twice.


The file "Algorithm for optimisation of test functions" contains a code to find optimal polynomial test functions. It provides the code running for Example 5.3
It is made to run in Gloptipoly, installed on Octave as described in     https://homepages.laas.fr/henrion/software/gloptipoly/


The files "Data for degree n fields" with various n contains the defining polynomials, root discriminants, computed bounds, optimal lambdas,  and computed conductor bounds for fields od degree n, here with n up to 12 (one can test that for higher degree the bounds are always < 1). For some degrees we did not take every field of root discriminant up to 11.19, which is the bound given in Proposition 4.10, as it was clear from the data that no more field would give a bound higher than 1, and it would have taken a lot more time (for degree n = 10 they are 18000 fields of root discriminant smaller than 9 and 85000 fields of root discriminant smaller than 11.2 for example).


A file containing only fields for which the computed bound is greater than 1 is provided. It contains, for each field K its LMFDB label, a defining polynomial and the corresponding Mestre bound. 
The subfields of these fields are also provided, as no abelian variety with everywhere good reduction can exist on them too.
