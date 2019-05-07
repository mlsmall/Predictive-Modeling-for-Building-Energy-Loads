<div tabindex="-1" id="notebook" class="border-box-sizing">

<div class="container" id="notebook-container">

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

Comparing building heating and cooling loads with respect to building characteristics. The data contains 768 different building shapes and 8 characteristics. The goal is to use the 8 building features to predict the heating and cooling load. The features are:

*   relative compactness
*   surface area - in meters squared
*   wall area - in meters squared
*   roof area - in meters squared
*   overall height - in meters
*   orientation - 2: North, 3: East, 4: South, 5: West
*   glazing area - as a percentage of the floor area - 0%, 10%, 25%, and 40%
*   glazing area distribution:
    *   0: uniform - with 25% glazing on each side
    *   1: north - 55% on the north side and 15% on each of the other sides
    *   2: east - 55% on the east side and 15% on each of the other sides
    *   3: south - 55% on the south side and 15% on each of the other sides
    *   4: west - 55% on the west side and 15% on each of the other sides

The values to predict are the heating and cooling loads listed in kWh/m2.

12 buildings were modeled with different shapes, surface areas and dimensions. The overall volume was kept the same for each building at 772 meters squared. Considering twelve building forms with three glazing area variations, six glazing area distributions each (5 distributions + 1 with no glazing), for four orientations, we obtain 12 × 3 × 6 × 4 = 768 different building variations.

The dataset, which can be found [here](https://archive.ics.uci.edu/ml/datasets/Energy+efficiency) was donated to the University of California at Irving.

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [1]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>

<span class="kn">from</span> <span class="nn">sklearn.ensemble</span> <span class="k">import</span> <span class="n">RandomForestRegressor</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="k">import</span> <span class="n">train_test_split</span>

<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
<span class="o">%</span><span class="k">matplotlib</span> inline
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [2]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">data</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">'Energy data.csv'</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [3]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">data</span><span class="o">.</span><span class="n">columns</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'relative_compactness'</span><span class="p">,</span> <span class="s1">'surface_area'</span><span class="p">,</span> <span class="s1">'wall_area'</span><span class="p">,</span> <span class="s1">'roof_area'</span><span class="p">,</span> <span class="s1">'overall_height'</span><span class="p">,</span>
                <span class="s1">'orientation'</span><span class="p">,</span> <span class="s1">'glazing_area'</span><span class="p">,</span> <span class="s1">'glazing_area_distribution'</span><span class="p">,</span> <span class="s1">'heating_load'</span><span class="p">,</span> <span class="s1">'cooling_load'</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [4]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">data</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[4]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table class="dataframe" border="1">

<thead>

<tr style="text-align: right;">

<th></th>

<th>relative_compactness</th>

<th>surface_area</th>

<th>wall_area</th>

<th>roof_area</th>

<th>overall_height</th>

<th>orientation</th>

<th>glazing_area</th>

<th>glazing_area_distribution</th>

<th>heating_load</th>

<th>cooling_load</th>

</tr>

</thead>

<tbody>

<tr>

<th>0</th>

<td>0.98</td>

<td>514.5</td>

<td>294.0</td>

<td>110.25</td>

<td>7.0</td>

<td>2</td>

<td>0.0</td>

<td>0</td>

<td>15.55</td>

<td>21.33</td>

</tr>

<tr>

<th>1</th>

<td>0.98</td>

<td>514.5</td>

<td>294.0</td>

<td>110.25</td>

<td>7.0</td>

<td>3</td>

<td>0.0</td>

<td>0</td>

<td>15.55</td>

<td>21.33</td>

</tr>

<tr>

<th>2</th>

<td>0.98</td>

<td>514.5</td>

<td>294.0</td>

<td>110.25</td>

<td>7.0</td>

<td>4</td>

<td>0.0</td>

<td>0</td>

<td>15.55</td>

<td>21.33</td>

</tr>

<tr>

<th>3</th>

<td>0.98</td>

<td>514.5</td>

<td>294.0</td>

<td>110.25</td>

<td>7.0</td>

<td>5</td>

<td>0.0</td>

<td>0</td>

<td>15.55</td>

<td>21.33</td>

</tr>

<tr>

<th>4</th>

<td>0.90</td>

<td>563.5</td>

<td>318.5</td>

<td>122.50</td>

<td>7.0</td>

<td>2</td>

<td>0.0</td>

<td>0</td>

<td>20.84</td>

<td>28.28</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [5]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">data</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[5]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table class="dataframe" border="1">

<thead>

<tr style="text-align: right;">

<th></th>

<th>relative_compactness</th>

<th>surface_area</th>

<th>wall_area</th>

<th>roof_area</th>

<th>overall_height</th>

<th>orientation</th>

<th>glazing_area</th>

<th>glazing_area_distribution</th>

<th>heating_load</th>

<th>cooling_load</th>

</tr>

</thead>

<tbody>

<tr>

<th>count</th>

<td>768.000000</td>

<td>768.000000</td>

<td>768.000000</td>

<td>768.000000</td>

<td>768.00000</td>

<td>768.000000</td>

<td>768.000000</td>

<td>768.00000</td>

<td>768.000000</td>

<td>768.000000</td>

</tr>

<tr>

<th>mean</th>

<td>0.764167</td>

<td>671.708333</td>

<td>318.500000</td>

<td>176.604167</td>

<td>5.25000</td>

<td>3.500000</td>

<td>0.234375</td>

<td>2.81250</td>

<td>22.307201</td>

<td>24.587760</td>

</tr>

<tr>

<th>std</th>

<td>0.105777</td>

<td>88.086116</td>

<td>43.626481</td>

<td>45.165950</td>

<td>1.75114</td>

<td>1.118763</td>

<td>0.133221</td>

<td>1.55096</td>

<td>10.090196</td>

<td>9.513306</td>

</tr>

<tr>

<th>min</th>

<td>0.620000</td>

<td>514.500000</td>

<td>245.000000</td>

<td>110.250000</td>

<td>3.50000</td>

<td>2.000000</td>

<td>0.000000</td>

<td>0.00000</td>

<td>6.010000</td>

<td>10.900000</td>

</tr>

<tr>

<th>25%</th>

<td>0.682500</td>

<td>606.375000</td>

<td>294.000000</td>

<td>140.875000</td>

<td>3.50000</td>

<td>2.750000</td>

<td>0.100000</td>

<td>1.75000</td>

<td>12.992500</td>

<td>15.620000</td>

</tr>

<tr>

<th>50%</th>

<td>0.750000</td>

<td>673.750000</td>

<td>318.500000</td>

<td>183.750000</td>

<td>5.25000</td>

<td>3.500000</td>

<td>0.250000</td>

<td>3.00000</td>

<td>18.950000</td>

<td>22.080000</td>

</tr>

<tr>

<th>75%</th>

<td>0.830000</td>

<td>741.125000</td>

<td>343.000000</td>

<td>220.500000</td>

<td>7.00000</td>

<td>4.250000</td>

<td>0.400000</td>

<td>4.00000</td>

<td>31.667500</td>

<td>33.132500</td>

</tr>

<tr>

<th>max</th>

<td>0.980000</td>

<td>808.500000</td>

<td>416.500000</td>

<td>220.500000</td>

<td>7.00000</td>

<td>5.000000</td>

<td>0.400000</td>

<td>5.00000</td>

<td>43.100000</td>

<td>48.030000</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

To simplify the model, we'll sum heating and cooling load into a new column called "energy load". Then we'll eliminate the heating and cooling load columns.

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [6]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">data_new</span> <span class="o">=</span> <span class="n">data</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [7]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">data_new</span><span class="p">[</span><span class="s1">'energy load'</span><span class="p">]</span> <span class="o">=</span> <span class="n">data</span><span class="p">[</span><span class="s1">'heating_load'</span><span class="p">]</span> <span class="o">+</span> <span class="n">data</span><span class="p">[</span><span class="s1">'cooling_load'</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [8]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">data_new</span> <span class="o">=</span> <span class="n">data_new</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">columns</span><span class="o">=</span><span class="p">[</span><span class="s1">'heating_load'</span><span class="p">,</span> <span class="s1">'cooling_load'</span><span class="p">])</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

The new dataset:

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [9]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">data_new</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">2</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[9]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table class="dataframe" border="1">

<thead>

<tr style="text-align: right;">

<th></th>

<th>relative_compactness</th>

<th>surface_area</th>

<th>wall_area</th>

<th>roof_area</th>

<th>overall_height</th>

<th>orientation</th>

<th>glazing_area</th>

<th>glazing_area_distribution</th>

<th>energy load</th>

</tr>

</thead>

<tbody>

<tr>

<th>0</th>

<td>0.98</td>

<td>514.5</td>

<td>294.0</td>

<td>110.25</td>

<td>7.0</td>

<td>2</td>

<td>0.0</td>

<td>0</td>

<td>36.88</td>

</tr>

<tr>

<th>1</th>

<td>0.98</td>

<td>514.5</td>

<td>294.0</td>

<td>110.25</td>

<td>7.0</td>

<td>3</td>

<td>0.0</td>

<td>0</td>

<td>36.88</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

Correlation between variables

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [10]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Setting the format for diplaying the correlation table</span>
<span class="n">pd</span><span class="o">.</span><span class="n">set_option</span><span class="p">(</span><span class="s1">'display.float_format'</span><span class="p">,</span> <span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="s1">'</span><span class="si">{:,.3f}</span><span class="s1">'</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">x</span><span class="p">))</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [11]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">data_new</span><span class="o">.</span><span class="n">corr</span><span class="p">()</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="s1">'energy load'</span><span class="p">,</span> <span class="n">ascending</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[11]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table class="dataframe" border="1">

<thead>

<tr style="text-align: right;">

<th></th>

<th>relative_compactness</th>

<th>surface_area</th>

<th>wall_area</th>

<th>roof_area</th>

<th>overall_height</th>

<th>orientation</th>

<th>glazing_area</th>

<th>glazing_area_distribution</th>

<th>energy load</th>

</tr>

</thead>

<tbody>

<tr>

<th>energy load</th>

<td>0.632</td>

<td>-0.669</td>

<td>0.445</td>

<td>-0.867</td>

<td>0.898</td>

<td>0.006</td>

<td>0.241</td>

<td>0.070</td>

<td>1.000</td>

</tr>

<tr>

<th>overall_height</th>

<td>0.828</td>

<td>-0.858</td>

<td>0.281</td>

<td>-0.973</td>

<td>1.000</td>

<td>0.000</td>

<td>0.000</td>

<td>0.000</td>

<td>0.898</td>

</tr>

<tr>

<th>relative_compactness</th>

<td>1.000</td>

<td>-0.992</td>

<td>-0.204</td>

<td>-0.869</td>

<td>0.828</td>

<td>0.000</td>

<td>0.000</td>

<td>0.000</td>

<td>0.632</td>

</tr>

<tr>

<th>wall_area</th>

<td>-0.204</td>

<td>0.196</td>

<td>1.000</td>

<td>-0.292</td>

<td>0.281</td>

<td>0.000</td>

<td>-0.000</td>

<td>0.000</td>

<td>0.445</td>

</tr>

<tr>

<th>glazing_area</th>

<td>0.000</td>

<td>0.000</td>

<td>-0.000</td>

<td>-0.000</td>

<td>0.000</td>

<td>0.000</td>

<td>1.000</td>

<td>0.213</td>

<td>0.241</td>

</tr>

<tr>

<th>glazing_area_distribution</th>

<td>0.000</td>

<td>-0.000</td>

<td>0.000</td>

<td>-0.000</td>

<td>0.000</td>

<td>0.000</td>

<td>0.213</td>

<td>1.000</td>

<td>0.070</td>

</tr>

<tr>

<th>orientation</th>

<td>0.000</td>

<td>0.000</td>

<td>0.000</td>

<td>0.000</td>

<td>0.000</td>

<td>1.000</td>

<td>0.000</td>

<td>0.000</td>

<td>0.006</td>

</tr>

<tr>

<th>surface_area</th>

<td>-0.992</td>

<td>1.000</td>

<td>0.196</td>

<td>0.881</td>

<td>-0.858</td>

<td>0.000</td>

<td>0.000</td>

<td>-0.000</td>

<td>-0.669</td>

</tr>

<tr>

<th>roof_area</th>

<td>-0.869</td>

<td>0.881</td>

<td>-0.292</td>

<td>1.000</td>

<td>-0.973</td>

<td>0.000</td>

<td>-0.000</td>

<td>-0.000</td>

<td>-0.867</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [12]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span> <span class="o">=</span> <span class="p">(</span><span class="mi">12</span><span class="p">,</span><span class="mi">12</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">heatmap</span><span class="p">(</span><span class="n">data_new</span><span class="o">.</span><span class="n">corr</span><span class="p">(),</span> <span class="n">annot</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">linewidths</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">linecolor</span><span class="o">=</span><span class="s1">'blue'</span><span class="p">);</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_png output_subarea ">![](data:image/png;base64,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j4CP8mjntbzLIfa/FMg5CP6+0PIpwJT92n4MfJzHPq4+2DFEREREJLKpwyAiIiIi4krkaKASQR2Go4CZ9SB469WcVjjn/vkDOUVEREQkrNRhOAo4574nOBlaRERERKRYqcMgIiIiIhFPk5696YvbRERERETEkyoMIiIiIhLxXECTnr2owiAiIiIiIp7UYRAREREREU8akiQiIiIiEU+Tnr2pwiAiIiIiIp5UYRARERGRiOf0Tc+eVGEQERERERFP6jCIiIiIiIgnDUkSERERkYinSc/eVGEQERERERFPqjCIiIiISMTTNz17U4VBREREREQ8qcMgIiIiIiKeNCRJRERERCKec+GOoORShUFERERERDypwyAiIiIiIp40JElEREREIp7ukuRNFQYREREREfGkCoOIiIiIRDxVGLypwiAiIiIiIp7UYRAREREREU8akiQiIiIiEU/fw+BNFQYREREREfGkCoOIiIiIRDxNevZmTvUXKQAz9AsjIiIihco5wn62vrxV97Cf4zScPyHsr0NeNCRJREREREQ8aUiSFFjKjM/DHUKRK9PhAgBqxrUIcyTFY33yQgC2nt8lvIEUk/gvpgBQKrp2eAMpBhnpawFI37Q8zJEUj+iqDQGYUfO8MEdS9Dqs/xKIjFwhsvLdm2vq4p/CHEnxiDn2tHCHAIBzJfLifomgCoOIiIiIiHhShUFEREREIp4LhDuCkksVBhERERER8aQOg4iIiIiIeNKQJBERERGJeAFNevakCoOIiIiIiHhShUFEREREIp5uq+pNFQYREREREfGkDoOIiIiIiHjSkCQRERERiXguoCFJXlRhEBERERERT6owiIiIiEjEcy7cEZRcqjCIiIiIiIgndRhERERERMSThiSJiIiISMTTpGdvqjCIiIiIiIgndRhERERERMSThiSJiIiISMQLOA1J8qIKg4iIiIiIeFKFQUREREQinlOFwZMqDCIiIiIi4kkdBhERERER8aQhSSIiIiIS8ZwLdwQllyoMIiIiIiLiSRUGEREREYl4uq2qN1UYRERERETEkzoMIiIiIiLiSUOSRERERCTi6XsYvKnCICIiIiIinlRhEBEREZGIp9uqelOHQcLq1z+WMPLf/yUQCHBel/YMOPe0XOsTNycz9PVP2bknlUDAcfvFPTi1bTPm/72GR9/6CgCH48bzutK1fYtw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
)</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

Correlation shows how features are related to each other using a linear correlation between variables. Keep in mind that since it only find the linear relationship between variables, it will not be able to find the non-linear relationship. A better metric to use is called _feature importance_, which we will determine after the model is built.

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

On to the model

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [12]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">y</span> <span class="o">=</span> <span class="n">data_new</span><span class="p">[</span><span class="s1">'energy load'</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [13]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">X</span> <span class="o">=</span> <span class="n">data_new</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">columns</span><span class="o">=</span><span class="s1">'energy load'</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [14]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span><span class="o">=</span><span class="mf">0.2</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">23</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [15]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">model</span> <span class="o">=</span> <span class="n">RandomForestRegressor</span><span class="p">(</span><span class="n">n_estimators</span><span class="o">=</span><span class="mi">100</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">23</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [16]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[16]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>RandomForestRegressor(bootstrap=True, criterion='mse', max_depth=None,
           max_features='auto', max_leaf_nodes=None,
           min_impurity_decrease=0.0, min_impurity_split=None,
           min_samples_leaf=1, min_samples_split=2,
           min_weight_fraction_leaf=0.0, n_estimators=100, n_jobs=None,
           oob_score=False, random_state=23, verbose=0, warm_start=False)</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [17]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">predictions</span> <span class="o">=</span> <span class="n">model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [18]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="k">import</span> <span class="n">r2_score</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [19]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">r2_score</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">predictions</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[19]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>0.9931211166410133</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

The random forest model provides us with a highly accurate R2 score of 0.993

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [20]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="k">for</span> <span class="n">feature</span> <span class="ow">in</span> <span class="nb">zip</span><span class="p">(</span><span class="n">data_new</span><span class="o">.</span><span class="n">columns</span><span class="p">,</span> <span class="n">model</span><span class="o">.</span><span class="n">feature_importances_</span><span class="p">):</span>
    <span class="nb">print</span><span class="p">(</span><span class="n">feature</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_subarea output_stream output_stdout output_text">

<pre>('relative_compactness', 0.5060543116884478)
('surface_area', 0.14821753795820464)
('wall_area', 0.04233577705009435)
('roof_area', 0.08329432066422113)
('overall_height', 0.14625311504507843)
('orientation', 0.0023343330653874043)
('glazing_area', 0.06172701478673418)
('glazing_area_distribution', 0.009783589741831876)
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

After training the model, relative compactness is the most important feature for predicting the heating and cooling load of a building. The glazing area distribution is relatively unimportant.

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

The higher the feature importance score, the more relevant the feature is to the output variable, which is energy load in this case.

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [21]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">feat_importances</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">(</span><span class="n">model</span><span class="o">.</span><span class="n">feature_importances_</span><span class="p">,</span> <span class="n">index</span><span class="o">=</span><span class="n">X</span><span class="o">.</span><span class="n">columns</span><span class="p">)</span>
<span class="n">feat_importances</span><span class="o">.</span><span class="n">nlargest</span><span class="p">(</span><span class="mi">10</span><span class="p">)</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">kind</span><span class="o">=</span><span class="s1">'barh'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_png output_subarea ">![](data:image/png;base64,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
)</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span> 
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

</div>