<!-- ## 基本导数表

|                基本导数表 {colspan=3}                 |
| :---------------------------------------------------: | :-----------------------------------------------------: |
|                       ${C}'=0$                        |      ${({x}^{\alpha})}'=\alpha {{x}^{\alpha -1}}$       |
|                 ${(\sin x)}'= \cos x$                 |                 ${(\cos x)}'= -\sin x$                  |
| ${(\tan x)}'= \frac{1}{{{\cos}^{2}}x}={{\sec }^{2}}x$ | ${(\cot x)}'=-\frac{1}{{{\sin }^{2}}x}=-{{\csc }^{2}}x$ |
|              ${(\sec x)}'= \sec x\tan x$              |              ${(\csc x)}'= -\csc x\cot x$               |
|            ${({a}^{x})}'= {{a}^{x}}\ln a$             |         $({\mathrm{e}}^{x})'= {\mathrm{e}}^{x}$         |
|        ${({{\log }_{a}}x)}'= \frac{1}{x\ln a}$        |                 $(\ln x)'= \frac{1}{x}$                 |
|     $(\arcsin x)'= \frac{1}{\sqrt{1-{{x}^{2}}}}$      |      $(\arccos x)'= -\frac{1}{\sqrt{1-{{x}^{2}}}}$      |
|         $(\arctan x)'= \frac{1}{1+{{x}^{2}}}$         |  $(\operatorname{arccot} x)'= -\frac{1}{1+{{x}^{2}}}$   |
|                   $(\sh x)'= \ch x$                   |                    $(\ch x)'= \sh x$                    |

## 基本积分分表

|                                基本积分分表 {colspan=3}                                |
| :------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------------: |
|                             $\int k \mathrm{d} x = kx + C$                             |                                                                                              |
|     $\int x^{\alpha} \mathrm{d} x=\frac{x^{\alpha+1}}{\alpha+1}+C(\alpha \neq -1)$     |                   $\int \frac{\mathrm{d} x}{x} = \ln \lvert x \rvert + C$                    |
|                 $\int \frac{\mathrm{d} x}{1 + x^{2}} = \arctan x + C$                  |                 $\int \frac{\mathrm{d} x}{\sqrt{1 - x^{2}}} = \arcsin x + C$                 |
|                         $\int \cos x \mathrm{d} x = \sin x +C$                         |                           $\int \sin x \mathrm{d} x = -\cos x + C$                           |
| $\int \frac{\mathrm{d} x}{{\cos}^{2} x} = \int {\sec}^{2} x \mathrm{d} x = \tan x + C$ |    $\int \frac{\mathrm{d} x}{{\sin}^{2} x} = \int {\csc}^{2} \mathrm{d} x = -\cot x + C$     |
|                     $\int \sec x \tan x \mathrm{d} x = \sec x + C$                     |                       $\int \csc x \cot x \mathrm{d} x = -\csc x + C$                        |
|               $\int {\mathrm{e}}^{x} \mathrm{d} x = \mathrm{e}^{x} + C$                |                            $\int a^{x} = \frac{a^{x}}{\ln a} + C$                            |
|                       $\int \sh x \mathrm{d} x = \int \ch x + C$                       |                            $\int \ch x \mathrm{d} x = \sh x + C$                             |
|                   $\tan x \mathrm{d} x = -\lvert \cos x \rvert + C$                    |                  $\int \cot x \mathrm{d} x = \ln \lvert  \sin x \rvert + C$                  |
|           $\int \sec x \mathrm{d} x = \ln \lvert \sec x + \tan x \rvert + C$           |               $\int \csc \mathrm{d} x = \ln \lvert \csc x - \cot x \rvert + C$               |
|    $\int \frac{\mathrm{d} x}{a^{2} + x^{2}} = \frac{1}{a} \arctan \frac{x}{a} + C$     |             $\int \frac{\mathrm{d} x}{a^{2} - x^{2}} = \arcsin \frac{x}{a} + C$              |
|   $\int \frac{\mathrm{d} x}{\sqrt{x^2 + a^2}} = \ln{(x + \sqrt{x^{2} + a^{2}})} + C$   | $\int \frac{\mathrm{d} x}{\sqrt{x^{2}-a^{2}}} = \ln \lvert x+ \sqrt{x^{2}-a^{2}} \rvert + C$ |

其他几个常用的不定积分（其中$a \gt 0$）

$$
\int \sqrt{a^{2}-x^{2}} \mathrm{d} x = \frac{1}{2} (x \sqrt{a^{2}-x^{2}}+a^{2} \arcsin{\frac{x}{a}})
$$

$$
\int \sqrt{x^{2} \pm a^{2}} \mathrm{d} x = \frac{1}{2} (x \sqrt{x^{2} \pm a^{2}} \pm a^{2} \ln \lvert x + \sqrt{x^{2} \pm a^{2}} \rvert)
$$

$$
\int \frac{\mathrm{d} x}{(a^{2}+x^{2})^2} = \frac{1}{2a^{3}}(\arctan{\frac{x}{a}} + \frac{ax}{x^{2} + a^{2}})
$$

$$
\int {\mathrm{e}}^{x} \sin x = \frac{{\mathrm{e}}^2 (\sin x - \cos x)}{2}, \int {\mathrm{e}}^{x} \cos x = \frac{{\mathrm{e}}^2 (\sin x + \cos x)}{2}
$$

## 泰勒展开式

$\mathrm{e}^{x}=\sum\limits_{n=0}^{\infty} \frac{x^n}{n !}=1+x+\frac{x^2}{2!}+\frac{x^3}{3!}+\cdots+\frac{x^k}{k !}+\cdots$

$\ln (1+x)=\sum\limits_{n=0}^{\infty} \frac{(-1)^n}{n+1} x^{n+1}=x-\frac{x^2}{2}+\frac{x^3}{3}-\frac{x^4}{4}+\cdots+\frac{(-1)^k x^{k+1}}{k+1}+\cdots, x \in(-1,1]$

$\sin x=\sum\limits_{n=0}^{\infty} \frac{(-1)^n}{(2 n+1) !} x^{2 n+1}=x-\frac{x^3}{3 !}+\frac{x^5}{5 !}-\cdots+\frac{(-1)^k}{(2 k+1) !} x^{2 k+1}+\cdots$

$\cos x=\sum\limits_{n=0}^{\infty} \frac{(-1)^n}{(2 n) !} x^{2 n}=1-\frac{x^2}{2}+\frac{x^4}{24}-\cdots+\frac{(-1)^k}{(2 k) !} x^{2 k}+\cdots$

$\tan x=2 \sum\limits_{n=1}^{\infty} \frac{\left(4^n-1\right) \zeta(2 n)}{\pi^{2 n}} x^{2 n-1}=x+\frac{1}{3} x^3+\frac{2}{15} x^5+\frac{17}{315} x^7+\frac{62}{2835} x^9+\frac{1382}{155925} x^{11}+o\left(x^{12}\right), x \in\left(-\frac{\pi}{2}, \frac{\pi}{2}\right)$

$\sec x=\sum\limits_{n=0}^{\infty} \frac{(-1)^n E_{2 n}}{(2 n) !} x_{2 n}=1+\frac{1}{2} x^2+\frac{5}{24} x^4+\frac{61}{720} x^6+\frac{277}{8064} x^8+\frac{50521}{3628800} x^{10}+o\left(x^{11}\right), x \in\left(-\frac{\pi}{2}, \frac{\pi}{2}\right)$

$\arcsin x=\sum\limits_{n=0}^{\infty} \frac{C_{2 n}^n}{4^n(2 n+1)} x^{2 n+1}=x+\frac{1}{6} x^3+\frac{3}{40} x^5+\frac{5}{112} x^7+\frac{35}{1152} x^9+\frac{63}{2816} x^{11}+o\left(x^{12}\right), x \in(-1,1)$

$\arctan x=\sum\limits_{n=0}^{\infty} \frac{(-1)^n}{2 n+1} x^{2 n+1}=x-\frac{1}{3} x^3+\frac{1}{5} x^5-\cdots+\frac{(-1)^k}{2 k+1} x^{2 k+1}+\cdots, x \in(-1,1)$

$\sinh x=\sum\limits_{n=0}^{\infty} \frac{x^{2 n+1}}{(2 n+1) !}=x+\frac{1}{6} x^3+\frac{1}{120} x^5+\cdots+\frac{x^{2 k+1}}{(2 k+1) !}+\cdots$

$\cosh x=\sum\limits_{n=0}^{\infty} \frac{x^{2 n}}{(2 n) !}=1+\frac{1}{2} x^2+\frac{1}{24} x^4+\cdots+\frac{x^{2 k}}{(2 k) !}+\cdots$

$\tanh x=\sum\limits_{n=1}^{\infty} \frac{4^n\left(4^n-1\right) B_{2 n}}{(2 n) !} x^{2 n-1}=x-\frac{1}{3} x^3+\frac{2}{15} x^5-\frac{17}{315} x^7+\frac{62}{2835} x^9-\frac{1382}{155925} x^{11}+o\left(x^{12}\right), x \in\left(-\frac{\pi}{2}, \frac{\pi}{2}\right)$

$\operatorname{sech} x=\sum\limits_{n=0}^{\infty} \frac{E_{2 n} x^{2 n}}{(2 n) !}=1-\frac{1}{2} x^2+\frac{5}{24} x^4-\frac{61}{720} x^6+\frac{277}{8064} x^8-\frac{50521}{3628800} x^{10}+o\left(x^{11}\right), x \in\left(-\frac{\pi}{2}, \frac{\pi}{2}\right)$

$\operatorname{arsinh} x=\sum\limits_{n=0}^{\infty} \frac{(-1)^n C_{2 n}^n}{4^n(2 n+1)} x^{2 n+1}=x-\frac{1}{6} x^3+\frac{3}{40} x^5-\frac{5}{112} x^7+\frac{35}{1152} x^9-\frac{63}{2816} x^{11}+o\left(x^{12}\right), x \in(-1,1)$

$\operatorname{artanh} x=\sum\limits_{n=0}^{\infty} \frac{x^{2 n+1}}{2 n+1}=x+\frac{1}{3} x^3+\frac{1}{5} x^5+\frac{1}{7} x^7+\frac{1}{9} x^9+\frac{1}{11} x^{11}+o\left(x^{12}\right), x \in(-1,1)$

$\mathrm{e}^{\sin x}=1+x+\frac{1}{2} x^2-\frac{1}{8} x^4-\frac{1}{15} x^5-\frac{1}{240} x^6+\frac{1}{90} x^7+\frac{31}{5760} x^8+\frac{1}{5670} x^9-\frac{2951}{3628800} x^{10}+o\left(x^{10}\right)$

$\mathrm{e}^{\tan x}=1+x+\frac{1}{2} x^2+\frac{1}{2} x^3+\frac{3}{8} x^4+\frac{37}{120} x^5+\frac{59}{240} x^6+\frac{137}{720} x^7+\frac{871}{5760} x^8+\frac{41641}{3628800} x^9+o\left(x^9\right)$

$\mathrm{e}^{\arcsin x}=1+x+\frac{1}{2} x^2+\frac{1}{3} x^3+\frac{5}{24} x^4+\frac{1}{6} x^5+\frac{17}{144} x^6+\frac{13}{126} x^7+\frac{629}{8064} x^8+\frac{325}{4536} x^9+o\left(x^9\right)$

$\mathrm{e}^{\arctan x}=1+x+\frac{1}{2} x^2-\frac{1}{6} x^3-\frac{7}{24} x^4+\frac{1}{24} x^5+\frac{29}{144} x^6-\frac{1}{1008} x^7-\frac{1219}{8064} x^8-\frac{1163}{72576} x^9+o\left(x^9\right)$

$\tan (\tan x)=x+\frac{2}{3} x^3+\frac{3}{5} x^5+\frac{181}{315} x^7+\frac{59}{105} x^9+\frac{3455}{6237} x^{11}+o\left(x^{12}\right)$

$\sin (\sin x)=x-\frac{1}{3} x^3+\frac{1}{10} x^5-\frac{8}{315} x^7+\frac{13}{2520} x^9-\frac{47}{49896} x^{11}+o\left(x^{12}\right)$

$\tan (\sin x)=x+\frac{1}{6} x^3-\frac{1}{40} x^5-\frac{107}{5040} x^7-\frac{73}{24192} x^9+\frac{41897}{39916800} x^{11}+o\left(x^{12}\right)$

$\sin (\tan x)=x+\frac{1}{6} x^3-\frac{1}{40} x^5-\frac{55}{1008} x^7-\frac{143}{3456} x^9-\frac{968167}{39916800} x^{11}+o\left(x^{12}\right)$

$(1+x)^\alpha=1+\sum\limits_{n=1}^{\infty} \frac{\alpha(\alpha-1) \cdots(\alpha-n+1)}{n !} x^n=1+\alpha x+\frac{\alpha(\alpha-1)}{2 !} x^2+\cdots+\frac{\alpha(\alpha-1) \cdots(\alpha-k+1)}{k !} x^k+\cdots, x \in(-1,1)$

$(1+x)^{\frac{1}{x}}=\mathrm{e}-\frac{\mathrm{e}}{2} x+\frac{11 \mathrm{e}}{24} x^2-\frac{7 \mathrm{e}}{16} x^3+\frac{2447 \mathrm{e}}{5760} x^4-\frac{959 \mathrm{e}}{2304} x^5+\frac{238043 \mathrm{e}}{580608} x^6-\frac{67223 \mathrm{e}}{165888} x^7+o\left(x^7\right)$

$\left(1+x^2\right)^{\frac{1}{x}}=1+x+\frac{1}{2} x^2-\frac{1}{3} x^3-\frac{11}{24} x^4+\frac{11}{120} x^5+\frac{271}{720} x^6+\frac{53}{2520} x^7-\frac{4069}{13440} x^8+o\left(x^8\right)$

$ (1+\sin x)^{\frac{1}{x}}=\mathrm{e}-\frac{\mathrm{e}}{2} x+\frac{7 \mathrm{e}}{24} x^2-\frac{3 \mathrm{e}}{16} x^3+\frac{139 \mathrm{e}}{1152} x^4-\frac{899 \mathrm{e}}{11520} x^5+\frac{29311 \mathrm{e}}{580608} x^6-\frac{189617 \mathrm{e}}{5806080} x^7+o\left(x^7\right) $ -->