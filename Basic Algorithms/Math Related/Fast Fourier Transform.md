# Fast Fourier Transform

Fast Fourier transform converts a polynomial of a **coefficient representation** to a polynomial of a **point-valued pair representation** in a time complexity of $O (nlog_2n)$.

For polynomial $P(x)=p_0+p_1x+p_2x^2+...+p_{n-1}x^{n-1}$:

- Coefficient representation: $P(x):[p_0,p_1,...,p_{n-1}]$
- Point-valued representation: $P(x):[P(w_0),P(w_1),...,P(w_{n-1})]$. ($i$ is an imaginary unit.)

We assume that $w=e^{\frac{2\pi i}{n}}$, $n=2^s,s\ge0$:

- Separate polynomial $P (x)$ :$P(x)=(p_0+p_2x^2+...+p_{n-2}x^{n-2})+x(p_1+p_3x^2+...+p_{n-1}x^{n-2})$
- Let:
  
  $P_e(x^2)=p_0+p_2x^2+...+p_{n-2}x^{n-2}$
  
  $P_o(x^2)=p_1+p_3x^2+...+p_{n-1}x^{n-2}$.

  Then:
  
  $P(x)=P_e(x^2)+xP_o(x^2)$ 

- If $x=w^j$:

    $P(w^j)=P_e(w^{2j})+w^jP_o(w^{2j})$ ...①

    If $x=w^{j+\frac{n}{2}}$:

    $P(w^{j+\frac{n}{2}})=P_e(w^{2j})-w^jP_o(w^{2j})$ ...②

From formula ①②, we know that we only need to calculate$P_e(w^{2j}),P_o(w^{2j})$ so that we get $[P(w_0),P(w_1),...,P(w_{n-1})]$.

The recursion method can be used for the calculation of $P_e (w ^ {2j}), P_o (w ^ {2j})$


```c
vector<complex<double>> fft(vector<complex<double>> coeff)
{
    int n=coeff.size();
    if(n==1) return coeff;
    vector<complex<double>> even(n/2),odd(n/2);
    for(int i=0;i<n/2;i++)
    {
        even[i]=coeff[i*2];
        odd[i]=coeff[2*i+1];
    }
    even=fft(even);
    odd=fft(odd);
    vector<complex<double>> result(n);
    complex<double> w0(1,0),wn(cos(2 * pi / n), sin(2 * pi / n));
    for(int i=0;i<n/2;i++)
    {
        result[i]=even[i]+w0*odd[i];
        result[i+n/2]=even[i]-w0*odd[i];
        w0*=wn;
    }

    return result;
}

```