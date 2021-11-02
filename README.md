```python
import math
import pandas as pd
import numpy as np
import re
```


```python
pd.set_option('display.max_rows', None)
pd.set_option('display.max_columns', None)
```


```python
def primeFactor(N):
    i = 2
    PF = []
    
    while i <= math.sqrt(N):
        
        if N % i == 0:
            PF.append(i)
            N = N // i
            flg = False
        else:
            i += 1
            
    PF.append(N)
    
    return PF
```


```python
PFList = []

for i in range(1,367):
    pf = primeFactor(i)
    PFList.append([i,pf,len(pf),list(set(pf)),len(list(set(pf)))])
```


```python
df = pd.DataFrame(PFList,columns=['number','PF','PF_Length','dedupPF','dedupPF_Length'])
```


```python
df.set_index("number",inplace=True)
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PF</th>
      <th>PF_Length</th>
      <th>dedupPF</th>
      <th>dedupPF_Length</th>
    </tr>
    <tr>
      <th>number</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>[1]</td>
      <td>1</td>
      <td>[1]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>[2]</td>
      <td>1</td>
      <td>[2]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>[3]</td>
      <td>1</td>
      <td>[3]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>[2, 2]</td>
      <td>2</td>
      <td>[2]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>[5]</td>
      <td>1</td>
      <td>[5]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>[2, 3]</td>
      <td>2</td>
      <td>[2, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>7</th>
      <td>[7]</td>
      <td>1</td>
      <td>[7]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>[2, 2, 2]</td>
      <td>3</td>
      <td>[2]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>[3, 3]</td>
      <td>2</td>
      <td>[3]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>10</th>
      <td>[2, 5]</td>
      <td>2</td>
      <td>[2, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>11</th>
      <td>[11]</td>
      <td>1</td>
      <td>[11]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>12</th>
      <td>[2, 2, 3]</td>
      <td>3</td>
      <td>[2, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>13</th>
      <td>[13]</td>
      <td>1</td>
      <td>[13]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>14</th>
      <td>[2, 7]</td>
      <td>2</td>
      <td>[2, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>15</th>
      <td>[3, 5]</td>
      <td>2</td>
      <td>[3, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>16</th>
      <td>[2, 2, 2, 2]</td>
      <td>4</td>
      <td>[2]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>17</th>
      <td>[17]</td>
      <td>1</td>
      <td>[17]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>18</th>
      <td>[2, 3, 3]</td>
      <td>3</td>
      <td>[2, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>19</th>
      <td>[19]</td>
      <td>1</td>
      <td>[19]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>20</th>
      <td>[2, 2, 5]</td>
      <td>3</td>
      <td>[2, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>21</th>
      <td>[3, 7]</td>
      <td>2</td>
      <td>[3, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>22</th>
      <td>[2, 11]</td>
      <td>2</td>
      <td>[2, 11]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>23</th>
      <td>[23]</td>
      <td>1</td>
      <td>[23]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>24</th>
      <td>[2, 2, 2, 3]</td>
      <td>4</td>
      <td>[2, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>25</th>
      <td>[5, 5]</td>
      <td>2</td>
      <td>[5]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>26</th>
      <td>[2, 13]</td>
      <td>2</td>
      <td>[2, 13]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>27</th>
      <td>[3, 3, 3]</td>
      <td>3</td>
      <td>[3]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>28</th>
      <td>[2, 2, 7]</td>
      <td>3</td>
      <td>[2, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>29</th>
      <td>[29]</td>
      <td>1</td>
      <td>[29]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>30</th>
      <td>[2, 3, 5]</td>
      <td>3</td>
      <td>[2, 3, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>31</th>
      <td>[31]</td>
      <td>1</td>
      <td>[31]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>32</th>
      <td>[2, 2, 2, 2, 2]</td>
      <td>5</td>
      <td>[2]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>33</th>
      <td>[3, 11]</td>
      <td>2</td>
      <td>[11, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>34</th>
      <td>[2, 17]</td>
      <td>2</td>
      <td>[17, 2]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>35</th>
      <td>[5, 7]</td>
      <td>2</td>
      <td>[5, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>36</th>
      <td>[2, 2, 3, 3]</td>
      <td>4</td>
      <td>[2, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>37</th>
      <td>[37]</td>
      <td>1</td>
      <td>[37]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>38</th>
      <td>[2, 19]</td>
      <td>2</td>
      <td>[2, 19]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>39</th>
      <td>[3, 13]</td>
      <td>2</td>
      <td>[3, 13]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>40</th>
      <td>[2, 2, 2, 5]</td>
      <td>4</td>
      <td>[2, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>41</th>
      <td>[41]</td>
      <td>1</td>
      <td>[41]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>42</th>
      <td>[2, 3, 7]</td>
      <td>3</td>
      <td>[2, 3, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>43</th>
      <td>[43]</td>
      <td>1</td>
      <td>[43]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>44</th>
      <td>[2, 2, 11]</td>
      <td>3</td>
      <td>[2, 11]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>45</th>
      <td>[3, 3, 5]</td>
      <td>3</td>
      <td>[3, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>46</th>
      <td>[2, 23]</td>
      <td>2</td>
      <td>[2, 23]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>47</th>
      <td>[47]</td>
      <td>1</td>
      <td>[47]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>48</th>
      <td>[2, 2, 2, 2, 3]</td>
      <td>5</td>
      <td>[2, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>49</th>
      <td>[7, 7]</td>
      <td>2</td>
      <td>[7]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>50</th>
      <td>[2, 5, 5]</td>
      <td>3</td>
      <td>[2, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>51</th>
      <td>[3, 17]</td>
      <td>2</td>
      <td>[17, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>52</th>
      <td>[2, 2, 13]</td>
      <td>3</td>
      <td>[2, 13]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>53</th>
      <td>[53]</td>
      <td>1</td>
      <td>[53]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>54</th>
      <td>[2, 3, 3, 3]</td>
      <td>4</td>
      <td>[2, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>55</th>
      <td>[5, 11]</td>
      <td>2</td>
      <td>[11, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>56</th>
      <td>[2, 2, 2, 7]</td>
      <td>4</td>
      <td>[2, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>57</th>
      <td>[3, 19]</td>
      <td>2</td>
      <td>[19, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>58</th>
      <td>[2, 29]</td>
      <td>2</td>
      <td>[2, 29]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>59</th>
      <td>[59]</td>
      <td>1</td>
      <td>[59]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>60</th>
      <td>[2, 2, 3, 5]</td>
      <td>4</td>
      <td>[2, 3, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>61</th>
      <td>[61]</td>
      <td>1</td>
      <td>[61]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>62</th>
      <td>[2, 31]</td>
      <td>2</td>
      <td>[2, 31]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>63</th>
      <td>[3, 3, 7]</td>
      <td>3</td>
      <td>[3, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>64</th>
      <td>[2, 2, 2, 2, 2, 2]</td>
      <td>6</td>
      <td>[2]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>65</th>
      <td>[5, 13]</td>
      <td>2</td>
      <td>[13, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>66</th>
      <td>[2, 3, 11]</td>
      <td>3</td>
      <td>[11, 2, 3]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>67</th>
      <td>[67]</td>
      <td>1</td>
      <td>[67]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>68</th>
      <td>[2, 2, 17]</td>
      <td>3</td>
      <td>[17, 2]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>69</th>
      <td>[3, 23]</td>
      <td>2</td>
      <td>[3, 23]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>70</th>
      <td>[2, 5, 7]</td>
      <td>3</td>
      <td>[2, 5, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>71</th>
      <td>[71]</td>
      <td>1</td>
      <td>[71]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>72</th>
      <td>[2, 2, 2, 3, 3]</td>
      <td>5</td>
      <td>[2, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>73</th>
      <td>[73]</td>
      <td>1</td>
      <td>[73]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>74</th>
      <td>[2, 37]</td>
      <td>2</td>
      <td>[2, 37]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>75</th>
      <td>[3, 5, 5]</td>
      <td>3</td>
      <td>[3, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>76</th>
      <td>[2, 2, 19]</td>
      <td>3</td>
      <td>[2, 19]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>77</th>
      <td>[7, 11]</td>
      <td>2</td>
      <td>[11, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>78</th>
      <td>[2, 3, 13]</td>
      <td>3</td>
      <td>[2, 3, 13]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>79</th>
      <td>[79]</td>
      <td>1</td>
      <td>[79]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>80</th>
      <td>[2, 2, 2, 2, 5]</td>
      <td>5</td>
      <td>[2, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>81</th>
      <td>[3, 3, 3, 3]</td>
      <td>4</td>
      <td>[3]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>82</th>
      <td>[2, 41]</td>
      <td>2</td>
      <td>[41, 2]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>83</th>
      <td>[83]</td>
      <td>1</td>
      <td>[83]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>84</th>
      <td>[2, 2, 3, 7]</td>
      <td>4</td>
      <td>[2, 3, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>85</th>
      <td>[5, 17]</td>
      <td>2</td>
      <td>[17, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>86</th>
      <td>[2, 43]</td>
      <td>2</td>
      <td>[2, 43]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>87</th>
      <td>[3, 29]</td>
      <td>2</td>
      <td>[3, 29]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>88</th>
      <td>[2, 2, 2, 11]</td>
      <td>4</td>
      <td>[2, 11]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>89</th>
      <td>[89]</td>
      <td>1</td>
      <td>[89]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>90</th>
      <td>[2, 3, 3, 5]</td>
      <td>4</td>
      <td>[2, 3, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>91</th>
      <td>[7, 13]</td>
      <td>2</td>
      <td>[13, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>92</th>
      <td>[2, 2, 23]</td>
      <td>3</td>
      <td>[2, 23]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>93</th>
      <td>[3, 31]</td>
      <td>2</td>
      <td>[3, 31]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>94</th>
      <td>[2, 47]</td>
      <td>2</td>
      <td>[2, 47]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>95</th>
      <td>[5, 19]</td>
      <td>2</td>
      <td>[19, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>96</th>
      <td>[2, 2, 2, 2, 2, 3]</td>
      <td>6</td>
      <td>[2, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>97</th>
      <td>[97]</td>
      <td>1</td>
      <td>[97]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>98</th>
      <td>[2, 7, 7]</td>
      <td>3</td>
      <td>[2, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>99</th>
      <td>[3, 3, 11]</td>
      <td>3</td>
      <td>[11, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>100</th>
      <td>[2, 2, 5, 5]</td>
      <td>4</td>
      <td>[2, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>101</th>
      <td>[101]</td>
      <td>1</td>
      <td>[101]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>102</th>
      <td>[2, 3, 17]</td>
      <td>3</td>
      <td>[17, 2, 3]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>103</th>
      <td>[103]</td>
      <td>1</td>
      <td>[103]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>104</th>
      <td>[2, 2, 2, 13]</td>
      <td>4</td>
      <td>[2, 13]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>105</th>
      <td>[3, 5, 7]</td>
      <td>3</td>
      <td>[3, 5, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>106</th>
      <td>[2, 53]</td>
      <td>2</td>
      <td>[2, 53]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>107</th>
      <td>[107]</td>
      <td>1</td>
      <td>[107]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>108</th>
      <td>[2, 2, 3, 3, 3]</td>
      <td>5</td>
      <td>[2, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>109</th>
      <td>[109]</td>
      <td>1</td>
      <td>[109]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>110</th>
      <td>[2, 5, 11]</td>
      <td>3</td>
      <td>[2, 11, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>111</th>
      <td>[3, 37]</td>
      <td>2</td>
      <td>[3, 37]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>112</th>
      <td>[2, 2, 2, 2, 7]</td>
      <td>5</td>
      <td>[2, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>113</th>
      <td>[113]</td>
      <td>1</td>
      <td>[113]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>114</th>
      <td>[2, 3, 19]</td>
      <td>3</td>
      <td>[19, 2, 3]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>115</th>
      <td>[5, 23]</td>
      <td>2</td>
      <td>[5, 23]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>116</th>
      <td>[2, 2, 29]</td>
      <td>3</td>
      <td>[2, 29]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>117</th>
      <td>[3, 3, 13]</td>
      <td>3</td>
      <td>[3, 13]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>118</th>
      <td>[2, 59]</td>
      <td>2</td>
      <td>[2, 59]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>119</th>
      <td>[7, 17]</td>
      <td>2</td>
      <td>[17, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>120</th>
      <td>[2, 2, 2, 3, 5]</td>
      <td>5</td>
      <td>[2, 3, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>121</th>
      <td>[11, 11]</td>
      <td>2</td>
      <td>[11]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>122</th>
      <td>[2, 61]</td>
      <td>2</td>
      <td>[2, 61]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>123</th>
      <td>[3, 41]</td>
      <td>2</td>
      <td>[41, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>124</th>
      <td>[2, 2, 31]</td>
      <td>3</td>
      <td>[2, 31]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>125</th>
      <td>[5, 5, 5]</td>
      <td>3</td>
      <td>[5]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>126</th>
      <td>[2, 3, 3, 7]</td>
      <td>4</td>
      <td>[2, 3, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>127</th>
      <td>[127]</td>
      <td>1</td>
      <td>[127]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>128</th>
      <td>[2, 2, 2, 2, 2, 2, 2]</td>
      <td>7</td>
      <td>[2]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>129</th>
      <td>[3, 43]</td>
      <td>2</td>
      <td>[43, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>130</th>
      <td>[2, 5, 13]</td>
      <td>3</td>
      <td>[2, 13, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>131</th>
      <td>[131]</td>
      <td>1</td>
      <td>[131]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>132</th>
      <td>[2, 2, 3, 11]</td>
      <td>4</td>
      <td>[11, 2, 3]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>133</th>
      <td>[7, 19]</td>
      <td>2</td>
      <td>[19, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>134</th>
      <td>[2, 67]</td>
      <td>2</td>
      <td>[2, 67]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>135</th>
      <td>[3, 3, 3, 5]</td>
      <td>4</td>
      <td>[3, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>136</th>
      <td>[2, 2, 2, 17]</td>
      <td>4</td>
      <td>[17, 2]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>137</th>
      <td>[137]</td>
      <td>1</td>
      <td>[137]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>138</th>
      <td>[2, 3, 23]</td>
      <td>3</td>
      <td>[2, 3, 23]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>139</th>
      <td>[139]</td>
      <td>1</td>
      <td>[139]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>140</th>
      <td>[2, 2, 5, 7]</td>
      <td>4</td>
      <td>[2, 5, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>141</th>
      <td>[3, 47]</td>
      <td>2</td>
      <td>[3, 47]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>142</th>
      <td>[2, 71]</td>
      <td>2</td>
      <td>[2, 71]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>143</th>
      <td>[11, 13]</td>
      <td>2</td>
      <td>[11, 13]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>144</th>
      <td>[2, 2, 2, 2, 3, 3]</td>
      <td>6</td>
      <td>[2, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>145</th>
      <td>[5, 29]</td>
      <td>2</td>
      <td>[29, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>146</th>
      <td>[2, 73]</td>
      <td>2</td>
      <td>[73, 2]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>147</th>
      <td>[3, 7, 7]</td>
      <td>3</td>
      <td>[3, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>148</th>
      <td>[2, 2, 37]</td>
      <td>3</td>
      <td>[2, 37]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>149</th>
      <td>[149]</td>
      <td>1</td>
      <td>[149]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>150</th>
      <td>[2, 3, 5, 5]</td>
      <td>4</td>
      <td>[2, 3, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>151</th>
      <td>[151]</td>
      <td>1</td>
      <td>[151]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>152</th>
      <td>[2, 2, 2, 19]</td>
      <td>4</td>
      <td>[2, 19]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>153</th>
      <td>[3, 3, 17]</td>
      <td>3</td>
      <td>[17, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>154</th>
      <td>[2, 7, 11]</td>
      <td>3</td>
      <td>[2, 11, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>155</th>
      <td>[5, 31]</td>
      <td>2</td>
      <td>[5, 31]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>156</th>
      <td>[2, 2, 3, 13]</td>
      <td>4</td>
      <td>[2, 3, 13]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>157</th>
      <td>[157]</td>
      <td>1</td>
      <td>[157]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>158</th>
      <td>[2, 79]</td>
      <td>2</td>
      <td>[2, 79]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>159</th>
      <td>[3, 53]</td>
      <td>2</td>
      <td>[3, 53]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>160</th>
      <td>[2, 2, 2, 2, 2, 5]</td>
      <td>6</td>
      <td>[2, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>161</th>
      <td>[7, 23]</td>
      <td>2</td>
      <td>[23, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>162</th>
      <td>[2, 3, 3, 3, 3]</td>
      <td>5</td>
      <td>[2, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>163</th>
      <td>[163]</td>
      <td>1</td>
      <td>[163]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>164</th>
      <td>[2, 2, 41]</td>
      <td>3</td>
      <td>[41, 2]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>165</th>
      <td>[3, 5, 11]</td>
      <td>3</td>
      <td>[11, 3, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>166</th>
      <td>[2, 83]</td>
      <td>2</td>
      <td>[2, 83]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>167</th>
      <td>[167]</td>
      <td>1</td>
      <td>[167]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>168</th>
      <td>[2, 2, 2, 3, 7]</td>
      <td>5</td>
      <td>[2, 3, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>169</th>
      <td>[13, 13]</td>
      <td>2</td>
      <td>[13]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>170</th>
      <td>[2, 5, 17]</td>
      <td>3</td>
      <td>[17, 2, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>171</th>
      <td>[3, 3, 19]</td>
      <td>3</td>
      <td>[19, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>172</th>
      <td>[2, 2, 43]</td>
      <td>3</td>
      <td>[2, 43]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>173</th>
      <td>[173]</td>
      <td>1</td>
      <td>[173]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>174</th>
      <td>[2, 3, 29]</td>
      <td>3</td>
      <td>[2, 3, 29]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>175</th>
      <td>[5, 5, 7]</td>
      <td>3</td>
      <td>[5, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>176</th>
      <td>[2, 2, 2, 2, 11]</td>
      <td>5</td>
      <td>[2, 11]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>177</th>
      <td>[3, 59]</td>
      <td>2</td>
      <td>[59, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>178</th>
      <td>[2, 89]</td>
      <td>2</td>
      <td>[89, 2]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>179</th>
      <td>[179]</td>
      <td>1</td>
      <td>[179]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>180</th>
      <td>[2, 2, 3, 3, 5]</td>
      <td>5</td>
      <td>[2, 3, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>181</th>
      <td>[181]</td>
      <td>1</td>
      <td>[181]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>182</th>
      <td>[2, 7, 13]</td>
      <td>3</td>
      <td>[2, 13, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>183</th>
      <td>[3, 61]</td>
      <td>2</td>
      <td>[3, 61]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>184</th>
      <td>[2, 2, 2, 23]</td>
      <td>4</td>
      <td>[2, 23]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>185</th>
      <td>[5, 37]</td>
      <td>2</td>
      <td>[37, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>186</th>
      <td>[2, 3, 31]</td>
      <td>3</td>
      <td>[2, 3, 31]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>187</th>
      <td>[11, 17]</td>
      <td>2</td>
      <td>[17, 11]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>188</th>
      <td>[2, 2, 47]</td>
      <td>3</td>
      <td>[2, 47]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>189</th>
      <td>[3, 3, 3, 7]</td>
      <td>4</td>
      <td>[3, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>190</th>
      <td>[2, 5, 19]</td>
      <td>3</td>
      <td>[2, 19, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>191</th>
      <td>[191]</td>
      <td>1</td>
      <td>[191]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>192</th>
      <td>[2, 2, 2, 2, 2, 2, 3]</td>
      <td>7</td>
      <td>[2, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>193</th>
      <td>[193]</td>
      <td>1</td>
      <td>[193]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>194</th>
      <td>[2, 97]</td>
      <td>2</td>
      <td>[97, 2]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>195</th>
      <td>[3, 5, 13]</td>
      <td>3</td>
      <td>[13, 3, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>196</th>
      <td>[2, 2, 7, 7]</td>
      <td>4</td>
      <td>[2, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>197</th>
      <td>[197]</td>
      <td>1</td>
      <td>[197]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>198</th>
      <td>[2, 3, 3, 11]</td>
      <td>4</td>
      <td>[11, 2, 3]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>199</th>
      <td>[199]</td>
      <td>1</td>
      <td>[199]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>200</th>
      <td>[2, 2, 2, 5, 5]</td>
      <td>5</td>
      <td>[2, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>201</th>
      <td>[3, 67]</td>
      <td>2</td>
      <td>[67, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>202</th>
      <td>[2, 101]</td>
      <td>2</td>
      <td>[2, 101]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>203</th>
      <td>[7, 29]</td>
      <td>2</td>
      <td>[29, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>204</th>
      <td>[2, 2, 3, 17]</td>
      <td>4</td>
      <td>[17, 2, 3]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>205</th>
      <td>[5, 41]</td>
      <td>2</td>
      <td>[41, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>206</th>
      <td>[2, 103]</td>
      <td>2</td>
      <td>[2, 103]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>207</th>
      <td>[3, 3, 23]</td>
      <td>3</td>
      <td>[3, 23]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>208</th>
      <td>[2, 2, 2, 2, 13]</td>
      <td>5</td>
      <td>[2, 13]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>209</th>
      <td>[11, 19]</td>
      <td>2</td>
      <td>[19, 11]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>210</th>
      <td>[2, 3, 5, 7]</td>
      <td>4</td>
      <td>[2, 3, 5, 7]</td>
      <td>4</td>
    </tr>
    <tr>
      <th>211</th>
      <td>[211]</td>
      <td>1</td>
      <td>[211]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>212</th>
      <td>[2, 2, 53]</td>
      <td>3</td>
      <td>[2, 53]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>213</th>
      <td>[3, 71]</td>
      <td>2</td>
      <td>[3, 71]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>214</th>
      <td>[2, 107]</td>
      <td>2</td>
      <td>[2, 107]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>215</th>
      <td>[5, 43]</td>
      <td>2</td>
      <td>[43, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>216</th>
      <td>[2, 2, 2, 3, 3, 3]</td>
      <td>6</td>
      <td>[2, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>217</th>
      <td>[7, 31]</td>
      <td>2</td>
      <td>[31, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>218</th>
      <td>[2, 109]</td>
      <td>2</td>
      <td>[2, 109]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>219</th>
      <td>[3, 73]</td>
      <td>2</td>
      <td>[73, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>220</th>
      <td>[2, 2, 5, 11]</td>
      <td>4</td>
      <td>[2, 11, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>221</th>
      <td>[13, 17]</td>
      <td>2</td>
      <td>[17, 13]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>222</th>
      <td>[2, 3, 37]</td>
      <td>3</td>
      <td>[2, 3, 37]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>223</th>
      <td>[223]</td>
      <td>1</td>
      <td>[223]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>224</th>
      <td>[2, 2, 2, 2, 2, 7]</td>
      <td>6</td>
      <td>[2, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>225</th>
      <td>[3, 3, 5, 5]</td>
      <td>4</td>
      <td>[3, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>226</th>
      <td>[2, 113]</td>
      <td>2</td>
      <td>[113, 2]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>227</th>
      <td>[227]</td>
      <td>1</td>
      <td>[227]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>228</th>
      <td>[2, 2, 3, 19]</td>
      <td>4</td>
      <td>[19, 2, 3]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>229</th>
      <td>[229]</td>
      <td>1</td>
      <td>[229]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>230</th>
      <td>[2, 5, 23]</td>
      <td>3</td>
      <td>[2, 5, 23]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>231</th>
      <td>[3, 7, 11]</td>
      <td>3</td>
      <td>[11, 3, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>232</th>
      <td>[2, 2, 2, 29]</td>
      <td>4</td>
      <td>[2, 29]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>233</th>
      <td>[233]</td>
      <td>1</td>
      <td>[233]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>234</th>
      <td>[2, 3, 3, 13]</td>
      <td>4</td>
      <td>[2, 3, 13]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>235</th>
      <td>[5, 47]</td>
      <td>2</td>
      <td>[5, 47]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>236</th>
      <td>[2, 2, 59]</td>
      <td>3</td>
      <td>[2, 59]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>237</th>
      <td>[3, 79]</td>
      <td>2</td>
      <td>[3, 79]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>238</th>
      <td>[2, 7, 17]</td>
      <td>3</td>
      <td>[17, 2, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>239</th>
      <td>[239]</td>
      <td>1</td>
      <td>[239]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>240</th>
      <td>[2, 2, 2, 2, 3, 5]</td>
      <td>6</td>
      <td>[2, 3, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>241</th>
      <td>[241]</td>
      <td>1</td>
      <td>[241]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>242</th>
      <td>[2, 11, 11]</td>
      <td>3</td>
      <td>[2, 11]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>243</th>
      <td>[3, 3, 3, 3, 3]</td>
      <td>5</td>
      <td>[3]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>244</th>
      <td>[2, 2, 61]</td>
      <td>3</td>
      <td>[2, 61]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>245</th>
      <td>[5, 7, 7]</td>
      <td>3</td>
      <td>[5, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>246</th>
      <td>[2, 3, 41]</td>
      <td>3</td>
      <td>[41, 2, 3]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>247</th>
      <td>[13, 19]</td>
      <td>2</td>
      <td>[19, 13]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>248</th>
      <td>[2, 2, 2, 31]</td>
      <td>4</td>
      <td>[2, 31]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>249</th>
      <td>[3, 83]</td>
      <td>2</td>
      <td>[83, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>250</th>
      <td>[2, 5, 5, 5]</td>
      <td>4</td>
      <td>[2, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>251</th>
      <td>[251]</td>
      <td>1</td>
      <td>[251]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>252</th>
      <td>[2, 2, 3, 3, 7]</td>
      <td>5</td>
      <td>[2, 3, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>253</th>
      <td>[11, 23]</td>
      <td>2</td>
      <td>[11, 23]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>254</th>
      <td>[2, 127]</td>
      <td>2</td>
      <td>[2, 127]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>255</th>
      <td>[3, 5, 17]</td>
      <td>3</td>
      <td>[17, 3, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>256</th>
      <td>[2, 2, 2, 2, 2, 2, 2, 2]</td>
      <td>8</td>
      <td>[2]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>257</th>
      <td>[257]</td>
      <td>1</td>
      <td>[257]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>258</th>
      <td>[2, 3, 43]</td>
      <td>3</td>
      <td>[43, 2, 3]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>259</th>
      <td>[7, 37]</td>
      <td>2</td>
      <td>[37, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>260</th>
      <td>[2, 2, 5, 13]</td>
      <td>4</td>
      <td>[2, 13, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>261</th>
      <td>[3, 3, 29]</td>
      <td>3</td>
      <td>[3, 29]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>262</th>
      <td>[2, 131]</td>
      <td>2</td>
      <td>[2, 131]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>263</th>
      <td>[263]</td>
      <td>1</td>
      <td>[263]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>264</th>
      <td>[2, 2, 2, 3, 11]</td>
      <td>5</td>
      <td>[11, 2, 3]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>265</th>
      <td>[5, 53]</td>
      <td>2</td>
      <td>[53, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>266</th>
      <td>[2, 7, 19]</td>
      <td>3</td>
      <td>[2, 19, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>267</th>
      <td>[3, 89]</td>
      <td>2</td>
      <td>[89, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>268</th>
      <td>[2, 2, 67]</td>
      <td>3</td>
      <td>[2, 67]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>269</th>
      <td>[269]</td>
      <td>1</td>
      <td>[269]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>270</th>
      <td>[2, 3, 3, 3, 5]</td>
      <td>5</td>
      <td>[2, 3, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>271</th>
      <td>[271]</td>
      <td>1</td>
      <td>[271]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>272</th>
      <td>[2, 2, 2, 2, 17]</td>
      <td>5</td>
      <td>[17, 2]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>273</th>
      <td>[3, 7, 13]</td>
      <td>3</td>
      <td>[3, 13, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>274</th>
      <td>[2, 137]</td>
      <td>2</td>
      <td>[137, 2]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>275</th>
      <td>[5, 5, 11]</td>
      <td>3</td>
      <td>[11, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>276</th>
      <td>[2, 2, 3, 23]</td>
      <td>4</td>
      <td>[2, 3, 23]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>277</th>
      <td>[277]</td>
      <td>1</td>
      <td>[277]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>278</th>
      <td>[2, 139]</td>
      <td>2</td>
      <td>[2, 139]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>279</th>
      <td>[3, 3, 31]</td>
      <td>3</td>
      <td>[3, 31]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>280</th>
      <td>[2, 2, 2, 5, 7]</td>
      <td>5</td>
      <td>[2, 5, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>281</th>
      <td>[281]</td>
      <td>1</td>
      <td>[281]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>282</th>
      <td>[2, 3, 47]</td>
      <td>3</td>
      <td>[2, 3, 47]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>283</th>
      <td>[283]</td>
      <td>1</td>
      <td>[283]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>284</th>
      <td>[2, 2, 71]</td>
      <td>3</td>
      <td>[2, 71]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>285</th>
      <td>[3, 5, 19]</td>
      <td>3</td>
      <td>[19, 3, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>286</th>
      <td>[2, 11, 13]</td>
      <td>3</td>
      <td>[2, 11, 13]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>287</th>
      <td>[7, 41]</td>
      <td>2</td>
      <td>[41, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>288</th>
      <td>[2, 2, 2, 2, 2, 3, 3]</td>
      <td>7</td>
      <td>[2, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>289</th>
      <td>[17, 17]</td>
      <td>2</td>
      <td>[17]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>290</th>
      <td>[2, 5, 29]</td>
      <td>3</td>
      <td>[2, 29, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>291</th>
      <td>[3, 97]</td>
      <td>2</td>
      <td>[97, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>292</th>
      <td>[2, 2, 73]</td>
      <td>3</td>
      <td>[73, 2]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>293</th>
      <td>[293]</td>
      <td>1</td>
      <td>[293]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>294</th>
      <td>[2, 3, 7, 7]</td>
      <td>4</td>
      <td>[2, 3, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>295</th>
      <td>[5, 59]</td>
      <td>2</td>
      <td>[59, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>296</th>
      <td>[2, 2, 2, 37]</td>
      <td>4</td>
      <td>[2, 37]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>297</th>
      <td>[3, 3, 3, 11]</td>
      <td>4</td>
      <td>[11, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>298</th>
      <td>[2, 149]</td>
      <td>2</td>
      <td>[2, 149]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>299</th>
      <td>[13, 23]</td>
      <td>2</td>
      <td>[13, 23]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>300</th>
      <td>[2, 2, 3, 5, 5]</td>
      <td>5</td>
      <td>[2, 3, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>301</th>
      <td>[7, 43]</td>
      <td>2</td>
      <td>[43, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>302</th>
      <td>[2, 151]</td>
      <td>2</td>
      <td>[2, 151]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>303</th>
      <td>[3, 101]</td>
      <td>2</td>
      <td>[3, 101]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>304</th>
      <td>[2, 2, 2, 2, 19]</td>
      <td>5</td>
      <td>[2, 19]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>305</th>
      <td>[5, 61]</td>
      <td>2</td>
      <td>[61, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>306</th>
      <td>[2, 3, 3, 17]</td>
      <td>4</td>
      <td>[17, 2, 3]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>307</th>
      <td>[307]</td>
      <td>1</td>
      <td>[307]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>308</th>
      <td>[2, 2, 7, 11]</td>
      <td>4</td>
      <td>[2, 11, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>309</th>
      <td>[3, 103]</td>
      <td>2</td>
      <td>[3, 103]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>310</th>
      <td>[2, 5, 31]</td>
      <td>3</td>
      <td>[2, 5, 31]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>311</th>
      <td>[311]</td>
      <td>1</td>
      <td>[311]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>312</th>
      <td>[2, 2, 2, 3, 13]</td>
      <td>5</td>
      <td>[2, 3, 13]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>313</th>
      <td>[313]</td>
      <td>1</td>
      <td>[313]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>314</th>
      <td>[2, 157]</td>
      <td>2</td>
      <td>[2, 157]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>315</th>
      <td>[3, 3, 5, 7]</td>
      <td>4</td>
      <td>[3, 5, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>316</th>
      <td>[2, 2, 79]</td>
      <td>3</td>
      <td>[2, 79]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>317</th>
      <td>[317]</td>
      <td>1</td>
      <td>[317]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>318</th>
      <td>[2, 3, 53]</td>
      <td>3</td>
      <td>[2, 3, 53]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>319</th>
      <td>[11, 29]</td>
      <td>2</td>
      <td>[11, 29]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>320</th>
      <td>[2, 2, 2, 2, 2, 2, 5]</td>
      <td>7</td>
      <td>[2, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>321</th>
      <td>[3, 107]</td>
      <td>2</td>
      <td>[107, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>322</th>
      <td>[2, 7, 23]</td>
      <td>3</td>
      <td>[2, 23, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>323</th>
      <td>[17, 19]</td>
      <td>2</td>
      <td>[17, 19]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>324</th>
      <td>[2, 2, 3, 3, 3, 3]</td>
      <td>6</td>
      <td>[2, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>325</th>
      <td>[5, 5, 13]</td>
      <td>3</td>
      <td>[13, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>326</th>
      <td>[2, 163]</td>
      <td>2</td>
      <td>[2, 163]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>327</th>
      <td>[3, 109]</td>
      <td>2</td>
      <td>[3, 109]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>328</th>
      <td>[2, 2, 2, 41]</td>
      <td>4</td>
      <td>[41, 2]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>329</th>
      <td>[7, 47]</td>
      <td>2</td>
      <td>[47, 7]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>330</th>
      <td>[2, 3, 5, 11]</td>
      <td>4</td>
      <td>[11, 2, 3, 5]</td>
      <td>4</td>
    </tr>
    <tr>
      <th>331</th>
      <td>[331]</td>
      <td>1</td>
      <td>[331]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>332</th>
      <td>[2, 2, 83]</td>
      <td>3</td>
      <td>[2, 83]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>333</th>
      <td>[3, 3, 37]</td>
      <td>3</td>
      <td>[3, 37]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>334</th>
      <td>[2, 167]</td>
      <td>2</td>
      <td>[2, 167]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>335</th>
      <td>[5, 67]</td>
      <td>2</td>
      <td>[67, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>336</th>
      <td>[2, 2, 2, 2, 3, 7]</td>
      <td>6</td>
      <td>[2, 3, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>337</th>
      <td>[337]</td>
      <td>1</td>
      <td>[337]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>338</th>
      <td>[2, 13, 13]</td>
      <td>3</td>
      <td>[2, 13]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>339</th>
      <td>[3, 113]</td>
      <td>2</td>
      <td>[113, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>340</th>
      <td>[2, 2, 5, 17]</td>
      <td>4</td>
      <td>[17, 2, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>341</th>
      <td>[11, 31]</td>
      <td>2</td>
      <td>[11, 31]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>342</th>
      <td>[2, 3, 3, 19]</td>
      <td>4</td>
      <td>[19, 2, 3]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>343</th>
      <td>[7, 7, 7]</td>
      <td>3</td>
      <td>[7]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>344</th>
      <td>[2, 2, 2, 43]</td>
      <td>4</td>
      <td>[2, 43]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>345</th>
      <td>[3, 5, 23]</td>
      <td>3</td>
      <td>[3, 5, 23]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>346</th>
      <td>[2, 173]</td>
      <td>2</td>
      <td>[2, 173]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>347</th>
      <td>[347]</td>
      <td>1</td>
      <td>[347]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>348</th>
      <td>[2, 2, 3, 29]</td>
      <td>4</td>
      <td>[2, 3, 29]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>349</th>
      <td>[349]</td>
      <td>1</td>
      <td>[349]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>350</th>
      <td>[2, 5, 5, 7]</td>
      <td>4</td>
      <td>[2, 5, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>351</th>
      <td>[3, 3, 3, 13]</td>
      <td>4</td>
      <td>[3, 13]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>352</th>
      <td>[2, 2, 2, 2, 2, 11]</td>
      <td>6</td>
      <td>[2, 11]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>353</th>
      <td>[353]</td>
      <td>1</td>
      <td>[353]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>354</th>
      <td>[2, 3, 59]</td>
      <td>3</td>
      <td>[59, 2, 3]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>355</th>
      <td>[5, 71]</td>
      <td>2</td>
      <td>[5, 71]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>356</th>
      <td>[2, 2, 89]</td>
      <td>3</td>
      <td>[89, 2]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>357</th>
      <td>[3, 7, 17]</td>
      <td>3</td>
      <td>[17, 3, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>358</th>
      <td>[2, 179]</td>
      <td>2</td>
      <td>[2, 179]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>359</th>
      <td>[359]</td>
      <td>1</td>
      <td>[359]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>360</th>
      <td>[2, 2, 2, 3, 3, 5]</td>
      <td>6</td>
      <td>[2, 3, 5]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>361</th>
      <td>[19, 19]</td>
      <td>2</td>
      <td>[19]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>362</th>
      <td>[2, 181]</td>
      <td>2</td>
      <td>[2, 181]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>363</th>
      <td>[3, 11, 11]</td>
      <td>3</td>
      <td>[11, 3]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>364</th>
      <td>[2, 2, 7, 13]</td>
      <td>4</td>
      <td>[2, 13, 7]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>365</th>
      <td>[5, 73]</td>
      <td>2</td>
      <td>[73, 5]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>366</th>
      <td>[2, 3, 61]</td>
      <td>3</td>
      <td>[2, 3, 61]</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>


