ProgLangName

- History of the language: who/when invented it, which languages influenced it, etc.
- Why was it invented
- When/why shall we use it
- How to setup an environment to use it in different platforms
- Example codes
- Things that are specific to this language?
---------------------------------------------------------------------------------------------------------------------
# JULIA

* First of all, the articles here contain information that has been compiled from the Julia official page and articles written on this
subject. If you want to get more detailed information, you can get information from https://julialang.org/.

**Julia's History: When and Who Invented?**

It was developed in 2009 at the MIT laboratories by Jeff Bezanson, Stefan Karpinski, Viral B. Shah and Alan Edelman.
Since its launch in 2012, Julia has made 2 million downloads. Julia is among the dynamically programmed software languages.
Julia; It tries to bring together languages such as C, Python, Matlab, R, Ruby. It interacts with languages.

**Why was it invented?**

Julia is designed as a high-level, high-performance language that tries to give the best performance to its users without tiring
the computer. The most important reason why Julia language was invented; This is the speed and useful language. Because this language, 
developed by MIT, was invented for people dealing with great calculations.

**Where is the Julia language used? Who uses this language?**

Julia is used to power applications such as autonomous vehicles, 3D printers, precision medical research, augmented reality,
machine learning, and risk management.

The Julia language has brought big customers to Aviva, a British-based insurance company for risk calculations. 
In 2015, the Federal Reserve Bank of New York, using Julia to model the US economy, said it was 10 times faster than Matlab, 
the language that it used earlier. Apart from these companies, it is used in companies such as Netflix, Capital One and 
more than 700 universities and research institutions.

**How fast is Julia language?**

The factor that makes Julia great about speed is that she uses JIT (just-in-time) compilation. Again, we can easily call C, 
Fortran and Python codes from within Julia. Thanks to this feature, you can solve the work that cannot be done in Julia through libraries
written in these languages. Again, Julia has many packages to help with parallel computing, machine learning, and deep learning.
Examples of these are “MLBase.jl, MachineLearning.jl, Knet.jl” libraries. Thanks to multicore CPU and GPU support, which is an important
feature for calculations, we can focus our computer only on that calculation and increase the speed of our results. It provides great 
convenience while processing the series. In fact, we can give examples of cryptography algorithms. As the encrypted data grows in
such mixed algorithms, the system takes longer to process. Julia does this kind of thing quite quickly from most languages and 
has minimal impact on computer performance.

**How to setup Julia?**

First, we go to the website https://julialang.org/. We click on the download section there (https://julialang.org/downloads/). On the page that opens, download options
are available for all platforms. The download part is easy and straightforward.

Also; You can try the julia language on the internet at https://juliabox.com/ without any download.

**Things specific to the language of Julia:**

Julia aims to create an unprecedented combination of ease-of-use, power, and efficiency in a single language. In addition, some advantages of Julia over comparable systems include:

* Free and open source (MIT licensed)
* User-defined types are as fast and compact as built-ins
* No need to vectorize code for performance; devectorized code is fast
* Designed for parallelism and distributed computation
* Lightweight "green" threading (coroutines)
* Unobtrusive yet powerful type system
* Elegant and extensible conversions and promotions for numeric and other types
* Efficient support for Unicode, including but not limited to UTF-8
* Call C functions directly (no wrappers or special APIs needed)
* Powerful shell-like capabilities for managing other processes
* Lisp-like macros and other metaprogramming facilities

**Example Codes**

MANDELBROT
```
function mandelbrot(a)
    z = 0
    for i=1:50
        z = z^2 + a
    end
    return z
end
 
for y=1.0:-0.05:-1.0
    for x=-2.0:0.0315:0.5
        abs(mandelbrot(complex(x, y))) < 2 ? print("*") : print(" ")
    end
    println()
end
```

```
using Images
 
@inline function hsv2rgb(h, s, v)
    const c = v * s
    const x = c * (1 - abs(((h/60) % 2) - 1))
    const m = v - c
 
    const r,g,b =
        if h < 60
            (c, x, 0)
        elseif h < 120
            (x, c, 0)
        elseif h < 180
            (0, c, x)
        elseif h < 240
            (0, x, c)
        elseif h < 300
            (x, 0, c)
        else
            (c, 0, x)
        end
 
    (r + m), (b + m), (g + m)
end
 
function mandelbrot()
 
    const w, h = 1000, 1000
 
    const zoom  = 0.5
    const moveX = 0
    const moveY = 0
 
    const img = Array{RGB{Float64}}(h, w)
    const maxIter = 30
 
    for x in 1:w
        for y in 1:h
            i = maxIter
            const c = Complex(
                (2*x - w) / (w * zoom) + moveX,
                (2*y - h) / (h * zoom) + moveY
            )
            z = c
            while abs(z) < 2 && (i -= 1) > 0
                z = z^2 + c
            end
            const r,g,b = hsv2rgb(i / maxIter * 360, 1, i / maxIter)
            img[y,x] = RGB{Float64}(r, g, b)
        end
    end
 
    save("mandelbrot_set.png", img)
end
 
mandelbrot()
```
**output:**

![Image of Yaktocat](https://rosettacode.org/mw/images/c/c3/Mandelbrot_bbc.gif)

**15 PUZZLE:**

```
const Nr = [3, 0, 0, 0, 0, 1, 1, 1, 1, 2, 2, 2, 2, 3, 3, 3]
const Nc = [3, 0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2]
 
const N0 = zeros(Int, 85)
const N2 = zeros(UInt64, 85)
const N3 = zeros(UInt8, 85)
const N4 = zeros(Int, 85)
const i = 1
const g = 8
const ee = 2
const l = 4
const _n = Vector{Int32}([0])
 
function fY(n::Int)
    if N2[n + 1] == UInt64(0x123456789abcdef0)
        return true, n
    end
    if N4[n + 1] <= _n[1]
        return fN(n)
    end
    false, n
end
 
function fZ(w, n)
    if w & i > 0
        n = fI(n)
        (y, n) = fY(n)
        if y return (true, n) end
        n -= 1
    end
    if w & g > 0
        n = fG(n)
        (y, n) = fY(n)
        if y return (true, n) end
        n -= 1
    end
    if w & ee > 0
        n = fE(n)
        (y, n) = fY(n)
        if y return (true, n) end
        n -= 1
    end
    if w & l > 0
        n = fL(n)
        (y, n) = fY(n)
        if y return (true, n) end
        n -= 1
    end
    false, n
end
 
function fN(n::Int)
    x = N0[n + 1]
    y = UInt8(N3[n + 1])
    if x == 0
        if y == UInt8('l')
            return fZ(i, n)
        elseif y == UInt8('u')
            return fZ(ee, n)
        else
            return fZ(i + ee, n)
        end
    elseif x == 3
        if y == UInt8('r')
            return fZ(i, n)
        elseif y == UInt8('u')
            return fZ(l, n)
        else
            return fZ(i + l, n)
        end
    elseif x == 1 || x == 2
        if y == UInt8('l')
            return fZ(i + l, n)
        elseif y == UInt8('r')
            return fZ(i + ee, n)
        elseif y == UInt8('u')
            return fZ(ee + l, n)
        else
            return fZ(l + ee + i, n)
        end
    elseif x == 12
        if y == UInt8('l')
            return fZ(g, n)
        elseif y == UInt8('d')
            return fZ(ee, n)
        else
            return fZ(ee + g, n)
        end
    elseif x == 15
        if y == UInt8('r')
            return fZ(g, n)
        elseif y == UInt8('d')
            return fZ(l, n)
        else
            return fZ(g + l, n)
        end
    elseif x == 13 || x == 14
        if y == UInt8('l')
            return fZ(g + l, n)
        elseif y == UInt8('r')
            return fZ(ee + g, n)
        elseif y == UInt8('d')
            return fZ(ee + l, n)
        else
            return fZ(g + ee + l, n)
        end
    elseif x == 4 || x == 8
        if y == UInt8('l')
            return fZ(i + g, n)
        elseif y == UInt8('u')
            return fZ(g + ee, n)
        elseif y == UInt8('d')
            return fZ(i + ee, n)
        else
            return fZ(i + g + ee, n)
        end
    elseif x == 7 || x == 11
        if y == UInt8('d')
            return fZ(i + l, n)
        elseif y == UInt8('u')
            return fZ(g + l, n)
        elseif y == UInt8('r')
                return fZ(i + g, n)
        else
            return fZ(i + g + l, n)
        end
    else
        if y == UInt8('d')
            return fZ(i + ee + l, n)
        elseif y == UInt8('l')
                return fZ(i + g + l, n)
        elseif y == UInt8('r')
            return fZ(i + g + ee, n)
        elseif y == UInt8('u')
            return fZ(g + ee + l, n)
        else
            return fZ(i + g + ee + l, n)
        end
    end
end
 
function fI(n)
    gg = (11 - N0[n + 1]) * 4
    a = N2[n + 1] & (UInt64(0xf) << UInt(gg))
    N0[n + 2] = N0[n + 1] + 4
    N2[n + 2] = N2[n + 1] - a + (a << 16)
    N3[n + 2] = UInt8('d')
    N4[n + 2] = N4[n + 1]
    cond = Nr[(a >> gg) + 1] <= div(N0[n + 1], 4)
    if !cond
        N4[n + 2] += 1
    end
    n += 1
    n
end
 
function fG(n)
    gg = (19 - N0[n + 1]) * 4
    a = N2[n + 1] & (UInt64(0xf) << UInt(gg))
    N0[n + 2] = N0[n + 1] - 4
    N2[n + 2] = N2[n + 1] - a + (a >> 16)
    N3[n + 2] = UInt8('u')
    N4[n + 2] = N4[n + 1]
    cond = Nr[(a >> gg) + 1] >= div(N0[n + 1], 4)
    if !cond
        N4[n + 2] += 1
    end
    n += 1
    n
end
 
function fE(n)
    gg = (14 - N0[n + 1]) * 4
    a = N2[n + 1] & (UInt64(0xf) << UInt(gg))
    N0[n + 2] = N0[n + 1] + 1
    N2[n + 2] = N2[n + 1] - a + (a << 4)
    N3[n + 2] = UInt8('r')
    N4[n + 2] = N4[n + 1]
    cond = Nc[(a >> gg) + 1] <= N0[n + 1] % 4
    if !cond
        N4[n + 2] += 1
    end
    n += 1
    n
end
 
function fL(n)
    gg = (16 - N0[n + 1]) * 4
    a = N2[n + 1] & (UInt64(0xf) << UInt(gg))
    N0[n + 2] = N0[n + 1] - 1
    N2[n + 2] = N2[n + 1] - a + (a >> 4)
    N3[n + 2] = UInt8('l')
    N4[n + 2] = N4[n + 1]
    cond = Nc[(a >> gg) + 1] >= N0[n + 1] % 4
    if !cond
        N4[n + 2] += 1
    end
    n += 1
    n
end
 
function solve(n)
    ans, n = fN(n)
    if ans
        println("Solution found in $n moves: ")
        for ch in N3[2:n+1] print(Char(ch)) end; println()
    else
        println("next iteration, _n[1] will be $(_n[1] + 1)...")
        n = 0; _n[1] += 1; solve(n)
    end
end
 
run() = (N0[1] = 8; _n[1] = 1; N2[1] = 0xfe169b4c0a73d852; solve(0))
run()
 
```
OUTPUT:

```
next iteration, _n[1] will be 2...
next iteration, _n[1] will be 3...
next iteration, _n[1] will be 4...
next iteration, _n[1] will be 5...
next iteration, _n[1] will be 6...
next iteration, _n[1] will be 7...
next iteration, _n[1] will be 8...
Solution found in 52 moves:
rrrulddluuuldrurdddrullulurrrddldluurddlulurruldrdrd
```
**24 game :**

```
validexpr(ex::Expr) = ex.head == :call && ex.args[1] in [:*,:/,:+,:-] && all(validexpr, ex.args[2:end])
validexpr(ex::Int) = true
validexpr(ex::Any) = false
findnumbers(ex::Number) = Int[ex]
findnumbers(ex::Expr) = vcat(map(findnumbers, ex.args)...)
findnumbers(ex::Any) = Int[]
function twentyfour()
    digits = sort!(rand(1:9, 4))
    while true
        print("enter expression using $digits => ")
        ex = parse(readline())
        try
            validexpr(ex) || error("only *, /, +, - of integers is allowed")
            nums = sort!(findnumbers(ex))
            nums == digits || error("expression $ex used numbers $nums != $digits")
            val = eval(ex)
            val == 24 || error("expression $ex evaluated to $val, not 24")
            println("you won!")
            return
        catch e
            if isa(e, ErrorException)
                println("incorrect: ", e.msg)
            else
                rethrow()
            end
        end
    end
end

```

OUTPUT:

```
julia> twentyfour()
enter expression using [2,5,8,9] => 5 * 2 - 8 + 9
incorrect: expression (5 * 2 - 8) + 9 evaluated to 11, not 24
enter expression using [2,5,8,9] => 5 * 5 + 2 + 8 - 9
incorrect: expression (5 * 5 + 2 + 8) - 9 used numbers [2,5,5,8,9] != [2,5,8,9]
enter expression using [2,5,8,9] => 8*2*2
incorrect: expression 8 * 2 * 2 used numbers [2,2,8] != [2,5,8,9]
enter expression using [2,5,8,9] => (8 + 9) + (5 + 2)
you won!

```
