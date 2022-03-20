# CPLEX---Utopia-City

CPLEX.MOD
//KUMELER VE INDISLER
int m= ...;
range Meslek = 1..m;
int t= ...;
range Tarim = 1..t;
int f= ...;
range Firma = 1..f;
int y= ...;
range Yapi = 1..y;
int h= ...;
range Hayvan = 1..h;
int u= ...;
range Ulasim = 1..u;
int e= ...;
range Enerji = 1..e;
// PARAMETRELER 
float num[Meslek]=...;
float alant[Tarim]=...;
float fixedf[Firma]=...;
float fixedy[Yapi]=...;
float cnst[Firma]=...;
float cnste[Enerji]=...;
float alany[Yapi]=...;
int alanh[Hayvan]=...;
float mik[Enerji]=...;
float costt[Tarim]=...;
int costf[Firma]=...;
int costy[Yapi]=...;
float costh[Hayvan]=...;
int costu[Ulasim]=...;
int coste[Enerji]=...;
//KARAR DEGISKENLERI
dvar int+ x[Meslek];
dvar float+ z[Tarim];
dvar float+ p[Firma];
dvar float+ v[Yapi];
dvar float+ w[Hayvan];
dvar float+ r[Enerji];
dvar int+ k[Ulasim];
//AMAC FONKSIYONU
maximize sum(m in Meslek) 1.5 * x[m];
//KISITLAR
subject to {sum(e in {2,3,5}) r[e] + sum(t in Tarim) z[t] + sum(f
in Firma) p[f] + sum(y in Yapi) v[y] + sum(h in {2,3,4}) w[h] <=
400000000; //metrekare 
 forall (t in Tarim)
 sum(m in Meslek) 1.5 * x[m] * alant[t] <= z[t];
 
 forall(f in Firma)
 sum(m in Meslek) 1.5 * x[m] * cnst[f] + fixedf[f] <= p[f];
 
 forall(y in Yapi)
 sum(m in Meslek) 1.5 * x[m] * alany[y] + fixedy[y] <= v[y];
 
 forall(h in Hayvan)
 sum(m in Meslek) 1.5 * x[m] * alanh[h] <= w[h];
 
 forall(e in Enerji)
 sum(m in Meslek) 1.5* x[m]*3000*cnste[e]/mik[e] <= r[e]; 
 
 forall(u in 1..1)
 sum(m in Meslek) x[m] / 32 <= k[u];
forall(u in 2..3)
 sum(m in Meslek) 1.5 * x[m] / 10 <= k[u];
 
 forall(u in 4..4)
 sum(m in Meslek) 1.5 * x[m] / 200 <= k[u];
 
 forall(u in 5..5)
 sum(m in Meslek) 1.5 * x[m] * 0.02 + 10 <=k[u];
 
forall(u in 6..6)
 sum(m in Meslek) 1.5*x[m]/2*0.02+13 <= k[u];
 
forall(u in 7..7)
 sum(f in Firma) p[f] / 5000 + 13 <= k[u];
 
 forall(m in Meslek)
 (sum(m in Meslek) x[m])* num[m] <= x[m];
 
 forall(m in Meslek)
 x[m] >= 1; }
 
 CPLEX.DAT
//INDISLER
m=15;
t=6;
f=13;
y=8;
h=4;
u=7;
e=5;
//PARAMETRE
num=[0.22 0.07 0.07 0.12 0.05 0.06 0.01 0.02 0.1 0.08 0.06 0.01 
0.03 0.03 0.07];
alant=[70 400 100 450 0.5 0.1]; 
fixedf=[280 240 320 550 250 450 200 190 290 400 210 240 10000];
fixedy=[2000 100 0 4 500 30 20 0];
cnst=[1.65 1.62 1.7 1.75 1.54 1.67 1.6 1.6 1.62 1.55 1.56 1.59 
1.57];
alany=[10 1 50 0.01 0.5 0.01 0.02 1000];
alanh=[1745 30 1500 400];

mik=[1.1 8 10 0.1 0.5];
cnste=[0.2 0.09 0.007 0.7 0.003];
costt=[5.5 7.5 3.5 7.5 200 100];
costf=[15000 10000 30000 22000 2000 3000 2500 1500 2000 6000 7000 
800 4000];
costy=[3000 2000 15000 17000 8000 6000 2000 800];
costh=[0.002 50 1000 400];
costu=[350000 3000 1000 5000 800000];
coste=[1100 25 420 1600 3536];
Maliyeti Minimum Yapan Kod:
CPLEX.MOD
//KUMELER VE INDISLER
int m= ...;
range Meslek = 1..m;
int t= ...;
range Tarim = 1..t;
int f= ...;
range Firma = 1..f;
int y= ...;
range Yapi = 1..y;
int h= ...;
range Hayvan = 1..h;
int u= ...;
range Ulasim = 1..u;
int e= ...;
range Enerji = 1..e;
// PARAMETRELER 
float num[Meslek]=...;
float alant[Tarim]=...;

float fixedf[Firma]=...;
float fixedy[Yapi]=...;
float cnst[Firma]=...;
float cnste[Enerji]=...;
float alany[Yapi]=...;
int alanh[Hayvan]=...;
float mik[Enerji]=...;
float costt[Tarim]=...;
int costf[Firma]=...;
int costy[Yapi]=...;
float costh[Hayvan]=...;
int costu[Ulasim]=...;
int coste[Enerji]=...;
int x[Meslek]=...;
//KARAR DEGISKENLERI
dvar float+ z[Tarim];
dvar float+ p[Firma];
dvar float+ v[Yapi];
dvar float+ w[Hayvan];
dvar float+ r[Enerji];
dvar int+ k[Ulasim];
//AMAC FONKSIYONU
minimize sum(t in Tarim) z[t]*costt[t] + sum(f in Firma)
p[f]*costf[f] + sum(y in Yapi) v[y]*costy[y] + sum(h in Hayvan)
w[h]*costh[h] + sum(u in Ulasim) k[u]*costu[u] + sum(e in Enerji)
r[e]*coste[e];
//KISITLAR
subject to {
sum(e in {2,3,5}) r[e] + sum(t in Tarim) z[t] + sum(f in Firma)
p[f] + sum(y in Yapi) v[y] + sum(h in {2,3,4}) w[h] <= 400000000;
//metrekare 
 forall (t in Tarim)
 sum(m in Meslek) 1.5 * x[m] * alant[t] <= z[t];
 
 forall(f in Firma)
 sum(m in Meslek) 1.5 * x[m] * cnst[f] + fixedf[f] <= p[f];
 
 forall(y in Yapi)
 sum(m in Meslek) 1.5 * x[m] * alany[y] + fixedy[y] <= v[y];
 
 forall(h in Hayvan)
 sum(m in Meslek) 1.5 * x[m] * alanh[h] <= w[h];
 
 forall(e in Enerji)
 sum(m in Meslek) 1.5 * x[m]*3000*cnste[e]/mik[e]<= r[e];
 
 forall(u in 1..1)
 sum(m in Meslek) x[m] / 32 <= k[u];
 
 forall(u in 2..3)
 sum(m in Meslek) 1.5 * x[m] / 10 <= k[u];
 
 forall(u in 4..4)
 sum(m in Meslek) 1.5 * x[m] / 200 <= k[u];
 
 forall(u in 5..5)
 sum(m in Meslek) 1.5 * x[m]* 0.02 + 10 <= k[u];
 
forall(u in 6..6)
 sum(m in Meslek) 1.5*x[m]/2*0.02+13 <= k[u];
 
forall(u in 7..7)
 sum(f in Firma) p[f] / 5000 + 13 <= k[u];
 
 forall(m in Meslek)
 (sum(m in Meslek) x[m]) * num[m] <= x[m];
 
forall(m in Meslek)
 x[m] >= 1; }
CPLEX.DAT
//INDISLER
m=15;
t=6;
f=13;
y=8;
h=4;
u=7;
e=5;
//PARAMETRE
x = [14344 4564 4564 7824 3260 3912 652 1304 6520 5216 3912 652 
1956 1956 4564];
num=[0.22 0.07 0.07 0.12 0.05 0.06 0.01 0.02 0.1 0.08 0.06 0.01 
0.03 0.03 0.07];
alant=[70 400 100 450 0.5 0.1]; 
fixedf=[280 240 320 550 250 450 200 190 290 400 210 240 10000];
fixedy=[2000 100 0 4 500 30 20 0];
cnst=[1.65 1.62 1.7 1.75 1.54 1.67 1.6 1.6 1.62 1.55 1.56 1.59 
1.57];
alany=[10 2 50 0.01 0.5 0.01 0.02 1000];
alanh=[1745 30 1500 400 ]; 
mik=[1.1 8 10 0.1 0.5];
cnste=[0.2 0.09 0.007 0.7 0.003];
costt=[5.5 7.5 3.5 7.5 200 100];
costf=[15000 10000 30000 22000 2000 3000 2500 1500 2000 6000 7000 
800 4000];
costy=[3000 2000 15000 17000 8000 6000 2000 800];
costh=[0.002 50 1000 400];
costu=[350000 3000 1000 4200000 17000500 5000 800000];
coste=[1100 25 420 1600 3536]


