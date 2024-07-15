Провести дисперсионный анализ для определения того, есть ли различия среднего роста среди взрослых футболистов, хоккеистов и штангистов.
Даны значения роста в трех группах случайно выбранных спортсменов:
Футболисты: 173, 175, 180, 178, 177, 185, 183, 182.
Хоккеисты: 177, 179, 180, 188, 177, 172, 171, 184, 180.
Штангисты: 172, 173, 169, 177, 166, 180, 178, 177, 172, 166, 170.

import numpy as np
import pandas as pd
from scipy import stats
from statsmodels.stats.multicomp import pairwise_tukeyhsd
import pandas as pd

football = np.array([173, 175, 180, 178, 177, 185, 183, 182])
hockey = np.array([177, 179, 180, 188, 177, 172, 171, 184, 180])
weightlifters = np.array([172, 173, 169, 177, 166, 180, 178, 177, 172, 166, 170])

stats.kruskal(football, hockey, weightlifters) 
KruskalResult(statistic=7.897493213863828, pvalue=0.01927885061595347)

df = pd.DataFrame({"score": [173, 175, 180, 178, 177, 185, 183, 182,177, 179, 180, 188, 177, 172, 171, 184, 180,172, 173, 169, 177, 166, 180, 178, 177, 172, 166, 170], "group": np.repeat(["football", "hockey", "weightlifters"], repeats = [8, 9, 11])})
df
tukey = pairwise_tukeyhsd(df["score"], df["group"], alpha = 0.05)
print(tukey)

Multiple Comparison of Means - Tukey HSD, FWER=0.05      
==============================================================
 group1      group2    meandiff p-adj   lower    upper  reject
--------------------------------------------------------------
football        hockey  -0.4583  0.979  -6.2732  5.3566  False
football weightlifters  -6.3977 0.0219 -11.9583 -0.8372   True
  hockey weightlifters  -5.9394 0.0284 -11.3181 -0.5607   True
--------------------------------------------------------------



Выводы:
Между группой football и hockeyТак нет различий в среднем росте, тогда как между группами football и weightlifters, а так же между группами hockey и weightlifters есть различия в среднем росте.
