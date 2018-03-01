### 01 hist可视化
```
l_subscribers = []
l_customers = []
l_subscribers, l_customers = filter_bike_time(city)
# x轴间隔
plt.hist(l_customers, bins=[x for x in range(0, 80, 5)], range=(min(l_customers), 75))
plt.title('Distribution of Trip Durations')
plt.xlabel('{} {} Duration (m)'.format(city, 'customers'))
plt.show()
# x轴间隔
plt.hist(l_subscribers, bins=[x for x in range(0, 80, 5)], color='green',range=(min(l_subscribers), 75))
plt.title('Distribution of Trip Durations')
plt.xlabel('{} {} Duration (m)'.format(city, 'subscribers'))
plt.show()
```

![hist](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAYcAAAEWCAYAAACNJFuYAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMS4wLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvpW3flQAAIABJREFUeJzt3Xm8HFWd9/HPl0Q22YK58IQECUtAFiFIQBQXNiEgEnBkSAYhMmjEB1TcQRw2QVFERwbFiRABWcImkuEBITAgLiy5QEjCZkIIcklILoQlbIHA7/njnIbKrb5rd+iG+32/Xv3qqlNVp37V1ff+qk5Vn1JEYGZmVrRSowMwM7Pm4+RgZmYlTg5mZlbi5GBmZiVODmZmVuLkYGZmJU4O1ilJv5H0H3Wq6/2SXpA0II/fKumL9ag713e9pPH1qq8X6z1V0lOSnqxTfQ9L+ng96mqUd8M2GMi/c+ifJM0D1geWAa8DDwAXAhMj4o0+1PXFiLipF8vcClwUEef2Zl152ZOAzSLi871dtp4kbQj8A9goIhZ1mHYI8N95dACwCvBSZXpErFHnWAYCr+V1BPAKMB3474i4op7r6rDei4A5EXHSilqHNYbPHPq3z0TEmsBGwOnA94Dz6r2S/I/r3Wgj4OmOiQEgIi6OiDVyEtgHmF8Zr5YY6vgZbZ3r/wBwEXCOpOP7UtG7eL9ZT0SEX/3wBcwD9uxQthPwBrBNHj8fODUPDwauBZ4FFgN/IR1c/D4v8zLwAvBdYDjp6PUI4J/AbYWygbm+W4EfA3cBzwHXAOvmabsCbdXiBUYDr5KOkl8A7ivU98U8vBLwA+AxYBHpjGjtPK0Sx/gc21PA8V18Tmvn5dtzfT/I9e+Zt/mNHMf5XdRR2p5c3gZ8B5gJvFoo2zUPnwpcBlwBLAFagQ92so6BebuGdygfm+Ncp2P9hXWcn4c3y3Ucnj+b/83beiXwZN73twJb5vn/b94Pr+bP4Ooq27AqcBawAHgC+Dmwcp62Z96v382f73zgsEJs+wEP5m1vA77R6L+b/vTymYO9KSLuIv0RVmsv/lae1kJqjvp+WiQOJf0j+Uyko+KfFpb5JLAlsHcnqzwM+HdgA1Lz1lk9iPFPwI+Ay/L6tqsy2xfyazdgE2AN4OwO83wM2ALYAzhB0padrPK/SAlik7w9hwGHR2pCK54RfKG72DsxNtezdifTPwtcAqxL+id9dS+P6P9IatLasRfLfIJ05vHpPH4tMAL4P8As0gEBEfFrUvL6Uf4MDqxS1wnAKGBbYHtgF+C4wvRhwGqk78CRpDOdtfK03wFHRDq73Rb4cy+2wWrk5GAdzSf9I+roNWAIqX39tYj4S+TDuy6cFBEvRsTLnUz/fUTMiogXgf8A/rVywbpGhwA/j4i5EfEC6Z/R2A7/VE+OiJcj4j7gPqCUZHIsBwPHRcSSiJgHnAkcWocYK34ZEW1dfEZ3RsTVEfEacAawFr34Rx8Rr5DO9Krt086cGBEv5c/njYg4P2//K8BJwA6S3tvDug4hfQ/aIzW/ncLyn98rpLPT1yJiCrAU2DxPew3YStKaEbE4Iu7pxTZYjZwcrKOhpH8mHZ0BzAFulDRX0rE9qOvxXkx/DHgPqfmqVhvk+op1DySd8VQU7y56iXR20dFgYOUqdQ2tQ4wVPf6MIuJ1UtPMBj2tXNKqpMRQbZ92u05JAyT9NO/z50nfAej5fhpC15/fU3m7Kor74kBgf+Cf+e62D/diG6xGTg72Jkk7kv5w/9pxWj5y/FZEbAJ8BvimpD0qkzupsrsziw0Lw+8nHSk+BbwIrF6IawCpOaun9c4nXSwu1r0MWNjNch09lWPqWNcTvaynKz3+jCStRNo/83tR/wGko/FpeXy5z5bUVLR8QMufER4G7AvsTmr62qwSTmX2bta/gD5+fhFxZ0TsD6xHatqa3JPlrD6cHAxJa0naj/THd1FEzKwyz36SNpMk4HnS7a+VI76FpDb53vq8pK0krU5qbrgyH0X+A1hV0qclvYd0EXiVwnILgeH5n2U1lwLfkLSxpDV46xrFst4El2O5HDhN0pqSNgK+SboL6O2yk6Qx+XP4Nuni7LRulkHS+yQdSrpm8uOIeDZPmk5uYpO0E+maRlfWJCWXp0lJ5bQO07vb95eSrukMltRCaj7s9vOTtJqkf5O0Vm5SW8Jb3zd7Gzg59G//I2kJqRnheNKdJId3Mu8I4CbSXSm3A7+OiFvztB8DP5D0rKRv92L9vyfdEfUk6a6WrwFExHOkO2HOJR1lvki6GF5RuW//aUnV2qEn5bpvAx4ltWt/tRdxFX01r38u6Yzqklz/2+Vq4POkZqGDgc92k+Tul/QCMJu0L78aEacUph9Putj8LOkf9SXdrP93pDOV+cD9wN87TD8X2E7SM5KurLL8yaRrOjOBGcCdpO9LT4wHHsvNWUdQ32s91g3/CM6sSUk6FRhWw51QZn3mMwczMytxcjAzsxI3K5mZWYnPHMzMrOQd27HW4MGDY/jw4Y0Ow8zsHeXuu+9+KiJaupvvHZschg8fTmtra6PDMDN7R5H0WPdzuVnJzMyqcHIwM7MSJwczMytxcjAzsxInBzMzK3FyMDOzEicHMzMrcXIwM7OSbpODpEmSFkmaVSi7TNL0/JonaXouHy7p5cK03xSW2UHSTElzJJ2VHxqDpHUlTZU0O78PWhEbamZmPdeTX0ifD5wNXFgpiIiDK8OSzgSeK8z/SESMrFLPOcAE4A7gOmA0cD1wLHBzRJyen0t8LPC93m1GY+lkdT9TL8WJ7hDRzBqn2zOHiLiNTh5Ono/+/5X0KMBOSRoCrBURt+fn015IerYtwBjggjx8QaHczMwapNZrDh8HFkbE7ELZxpLulfRnSR/PZUNZ/jGPbbkMYP2IWACQ39frbGWSJkhqldTa3t5eY+hmZtaZWpPDOJY/a1gAvD8itic9iP0SSWsB1dpdet1uEhETI2JURIxqaem2U0EzM+ujPvfKKmkg8Flgh0pZRCwFlubhuyU9AmxOOlMYVlh8GOmB5QALJQ2JiAW5+WlRX2MyM7P6qOXMYU/goYh4s7lIUoukAXl4E2AEMDc3Fy2RtHO+TnEYcE1ebAowPg+PL5SbmVmD9ORW1kuB24EtJLVJOiJPGkv5QvQngBmS7gOuBI6MiMrF7K8A5wJzgEdIdyoBnA58StJs4FN53MzMGqjbZqWIGNdJ+ReqlF0FXNXJ/K3ANlXKnwb26C4OMzN7+/gX0mZmVuLkYGZmJU4OZmZW4uRgZmYlTg5mZlbi5GBmZiVODmZmVuLkYGZmJU4OZmZW4uRgZmYlTg5mZlbi5GBmZiVODmZmVuLkYGZmJU4OZmZW4uRgZmYlTg5mZlbi5GBmZiVODmZmVuLkYGZmJd0mB0mTJC2SNKtQdpKkJyRNz699C9OOkzRH0sOS9i6Uj85lcyQdWyjfWNKdkmZLukzSyvXcQDMz672enDmcD4yuUv6LiBiZX9cBSNoKGAtsnZf5taQBkgYAvwL2AbYCxuV5AX6S6xoBPAMcUcsGmZlZ7bpNDhFxG7C4h/WNASZHxNKIeBSYA+yUX3MiYm5EvApMBsZIErA7cGVe/gLggF5ug5mZ1Vkt1xyOljQjNzsNymVDgccL87Tlss7K3wc8GxHLOpRXJWmCpFZJre3t7TWEbmZmXelrcjgH2BQYCSwAzszlqjJv9KG8qoiYGBGjImJUS0tL7yI2M7MeG9iXhSJiYWVY0m+Ba/NoG7BhYdZhwPw8XK38KWAdSQPz2UNxfjMza5A+nTlIGlIYPRCo3Mk0BRgraRVJGwMjgLuAacCIfGfSyqSL1lMiIoBbgM/l5ccD1/QlJjMzq59uzxwkXQrsCgyW1AacCOwqaSSpCWge8GWAiLhf0uXAA8Ay4KiIeD3XczRwAzAAmBQR9+dVfA+YLOlU4F7gvLptnZmZ9Um3ySEixlUp7vQfeEScBpxWpfw64Loq5XNJdzOZmVmT8C+kzcysxMnBzMxKnBzMzKzEycHMzEqcHMzMrMTJwczMSpwczMysxMnBzMxKnBzMzKzEycHMzEqcHMzMrMTJwczMSpwczMysxMnBzMxKnBzMzKzEycHMzEqcHMzMrMTJwczMSpwczMysxMnBzMxKuk0OkiZJWiRpVqHsDEkPSZoh6WpJ6+Ty4ZJeljQ9v35TWGYHSTMlzZF0liTl8nUlTZU0O78PWhEbamZmPdeTM4fzgdEdyqYC20TEtsA/gOMK0x6JiJH5dWSh/BxgAjAivyp1HgvcHBEjgJvzuJmZNVC3ySEibgMWdyi7MSKW5dE7gGFd1SFpCLBWRNweEQFcCByQJ48BLsjDFxTKzcysQepxzeHfgesL4xtLulfSnyV9PJcNBdoK87TlMoD1I2IBQH5fr7MVSZogqVVSa3t7ex1CNzOzampKDpKOB5YBF+eiBcD7I2J74JvAJZLWAlRl8ejt+iJiYkSMiohRLS0tfQ3bzMy6MbCvC0oaD+wH7JGbioiIpcDSPHy3pEeAzUlnCsWmp2HA/Dy8UNKQiFiQm58W9TUmMzOrjz6dOUgaDXwP2D8iXiqUt0gakIc3IV14npubi5ZI2jnfpXQYcE1ebAowPg+PL5SbmVmDdHvmIOlSYFdgsKQ24ETS3UmrAFPzHal35DuTPgGcImkZ8DpwZERULmZ/hXTn02qkaxSV6xSnA5dLOgL4J3BQXbbMzMz6rNvkEBHjqhSf18m8VwFXdTKtFdimSvnTwB7dxWFmZm8f/0LazMxKnBzMzKzEycHMzEqcHMzMrMTJwczMSvr8IzhbsXRytR+V912c2OsfpJtZP+YzBzMzK3FyMDOzEicHMzMrcXIwM7MSJwczMytxcjAzsxInBzMzK3FyMDOzEicHMzMrcXIwM7MSJwczMytxcjAzsxInBzMzK3FyMDOzEicHMzMr6VFykDRJ0iJJswpl60qaKml2fh+UyyXpLElzJM2Q9KHCMuPz/LMljS+U7yBpZl7mLEn1fZiBmZn1Sk/PHM4HRncoOxa4OSJGADfncYB9gBH5NQE4B1IyAU4EPgzsBJxYSSh5ngmF5Tquy8zM3kY9Sg4RcRuwuEPxGOCCPHwBcECh/MJI7gDWkTQE2BuYGhGLI+IZYCowOk9bKyJuj4gALizUZWZmDVDLNYf1I2IBQH5fL5cPBR4vzNeWy7oqb6tSXiJpgqRWSa3t7e01hG5mZl1ZERekq10viD6UlwsjJkbEqIgY1dLSUkOIZmbWlVqSw8LcJER+X5TL24ANC/MNA+Z3Uz6sSrmZmTVILclhClC542g8cE2h/LB819LOwHO52ekGYC9Jg/KF6L2AG/K0JZJ2zncpHVaoy8zMGmBgT2aSdCmwKzBYUhvprqPTgcslHQH8Ezgoz34dsC8wB3gJOBwgIhZL+iEwLc93SkRULnJ/hXRH1GrA9fllZmYN0qPkEBHjOpm0R5V5Aziqk3omAZOqlLcC2/QkFjMzW/H8C2kzMytxcjAzsxInBzMzK3FyMDOzEicHMzMr6dHdSu82OtmdvpqZdcVnDmZmVuLkYGZmJU4OZmZW4uRgZmYlTg5mZlbi5GBmZiVODmZmVuLkYGZmJU4OZmZW4uRgZmYlTg5mZlbi5GBmZiVODmZmVuLkYGZmJX1ODpK2kDS98Hpe0jGSTpL0RKF838Iyx0maI+lhSXsXykfnsjmSjq11o8zMrDZ9fp5DRDwMjASQNAB4ArgaOBz4RUT8rDi/pK2AscDWwAbATZI2z5N/BXwKaAOmSZoSEQ/0NTYzM6tNvR72swfwSEQ8JnX6IJ0xwOSIWAo8KmkOsFOeNici5gJImpzndXIwM2uQel1zGAtcWhg/WtIMSZMkDcplQ4HHC/O05bLOykskTZDUKqm1vb29TqGbmVlHNScHSSsD+wNX5KJzgE1JTU4LgDMrs1ZZPLooLxdGTIyIURExqqWlpaa4zcysc/VoVtoHuCciFgJU3gEk/Ra4No+2ARsWlhsGzM/DnZWbmVkD1KNZaRyFJiVJQwrTDgRm5eEpwFhJq0jaGBgB3AVMA0ZI2jifhYzN85qZWYPUdOYgaXXSXUZfLhT/VNJIUtPQvMq0iLhf0uWkC83LgKMi4vVcz9HADcAAYFJE3F9LXGZmVpuakkNEvAS8r0PZoV3MfxpwWpXy64DraonFzMzqx7+QNjOzEicHMzMrcXIwM7MSJwczMyupV/cZ1uR0cqfdmvRJnFj1d4pm9i7hMwczMytxcjAzsxInBzMzK3FyMDOzEicHMzMrcXIwM7MSJwczMytxcjAzsxInBzMzK3FyMDOzEicHMzMrcXIwM7MSJwczMytxcjAzsxInBzMzK6k5OUiaJ2mmpOmSWnPZupKmSpqd3wflckk6S9IcSTMkfahQz/g8/2xJ42uNy8zM+q5eZw67RcTIiBiVx48Fbo6IEcDNeRxgH2BEfk0AzoGUTIATgQ8DOwEnVhKKmZm9/VZUs9IY4II8fAFwQKH8wkjuANaRNATYG5gaEYsj4hlgKjB6BcVmZmbdqEdyCOBGSXdLmpDL1o+IBQD5fb1cPhR4vLBsWy7rrHw5kiZIapXU2t7eXofQzcysmno8Q3qXiJgvaT1gqqSHupi32oOMo4vy5QsiJgITAUaNGuWHGJuZrSA1nzlExPz8vgi4mnTNYGFuLiK/L8qztwEbFhYfBszvotzMzBqgpuQg6b2S1qwMA3sBs4ApQOWOo/HANXl4CnBYvmtpZ+C53Ox0A7CXpEH5QvReuczMzBqg1mal9YGrJVXquiQi/iRpGnC5pCOAfwIH5fmvA/YF5gAvAYcDRMRiST8EpuX5TomIxTXGZmZmfVRTcoiIucB2VcqfBvaoUh7AUZ3UNQmYVEs8ZmZWH/6FtJmZlTg5mJlZiZODmZmVODmYmVmJk4OZmZU4OZiZWYmTg5mZlTg5mJlZiZODmZmVODmYmVlJPbrstn5IJ1frZb3v4kT3wG7WTHzmYGZmJU4OZmZW4uRgZmYlTg5mZlbi5GBmZiVODmZmVuLkYGZmJU4OZmZW4uRgZmYlfU4OkjaUdIukByXdL+nrufwkSU9Imp5f+xaWOU7SHEkPS9q7UD46l82RdGxtm2RmZrWqpfuMZcC3IuIeSWsCd0uamqf9IiJ+VpxZ0lbAWGBrYAPgJkmb58m/Aj4FtAHTJE2JiAdqiM3MzGrQ5+QQEQuABXl4iaQHgaFdLDIGmBwRS4FHJc0BdsrT5kTEXABJk/O8Tg5mZg1Sl2sOkoYD2wN35qKjJc2QNEnSoFw2FHi8sFhbLuus3MzMGqTm5CBpDeAq4JiIeB44B9gUGEk6szizMmuVxaOL8mrrmiCpVVJre3t7raGbmVknakoOkt5DSgwXR8QfACJiYUS8HhFvAL/lraajNmDDwuLDgPldlJdExMSIGBURo1paWmoJ3czMulDL3UoCzgMejIifF8qHFGY7EJiVh6cAYyWtImljYARwFzANGCFpY0krky5aT+lrXGZmVrta7lbaBTgUmClpei77PjBO0khS09A84MsAEXG/pMtJF5qXAUdFxOsAko4GbgAGAJMi4v4a4jIzsxrVcrfSX6l+veC6LpY5DTitSvl1XS1nZmZvL/9C2szMSpwczMysxMnBzMxKnBzMzKyklruVzOpGJ1e7t6E2cWLV31KaWQ/4zMHMzEqcHMzMrMTJwczMSpwczMysxMnBzMxKnBzMzKzEycHMzEqcHMzMrMTJwczMSpwczMysxMnBzMxKnBzMzKzEHe/Zu1a9O/NzR37Wn/jMwczMSpwczMysxMnBzMxKmuaag6TRwC+BAcC5EXF6g0MyW46vYVh/0hTJQdIA4FfAp4A2YJqkKRHxQGMjM1tx/PQ7a2ZNkRyAnYA5ETEXQNJkYAzg5GDWCysi4fQ39U6w79QzzmZJDkOBxwvjbcCHO84kaQIwIY++IOnhPq5vMPBUH5d9uzR7jM0eHzR/jM0eH/TDGHVS3RNss8W3UU9mapbkUG1rS+kxIiYCE2temdQaEaNqrWdFavYYmz0+aP4Ymz0+cIz10OzxdaZZ7lZqAzYsjA8D5jcoFjOzfq9ZksM0YISkjSWtDIwFpjQ4JjOzfqspmpUiYpmko4EbSLeyToqI+1fgKmtumnobNHuMzR4fNH+MzR4fOMZ6aPb4qlKEb30zM7PlNUuzkpmZNREnBzMzK+l3yUHSaEkPS5oj6dgmiGeSpEWSZhXK1pU0VdLs/D6owTFuKOkWSQ9Kul/S15spTkmrSrpL0n05vpNz+caS7szxXZZvdmgoSQMk3Svp2maLUdI8STMlTZfUmsuaYh8XYlxH0pWSHsrfx480U4yStsifX+X1vKRjminGnupXyaHQTcc+wFbAOElbNTYqzgdGdyg7Frg5IkYAN+fxRloGfCsitgR2Bo7Kn1uzxLkU2D0itgNGAqMl7Qz8BPhFju8Z4IgGxVf0deDBwnizxbhbRIws3JffLPu44pfAnyLiA8B2pM+yaWKMiIfz5zcS2AF4Cbi6mWLssYjoNy/gI8ANhfHjgOOaIK7hwKzC+MPAkDw8BHi40TF2iPcaUj9YTRcnsDpwD+kX9k8BA6vt+wbFNoz0j2F34FrSjz+bJkZgHjC4Q1nT7GNgLeBR8o00zRhjh7j2Av7WzDF29epXZw5U76ZjaINi6cr6EbEAIL+v1+B43iRpOLA9cCdNFGdurpkOLAKmAo8Az0bEsjxLM+zr/wS+C7yRx99Hc8UYwI2S7s5d1UAT7WNgE6Ad+F1umjtX0nubLMaiscClebhZY+xUf0sOPeqmw6qTtAZwFXBMRDzf6HiKIuL1SKfyw0gdOW5Zbba3N6q3SNoPWBQRdxeLq8zayO/jLhHxIVKz61GSPtHAWKoZCHwIOCcitgdepEmbZ/K1o/2BKxodS1/1t+TwTummY6GkIQD5fVGD40HSe0iJ4eKI+EMubro4I+JZ4FbStZF1JFV+6Nnofb0LsL+kecBkUtPSf9JEMUbE/Py+iNROvhPNtY/bgLaIuDOPX0lKFs0UY8U+wD0RsTCPN2OMXepvyeGd0k3HFGB8Hh5PauNvGEkCzgMejIifFyY1RZySWiStk4dXA/YkXai8Bfhco+MDiIjjImJYRAwnfe/+NyIOoUlilPReSWtWhknt5bNokn0MEBFPAo9L2iIX7UHq1r9pYiwYx1tNStCcMXat0Rc93u4XsC/wD1Kb9PFNEM+lwALgNdKR0RGktuibgdn5fd0Gx/gxUnPHDGB6fu3bLHEC2wL35vhmASfk8k2Au4A5pNP7VRq9v3NcuwLXNlOMOY778uv+yt9Gs+zjQpwjgda8r/8IDGrCGFcHngbWLpQ1VYw9ebn7DDMzK+lvzUpmZtYDTg5mZlbi5GBmZiVODmZmVuLkYGZmJU4O73KSfiHpmML4DZLOLYyfKembfah3nqTBVcr3r6W329yD5ep9Xb4WnW1TjXWeImnPFVV/lfVVeladKekBSadKWqWO9R9Q7KyyuH11qHv74nezh8tMljSiHuu35Tk5vPv9HfgogKSVgMHA1oXpHwX+Vq+VRcSUiDi9hiqOId0n/o4naUBEnBARN9Whrt480ne3iPgg6RfOm9DLx1Tm3os7cwCpR2MA6rV92feB/+rlMueQ+quyOnNyePf7Gzk5kJLCLGCJpEH5iHJL4F5Ja0i6WdI9+ahzDLz5y9n/p/SshFmSDi7U/dXC/B/I839B0tl5+HxJZ0n6u6S5kj6Xy1eS9GulZy9cK+k6SZ+T9DVgA+AWSbfkecfl+mdJ+kllxZJekHRajusOSet33HBJnyz0q3+vpDUl7ar8LIU8z9mSvlBY7DtKz4a4S9JmeZ6D8vrvk3RbLhsg6Wc5thmSvprL50k6QdJfgYPyZ/C5bupvkXSVpGn5tUsuP0nSREk3AhdK2jovNz2vs8sj5oh4ATgSOEDpeQKdbnuVuL+UY7kvx7a6pI+S+gs6I8ewaXH7JO2RP+eZSs8pWaVQ98kdvysd9tWawLYRcV9h2y+QdGNe/rOSfpqX/5NSdy4AfwH27GXytB5wcniXi9RfzjJJ7yclidtJPap+BBgFzIiIV4FXgAMjdby2G3CmJJGeNTE/IraLiG2APxWqfyrPfw7w7U5CGEL6hfV+QOWM4rOkbso/CHwxx0JEnEXqW2i3iNhN0gak5x3sTvpl7I6SDsh1vBe4I9IzHG4DvlRl3d8GjorUId/HgZd78JE9HxE7AWeT+j4COAHYO69r/1w2AdgY2D4itgUuLtTxSkR8LCIm97D+X5Ke6bAj8C9AsWllB2BMRPwb6R/9L/P2jCL9or5LkTpIfBToSdNLMe4/RMSOeZsfBI6IiL+TuoH4TqRnFjxSWVDSqqRnkxycz1oGAl8p1N3dd2UU6cClaFPg08AY4CLgllz3y7mciHiD9Ovy7XqwfdYLTg79Q+XsoZIcbi+M/z3PI+BHkmYAN5G6jl4fmEk6MvuJpI9HxHOFeisd8N1N+mdfzR8j4o2IeCDXBylZXJHLnyT1L1TNjsCtEdEeqVvri4FKT6Gvkp6J0NX6/wb8PJ+RrBNvdY3dlUsL7x8p1HO+pC8BlSaXPYHfVOqMiMWFOi7rZf17AmcrdTk+BVgrH0kDTImISlK7Hfi+pO8BGxXKu1Ot99dqinFvI+kvkmYCh7B8U2Q1WwCPRsQ/8vgFvLWvoPvvyhBSd9xF10fEa6Tv4ADeOjCZ2aGORaQzTqsjJ4f+oXLd4YOko7M7SP+YitcbDgFagB3ykelCYNX8x74D6Q/yx5JOKNS7NL+/TjpSrGZpYVgd3rvT1XyvxVt9v1Rdf7728UVgNeCO3JyxjOW/96t2XKzjcEQcCfyA1KPvdEnvy7F11vfMi13EXao/x/ORfDQ+MiKGRsSSjnVFxCWkM5eXgRsk7d7FeoA3m2uGk/oT627bi3GfDxydj9RPrjJvaVXdTO/uu/JylXUshTfPDor7+40OdaxKz84KrRecHPqHv5GadRZHeu7BYmAdUoK4Pc+zNul5A69J2g3YCCA37bwUERcBPyN1kVyrvwL/kq89rE/qiK5iCVA5ar4T+KSkwUoXSccBf+7pSiRtGhEzI+InpM7aPgA8BmwlaRVJa5N69izqn9OjAAABvklEQVQ6uPB+e6GeOyPiBNKT2zYEbgSOrLR1S1q3h2GV6s91HV2Ie2Qn27MJMDc3v00hdTjYKaXnb/yadPb2DN1ve9GawILctn9Ioby4f4oeAoZXrqMAh9KLfUVqutqs27mq25zUWaDVkS/i9A8zSXcpXdKhbI2IeCqPXwz8j9KD5aeT/tghnW2cIekNUs+xxXbkvrqK9I9pFumI9k6g0lw1Ebhe0oJ83eE4UrOTgOsiojddHR+TE93rpK6dr4+IpZIuJ/XqOZvUm2vRKpLuJB04jctlZ+SLvyL1qHlfjn1zYIak14Dfkq4jdKda/V8DfpWb9AaSrqEcWWXZg4HP5/U9CZzSyTpuydeLViI9l+GHABHxeDfbXvQfpP3yGOm7UkkIk4Hf5qa6Ny+0R8Qrkg4HrsgJcxrwmy7qX05EPCRpbUlrFs6aupUPLl6O/JQ1qx/3ymoNIWmNiHghN9HcRXoK2ZONjssaR9I3gCUR0ePfOuRlno+I81ZcZP2TzxysUa5VekDPysAPnRiMdCfTQb1c5lng9ysgln7PZw5mZlbiC9JmZlbi5GBmZiVODmZmVuLkYGZmJU4OZmZW8v8BcdrdY10hsyUAAAAASUVORK5CYII=)


![pandas bar](https://udacity-reviews-uploads.s3.us-west-2.amazonaws.com/_attachments/67065/1514970688/TIM%E6%88%AA%E5%9B%BE20180103162043.png)