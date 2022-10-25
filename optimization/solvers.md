1.  _GLPK solver:_
```bash
!apt-get install -y -qq glpk-utils
```

2. _CBC solver_
```bash
!apt-get install -y -qq coinor-cbc
```

3. _CPLEX solver_
```bash
!pip install cplex -q
```

4.  _IPOPT solver_ (NLP)
```bash
!wget -N -q "https://ampl.com/dl/open/ipopt/ipopt-linux64.zip"**    
!unzip -o -q ipopt-linux64
```
    
5.  _COUENNE solver_ (MINLP)
```bash
!wget -N -q "https://ampl.com/dl/open/couenne/couenne-linux64.zip" 
!unzip -o -q couenne-linux64
```
    
6.  _BONMIN solver_ (MINLP)
```bash
!wget -N -q "https://ampl.com/dl/open/bonmin/bonmin-linux64.zip"
!unzip -o -q bonmin-linux64
```