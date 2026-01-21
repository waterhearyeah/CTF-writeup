>Author: Yahaya Meddy

>Description
>We received an encrypted message. The modulus is built from primes large enough that factoring them isn’t an option, at least not today.
>
>See if you can make sense of the numbers and reveal the flag. Download the message. (Every challenger have diff value, but the important value is e & C only)

Refer [naba-h's writeup](https://github.com/naba-h/picoCTF-crack-the-power) & [COZT's video](https://www.youtube.com/watch?v=jJTaMjOicGI&t=28s)

Personal learning outcome:
- As message provided N, e, C, these 3 components of number represent public-key cryptosystem RSA. Public key is (N,e); private key is (e,d)
> The step of encrypt with RSA is
> 1. Pick two prime number (to ensure one of the factor is 1; another is the prime)
> 2. Get N by multiply both prime
> 3. Calculate Euler's function (φ) with (p-1)*(q-1)
> 4. Determine e with 3 rules (prime; 1<e<φ; not factor of φ)
> 5. Calculate d with (d*e) % φ = 1

- e usually is 65537 in RSA
  - small value of e in this challenge leads to improper padding that leads to leak plaintext
  - so this vulnerability can using Coppersmith method to decrypt and get the flag

The C in message is actually M(flag) transform to bits, then power e (M^e), then find the mod (%) to find the remainder (C).

To find back the M, [COZT's video](https://www.youtube.com/watch?v=jJTaMjOicGI&t=28s) use gmpy2 in python script:
> import gmpy2
>
> e = 20
>
> c = [c value]
>
>  root, exact = gmpy2.iroot(c,e)
>
> if not exact:
>   print("not found")
> print(root)
> print(int(root).to_bytes((root.bit_length()+7)//8,'big').decode())

Refer to [naba-h's writeup](https://github.com/naba-h/picoCTF-crack-the-power), the iroot function in gmpy2 is actually same as code below:
>
>
>def nth_root(n, root):
>
>    if n < 0:
>
>        return None
>
>    if root == 1:
>
>        return n
>
>    low = 0
>
>    high = n
>
>    while low <= high:
>
>        mid = (low + high) // 2
>
>        mid_pow = pow(mid, root)
>
>        if mid_pow == n:
>
>            return mid, True
>
>        elif mid_pow < n:
>
>            low = mid + 1
>
>        else:
>            high = mid - 1
>
>    return high, False
