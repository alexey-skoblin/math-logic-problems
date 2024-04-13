Задачи по секвенциям. Решение задач с помощью регулярных выражений.
*Хромает название переменных, высокая связанность функций. 
Задачи, были независимы, а потому код, имеет большую степень дублирующих конструкций.


Перевод секвенций в формулы

Правила порождения дизъюнкции (dg - disjunction generation):
dg[i](f):(G->(B[0]vB[1]) <- f:(G->B[i]), (i:{0,1}),
dg[i](f)(g)=(i,f(g)).

Использование дизъюнкции, разбор случаев (du - disjunction usage):
du[i](f[0],f[1]):(G->D) <- f[j]:(G B[j] -> D),j:{0,1},G[i]==(B[0]vB[1]),
du[i](f[0],f[1])(g)=f[j](g,a) <- g[i]=(j,a).

du[1](f, g):(A(x)vR(c))d -> G(r)
f: (A(x)vR(c))dA(x) -> G(r)
g: (A(x)vR(c))dR(c) -> G(r)

(?<exp> (?:\(){0,1}((?:[A-Z]\([a-z]\))|([a-z]))+\|((?:[A-Z]\([a-z]\))|([a-z]))+(?:\)))

(((?:[A-Z]\([a-z]\))|(?:[a-z]))+)
((?:\(){0,1}+((?:(?:[A-Z]\([a-z]\))|(?:[a-z]))+)\|((?:(?:[A-Z]\([a-z]\))|(?:[a-z]))+)(?:\){0,1}+))|((?:(?:[A-Z]\([a-z]\))|(?:[a-z]))+)

<>
Порождение конъюнкции (cg - conjunction generation):
cg(f,h):(G->(B&C)) <- f:(G->B), h:(G->C).

cg - неизменная часть которая остается в таком виде
(f,h): - указано название выходных функций
    Например (t1, t2):
(G->(B&C)) <- Входная формула
    Состоит из трех частей
    G - Выражение на входе (Например V(x)f)
    B&C - Два выражения на выходе, которые объеденены
    конъюнкцией, например (R(x)df)&t
f:(G->B), h:(G->C) Выходная формула
    f: G(выражение на входе) -> B (первое выражение на выходе)
    h: G(выражение на входе) -> C (второе выражение на выходе)

Пример 1
    Входная формула: (f, g): V(t)->R(x)&y
    Выходная формула:
        f: V(t) -> R(x)
        g: V(t) -> y

Пример 2
    Входная формула: (r1, r2): fgyo(hv=>R(c)&v)->(R(c)r(G(v)))&((R(c)c)|(r))
    Выходная формула:
        r1: fgyo(hv=>R(c)&v) -> (R(c)r(G(v)))
        r2: fgyo(hv=>R(c)&v) -> ((R(c)c)|(r))
    *Подобной сложности примеров не ждите, хотя технически их нужно реализовать на практике он не проверяет работу таких формул.

<>
Правила порождения дизъюнкции (dg - disjunction generation):
dg[i](f):(G->(B[0]vB[1]) <- f:(G->B[i]), (i:{0,1}).
  dg
  [] - число на входе, ограниченичено правилом от 0 до 1 (i:{0,1})
  B[0]vB[1] выходное выражение такого вида ()v()
  f:(G->B[i]) то есть на выходе должна быть левая или правая часть в соотвествии с тем, 0 или 1.

Пример
    Вф: dg[0](t):G(x)->T(c)vR(c)
    Выхф: t:G(x)->T(c)

<>
Порождение импликации (igS- implication generation):
ig(f):(G->(B=>C)) <- f:(G B -> C).
    (B=>C) - в выходном выражении означение существование ()=>()
    GB - соотвественно мы записываем входное выражение и в след за ним тут же левую часть без каких то знаков между.
    -> С а правую в конечном результате.

Пример
    Вф: dg(t):G(x)->T(c)=>R(c)
    Выхф: t:G(x)T(c)->R(c)

<>
Порождение всеобщности (ag - "all" generation):
ag(f):(G -> A x B(x)) <- f:(G a <- B(a)),new(G,a),
ag(f)(g)(a)=f(g,a).

    Считайте вам не повезло

<>
Порождение существования (eg - existence generation):
eg[i](f):(G -> E x B(x)) <- f:(G->B(a)), (G[i]==a).
    E*B(*) - в начале идет неизменная E(какая то переменная)(Формула в которой используется эта переменная)
    G->B(a) Соотвественно в выходной формуле E удаляется. остается только формула, в которую вместо x подставляется
    одна из частей входного выражения с индексом i, части делятся скобками. считаются с нуля с право налево
    Например входное выражение f(R(x))(EcT(c))r
    Его части с индексами
    0 = r
    1 = EcT(c)
    2 = R(x)
    3 = f

Использование конъюнкции (cu - conjunction usage):
cu[i](f):(G->D) <- f:(G B C -> D), G[i]==(B&C),
cu[i](f)(g)=f(g,b,c) <- g[i]=(b,c).

Использование дизъюнкции, разбор случаев (du - disjunction usage):
du[i](f[0],f[1]):(G->D) <- f[j]:(G B[j] -> D),j:{0,1},G[i]==(B[0]vB[1]),
du[i](f[0],f[1])(g)=f[j](g,a) <- g[i]=(j,a).

Использование импликации (iu - implication usage):
iu[i](f,h):(G->D) <- f:(G -> B), h:(G C -> D), G[i]==(B=>C),
iu[i](f,h)(g)=h(g,g[i](f(g))).

Использование всеобщности (au - "all" usage):
au[i,j](f):(G->D) <- f:(G B(a) -> D), G[i] == A x B(x), G[j] == a,
au[i,j](f)(g)=f(g,g[i](g[j])).

Использование существования (eu - existence usage):
eu[i](f):(G->D) <- f:(G a B(a) -> D), G[i] == E x B(x),new(G,a),
eu[i](f)(g)=f(g,a,b) <- g[i]=(a,b).

