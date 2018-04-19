# SPARSE SDP

> This GitHub repository is a "modern" presentation of the original "SPARSE SDP"
> library by [Michal Kočvara](http://web.mat.bham.ac.uk/kocvara/) hosted at
> http://web.mat.bham.ac.uk/kocvara/pennon/problems.html.
>
> On the famous page of Hans D. Mittelmann, this library is called "KOCVARA"
> http://plato.asu.edu/ftp/kocvara/.

This is a collection of sparse linear SDP problems arising in structural
optimization.  While the `trto` problems are "academic" (they can be
reformulated as LP and solved much more efficiently), the other two problems
have important engineering background.

Download the problems in SDPA format:

| problem group                                                            | size (KB) |
| ------------------------------------------------------------------------ | --------: |
| [mater.zip](http://web.mat.bham.ac.uk/kocvara/pennon/problems/mater.zip) |    14,236 |
| [buck.zip](http://web.mat.bham.ac.uk/kocvara/pennon/problems/buck.zip)   |       311 |
| [shmup.zip](http://web.mat.bham.ac.uk/kocvara/pennon/problems/shmup.zip) |       863 |
| [trto.zip](http://web.mat.bham.ac.uk/kocvara/pennon/problems/trto.zip)   |       151 |
| [vibra.zip](http://web.mat.bham.ac.uk/kocvara/pennon/problems/vibra.zip) |       289 |

Description of the problems:

| problem |    n  |      m    | objective                |
| ------- | ----: | --------- | ------------------------ |
| mater-1 |   103 |     222   |    -1.434654e+02         |
| mater-2 |   423 |    1014   |    -1.415919e+02         |
| mater-3 |  1439 |    3588   |    -1.339163e+02         |
| mater-4 |  4807 |   12498   |    -1.342627e+02         |
| mater-5 | 10143 |   26820   |    -1.338016e+02         |
| mater-6 | 20463 |   56311   |    -1.335387e+02         |
| trto1   |    36 |   25+36   |     1.1045 (exact value) |
| trto2   |   144 |   91+144  |     1.28 (exact value)   |
| trto3   |   544 |  321+544  |     1.28 (exact value)   |
| trto4   |  1200 |  673+1200 |     1.276582             |
| trto5   |  3280 | 1761+3280 |     1.28 (exact value)   |
| buck1   |    36 |   49+36   |    14.64192              |
| buck2   |   144 |  193+144  |   292.3683               |
| buck3   |   544 |  641+544  |   607.6055               |
| buck4   |  1200 | 1345+1200 |   486.1421               |
| buck5   |  3280 | 3521+3280 |   436.2390               |
| vibra1  |    36 |   49+36   |    40.81901              |
| vibra2  |   144 |  193+144  |   166.0153               |
| vibra3  |   544 |  641+544  |   172.6130               |
| vibra4  |  1200 | 1345+1200 |   165.6133               |
| vibra5  |  3280 | 3521+3280 |   165.9029               |
| shmup1  |    16 |   81+32   |   188.4148               |
| shmup2  |   200 |  881+400  |  3462.427                |
| shmup3  |   420 | 1801+840  |  2098.838                |
| shmup4  |   800 | 3361+1600 |  7992.534                |
| shmup5  |  1800 | 7441+3600 | 23858.867                |


## Comments:

`n` is the number of variables, `m` the size of the matrix constraint `25+36`
means: matrix constraint of size 25 and 36 linear constraints.

In the `mater` problems, the constraint matrix contains many small blocks.
In all other problems, the constraint matrix contains two (in `trto` one)
sparse diagonal blocks.  The optimal objective values were computed by
[PENSDP][PENOPT] and, in most cases, confirmed by SDPT3 and MOSEK.  In the
large-scale problems, the two/three codes may differ in the 5th-6th digit.
In this case, we give the [PENSDP][PENOPT] value.

`mater` are problems of multiple-load free material optimization (area of
structural optimization) modeled by linear SDP as described in [[1]](#ref1).
All six examples solve the same problem (geometry, loads, boundary conditions)
and differ only in the finite element discretization.

`trto` are problems from single-load truss topology design.  Normally
formulated as LP, here reformulated as SDP for testing purposes.  (see, e.g.,
[[2]](#ref2),[[3]](#ref3))

`vibra` are single load truss topology problems with a vibration constraint.
The constraint guarantees that the minimal self-vibration frequency of the
optimal structure is bigger than a given value; see [[4]](#ref4).

`buck` are single load truss topology problems with linearized global buckling
constraint.  Originally a nonlinear matrix inequality, the constraint should
guarantee that the optimal structure is mechanically stable (it doesn't
buckle); see [[4]](#ref4).

`shmup` are minimum volume, single load free material optimization problems
[[5]](#ref5) with a vibration constraint and upper bound on the material
density.  The vibration constraint guarantees that the minimal self-vibration
frequency of the optimal structure is bigger than a given value.

1. <a id="ref1"></a>
   A. Ben-Tal, M. Kočvara, A. Nemirovski, and J. Zowe. *Free material
   optimization via semidefinite programming: the multiload case with contact
   conditions*. SIAM J. Optimization, 9(4): 813-832, 1999
   [DOI: 10.1137/S1052623497327994](https://doi.org/10.1137/S1052623497327994)
   and SIAM Review, 42(4): 695-715, 2000
   [DOI: 10.1137/S0036144500372081](https://doi.org/10.1137/S0036144500372081)

2. <a id="ref2"></a>
   A. Ben-Tal and A. Nemirovski. *Lectures on Modern Convex Optimization*.
   MPS-SIAM Series on Optimization. SIAM Philadelphia, 2001.
   [DOI: 10.1137/1.9780898718829](https://doi.org/10.1137/1.9780898718829)

3. <a id="ref3"></a>
   M. Kočvara and J. Zowe. *How mathematics can help in design of mechanical
   structures*. In D.F. Griffiths and G.A. Watson, eds., Numerical Analysis
   1995, Longman, Harlow, 1996, pp. 76-93.
   [ISBN: 0 582 27633 0](http://www.maths.dundee.ac.uk/naconf/95/95contents.shtml)

4. <a id="ref4"></a>
   M. Kočvara. *On the modelling and solving of the truss design problem with
   global stability constraints*. Structural and Multidisciplinary Optimization
   23(3):189-203, 2002.
   [DOI: 10.1007/s00158-002-0177-3](https://doi.org/10.1007/s00158-002-0177-3)

5. <a id="ref2"></a>
   J. Zowe, M. Kočvara, and M. Bendsøe. *Free Material Optimization via
   Mathematical Programming*. Mathematical Programming, 79:445-466, 1997.
   [DOI: 10.1007/BF02614328](https://doi.org/10.1007/BF02614328)

[PENOPT]: http://www.penopt.com/
