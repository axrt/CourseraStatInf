# Lecture 2
Alexander Tuzhikov  
September 10, 2015  

#The variance

The variance of a random variable is a measure of spread. The square root of variance is standard deviation.

The average of random sample from a population is itself a random variable. We call the standard deviation of a statistic a standard error.

```r
if(!require("ggplot2")){
        install.packages("ggplot2")
        library("ggplot2")
}
```

```
## Loading required package: ggplot2
```

```r
if(!require("UsingR")){
        install.packages("UsingR")
        library("UsingR")
}
```

```
## Loading required package: UsingR
## Loading required package: MASS
## Loading required package: HistData
## Loading required package: Hmisc
## Loading required package: grid
## Loading required package: lattice
## Loading required package: survival
## Loading required package: Formula
## 
## Attaching package: 'Hmisc'
## 
## The following objects are masked from 'package:base':
## 
##     format.pval, round.POSIXt, trunc.POSIXt, units
## 
## 
## Attaching package: 'UsingR'
## 
## The following object is masked from 'package:survival':
## 
##     cancer
## 
## The following object is masked from 'package:ggplot2':
## 
##     movies
```


```r
#norm
nosim<- 1000
n<- 10
sd(apply(matrix(rnorm(nosim*n),nosim),1,mean))
```

```
## [1] 0.3178546
```

```r
sqrt(n)
```

```
## [1] 3.162278
```

```r
#unif
sd(apply(matrix(runif(nosim*n),nosim),1,mean))
```

```
## [1] 0.09284279
```

```r
1/sqrt(12*n)
```

```
## [1] 0.09128709
```

```r
#pois
sd(apply(matrix(rpois(nosim*n, 4),nosim),1,mean))
```

```
## [1] 0.6303838
```

```r
2/sqrt(n)
```

```
## [1] 0.6324555
```


```r
choose(8,7)*0.5^8 + choose(8,8) * 0.5^8
```

```
## [1] 0.03515625
```

```r
pbinom(6, size=8, prob=0.5, lower.tail = FALSE)
```

```
## [1] 0.03515625
```


```r
pnorm(1160, mean=1020, sd=50, lower.tail=FALSE)
```

```
## [1] 0.00255513
```

```r
pnorm(2.8, lower.tail = FALSE)
```

```
## [1] 0.00255513
```

```r
qnorm(0.75, mean=1020, sd=50)
```

```
## [1] 1053.724
```


```r
ppois(3, lambda=2.5*4)
```

```
## [1] 0.01033605
```

```r
pbinom(2, size=500, prob=0.01)
```

```
## [1] 0.1233858
```

```r
ppois(2, lambda = 500 * 0.01)
```

```
## [1] 0.124652
```

```r
n<- 1000
cumsum(rnorm(n))/(1:n)
```

```
##    [1] -0.774393056 -0.402905029 -0.347959227 -0.496587972  0.098948280
##    [6] -0.204525267 -0.205484498 -0.071943173  0.021221305  0.045499952
##   [11]  0.077462274  0.097089805  0.101400469 -0.011796493 -0.056668781
##   [16] -0.070326591 -0.008801833 -0.015273967  0.032228918  0.023553898
##   [21]  0.069429022  0.065686252  0.114203973  0.108535372  0.084210142
##   [26]  0.136387018  0.156622606  0.203003179  0.168332973  0.188940187
##   [31]  0.154654917  0.200973349  0.204598969  0.199886541  0.148817949
##   [36]  0.167692837  0.171345312  0.196559192  0.206033897  0.214838786
##   [41]  0.244025534  0.215423246  0.242707266  0.212067625  0.181073687
##   [46]  0.196975301  0.185500846  0.157988053  0.151630945  0.138207381
##   [51]  0.130948911  0.080766814  0.114526512  0.138371200  0.134971692
##   [56]  0.131367770  0.088647962  0.060704253  0.044433941  0.035843996
##   [61]  0.038084422  0.029195084  0.028632862  0.036687672  0.039576772
##   [66]  0.024220069  0.024169830  0.034099726  0.035929658  0.018036266
##   [71] -0.003443240 -0.005726902  0.009011155 -0.004439825 -0.024504732
##   [76] -0.034067125 -0.025648857 -0.016706308 -0.012350232  0.008108916
##   [81] -0.005784128  0.009058294  0.002988287  0.006982475  0.009663408
##   [86] -0.001353809  0.004956769  0.013969596  0.027977110  0.024202450
##   [91]  0.016700925  0.006118898  0.012948873  0.003579419 -0.002336946
##   [96] -0.001341028  0.012314375  0.015252192  0.009969860  0.016838614
##  [101]  0.012526451  0.016112021  0.036392233  0.028594290  0.049661602
##  [106]  0.059560928  0.046627983  0.043603637  0.043534583  0.042737980
##  [111]  0.041330278  0.041204296  0.031265637  0.026555148  0.029272346
##  [116]  0.041085476  0.041956267  0.055252522  0.053178761  0.038813655
##  [121]  0.051377580  0.056208951  0.059603066  0.057382588  0.061510794
##  [126]  0.056287532  0.059010051  0.060500714  0.059769840  0.058606530
##  [131]  0.070840280  0.073833794  0.074411960  0.077964733  0.076584398
##  [136]  0.083619773  0.083100555  0.090439817  0.080541418  0.077346877
##  [141]  0.080366422  0.078536561  0.085750089  0.085940583  0.083513316
##  [146]  0.089083592  0.088545105  0.083324314  0.071022836  0.078231768
##  [151]  0.075348435  0.063909055  0.070300149  0.072985636  0.086358634
##  [156]  0.089516537  0.087623648  0.090288182  0.084718436  0.087903165
##  [161]  0.087299640  0.093525850  0.099701155  0.096603940  0.096770812
##  [166]  0.092827136  0.092761429  0.096089467  0.099027806  0.109866055
##  [171]  0.102540178  0.101820799  0.106204619  0.105509468  0.093983509
##  [176]  0.093741880  0.083871931  0.078403667  0.072531312  0.073053118
##  [181]  0.069532048  0.067320995  0.076537102  0.068367382  0.061712444
##  [186]  0.062500604  0.062373136  0.067932138  0.063420109  0.062643660
##  [191]  0.067484529  0.069305469  0.075047504  0.071041606  0.064234292
##  [196]  0.058523397  0.058943084  0.058594600  0.054641948  0.049772562
##  [201]  0.050263840  0.051412415  0.058209018  0.068227209  0.070025167
##  [206]  0.066634705  0.058300600  0.060125537  0.056966314  0.055505638
##  [211]  0.052386216  0.054548361  0.051882263  0.058210246  0.064897323
##  [216]  0.069914823  0.073424680  0.067746176  0.066021128  0.065838709
##  [221]  0.063276518  0.057837383  0.056338698  0.058689790  0.059158727
##  [226]  0.061494743  0.055208724  0.058199518  0.051172129  0.048651483
##  [231]  0.050736600  0.049297450  0.045839029  0.039512162  0.033815470
##  [236]  0.029224461  0.034982754  0.038738386  0.040244803  0.047756683
##  [241]  0.049472504  0.053502174  0.047990615  0.051855803  0.046862529
##  [246]  0.061977420  0.059196225  0.060311891  0.058189513  0.059962973
##  [251]  0.055209622  0.051005835  0.052358944  0.060546837  0.063109739
##  [256]  0.054969841  0.059735198  0.061652894  0.071076759  0.068129208
##  [261]  0.060598453  0.060339824  0.069544300  0.072518653  0.065532761
##  [266]  0.060519716  0.058066390  0.052587174  0.055571465  0.057802369
##  [271]  0.055654523  0.051048971  0.048090889  0.049344863  0.051084800
##  [276]  0.045645669  0.050184779  0.048029944  0.047928251  0.048782565
##  [281]  0.050669198  0.052478032  0.049798969  0.047717177  0.056210315
##  [286]  0.051033470  0.057728203  0.056225777  0.052262613  0.045197303
##  [291]  0.049335203  0.051482484  0.053291721  0.047953122  0.047923436
##  [296]  0.050569509  0.052967882  0.052988562  0.055350890  0.058180812
##  [301]  0.052686457  0.053111207  0.055804270  0.057716997  0.062341397
##  [306]  0.061785384  0.059375212  0.062980421  0.063236756  0.061087623
##  [311]  0.065225783  0.068346512  0.070104585  0.071925760  0.070608328
##  [316]  0.067273770  0.067054242  0.064946081  0.070897379  0.074695136
##  [321]  0.073378844  0.072119879  0.070743358  0.070237887  0.066462999
##  [326]  0.070488451  0.069931835  0.069605548  0.070694078  0.067098999
##  [331]  0.067301328  0.066159242  0.070099385  0.069206019  0.069294821
##  [336]  0.069495964  0.065712930  0.070050212  0.069528512  0.068883115
##  [341]  0.069825759  0.067007596  0.065367519  0.062803123  0.061363343
##  [346]  0.063253315  0.068752233  0.067884235  0.069727230  0.071754115
##  [351]  0.070025499  0.066203872  0.069671909  0.067742343  0.058521543
##  [356]  0.056626837  0.060032494  0.060137163  0.063995218  0.062698519
##  [361]  0.060223016  0.060047493  0.061824294  0.059022815  0.061482622
##  [366]  0.061831276  0.057949380  0.056518953  0.056576344  0.055874459
##  [371]  0.053819111  0.054369780  0.054891842  0.052402932  0.052561639
##  [376]  0.051327537  0.054763503  0.046306265  0.049921262  0.051185053
##  [381]  0.047388783  0.049746661  0.051404339  0.049989925  0.043713227
##  [386]  0.041935817  0.034856246  0.036301688  0.034271275  0.036607153
##  [391]  0.035757608  0.039491095  0.037493917  0.041129144  0.042508639
##  [396]  0.041130536  0.043844731  0.039067874  0.043158003  0.042165208
##  [401]  0.045696384  0.043448390  0.044778457  0.047035331  0.045621858
##  [406]  0.051049152  0.051162584  0.050551450  0.048888168  0.051240873
##  [411]  0.053170716  0.055945504  0.054019733  0.050659071  0.052565246
##  [416]  0.053800662  0.056205968  0.055616252  0.055035089  0.054638625
##  [421]  0.054687783  0.059117425  0.059844158  0.059420773  0.059692204
##  [426]  0.063390637  0.064007922  0.057876141  0.054210202  0.052273607
##  [431]  0.054577028  0.054424388  0.055712959  0.056885097  0.053200002
##  [436]  0.054457082  0.053387649  0.052181546  0.049830265  0.047774139
##  [441]  0.049299708  0.047950804  0.049304856  0.047362272  0.042216440
##  [446]  0.039951658  0.038812499  0.040617580  0.041934910  0.039091597
##  [451]  0.040144386  0.043363386  0.043349224  0.043074800  0.041909615
##  [456]  0.043296598  0.042784297  0.039983564  0.037765070  0.035837510
##  [461]  0.036645313  0.037253048  0.037412763  0.036237103  0.034336871
##  [466]  0.032491971  0.029768883  0.026798534  0.027732925  0.029836255
##  [471]  0.030036878  0.029537280  0.032494726  0.031141227  0.029441615
##  [476]  0.030527599  0.027985900  0.031636683  0.032576137  0.033317092
##  [481]  0.031860820  0.033832284  0.031992336  0.034685185  0.033776320
##  [486]  0.033991210  0.033761022  0.035489541  0.037614709  0.037326277
##  [491]  0.037683041  0.037590312  0.039573743  0.035445297  0.034873466
##  [496]  0.034338544  0.037768190  0.036164119  0.038611363  0.035003831
##  [501]  0.031793908  0.030725478  0.031251039  0.034056197  0.035624871
##  [506]  0.033262822  0.033992067  0.032698297  0.032833597  0.033530779
##  [511]  0.033500090  0.034523602  0.036910389  0.041153649  0.038956457
##  [516]  0.038813057  0.039370876  0.041682911  0.043421992  0.040688731
##  [521]  0.044261818  0.047180579  0.047032717  0.048135795  0.044747336
##  [526]  0.041332323  0.037758611  0.035855600  0.032756520  0.032833731
##  [531]  0.033297540  0.034474445  0.033208687  0.031938904  0.032024240
##  [536]  0.032248679  0.033894203  0.033514853  0.035961692  0.034813477
##  [541]  0.033752471  0.035145001  0.033165120  0.034105046  0.032461118
##  [546]  0.031427900  0.028462754  0.028919863  0.029865602  0.030201718
##  [551]  0.029942586  0.030562059  0.030635480  0.033460175  0.032175195
##  [556]  0.036236809  0.037816177  0.038233050  0.041353229  0.039390324
##  [561]  0.037912469  0.039715525  0.040325122  0.039626023  0.040889199
##  [566]  0.038940010  0.036178013  0.035653316  0.035108545  0.037000042
##  [571]  0.035871305  0.035889108  0.032837294  0.033728435  0.032914458
##  [576]  0.032807675  0.030896675  0.030125601  0.034351503  0.034342398
##  [581]  0.035678427  0.034706779  0.034355331  0.034249792  0.030500435
##  [586]  0.033270477  0.034241394  0.033047535  0.034856632  0.033842198
##  [591]  0.033577476  0.032807399  0.033598820  0.031494588  0.028988994
##  [596]  0.027897212  0.026605991  0.030236005  0.032753293  0.029923073
##  [601]  0.029386647  0.029115222  0.028119839  0.024861847  0.024635078
##  [606]  0.024611186  0.024121167  0.024460537  0.023668260  0.021680988
##  [611]  0.019805332  0.021624625  0.017907805  0.016517629  0.018848573
##  [616]  0.018987544  0.017947800  0.017178148  0.016092482  0.015228272
##  [621]  0.015469924  0.014070521  0.015009673  0.011829347  0.011467812
##  [626]  0.011685048  0.013058420  0.012222132  0.010915496  0.010411729
##  [631]  0.009677569  0.011074928  0.011856736  0.013189253  0.012947119
##  [636]  0.012781981  0.011601699  0.008023725  0.006398499  0.007647880
##  [641]  0.006471790  0.005549617  0.006220783  0.007878175  0.010499388
##  [646]  0.009165319  0.009147503  0.008770736  0.006856264  0.006416452
##  [651]  0.004514548  0.004666023  0.002796044  0.003797755  0.004171391
##  [656]  0.004523325  0.004609325  0.005519296  0.005728768  0.005575389
##  [661]  0.004197787  0.005902851  0.006302674  0.007552056  0.009537832
##  [666]  0.012325078  0.012514814  0.012133018  0.011051716  0.010879024
##  [671]  0.012378107  0.013781214  0.013999368  0.011134580  0.010247703
##  [676]  0.011868518  0.009388055  0.010212996  0.012059973  0.010936126
##  [681]  0.011064234  0.011202713  0.013128837  0.014213504  0.015031547
##  [686]  0.019134535  0.018444391  0.019690003  0.020302837  0.020863521
##  [691]  0.023477672  0.022865488  0.020098615  0.022331139  0.025713711
##  [696]  0.025653883  0.025647711  0.022758429  0.023722707  0.024170122
##  [701]  0.022151268  0.023207905  0.024941353  0.026382237  0.026912478
##  [706]  0.026771258  0.026675183  0.025688628  0.025992381  0.026788744
##  [711]  0.026483906  0.029954712  0.029795612  0.027791153  0.027136644
##  [716]  0.027195680  0.028019577  0.028195705  0.027126429  0.028037553
##  [721]  0.026669696  0.025251493  0.025793568  0.027880679  0.029321509
##  [726]  0.028819264  0.028670579  0.029178993  0.029654875  0.031359384
##  [731]  0.029804666  0.029183469  0.027967911  0.029401126  0.030144689
##  [736]  0.030573340  0.030497299  0.029034063  0.030981710  0.029694127
##  [741]  0.027178577  0.028503329  0.028297660  0.030942336  0.031773152
##  [746]  0.032715241  0.031702442  0.031751958  0.030431874  0.031554798
##  [751]  0.029509094  0.030127786  0.031659234  0.031503857  0.031847457
##  [756]  0.032180045  0.031370506  0.031283473  0.030047330  0.032002298
##  [761]  0.033689593  0.033351428  0.031887786  0.031502702  0.030435073
##  [766]  0.029284138  0.029534763  0.030771390  0.030537614  0.030751818
##  [771]  0.029867187  0.031489442  0.031080242  0.032104307  0.033958775
##  [776]  0.033686631  0.032944602  0.029473026  0.029889268  0.029089820
##  [781]  0.030905354  0.028169987  0.026323564  0.026535689  0.024698981
##  [786]  0.025825670  0.026991999  0.027867345  0.027784712  0.028195841
##  [791]  0.027609224  0.028581594  0.027379671  0.026917135  0.028820924
##  [796]  0.027900399  0.027223888  0.027742864  0.028914198  0.028348986
##  [801]  0.027233413  0.026475000  0.027680216  0.027588015  0.028984667
##  [806]  0.027094638  0.027865586  0.028527845  0.031265815  0.032178602
##  [811]  0.032139097  0.033087933  0.033893861  0.033386688  0.033336840
##  [816]  0.032734843  0.031297730  0.031327582  0.031327375  0.030936377
##  [821]  0.030181494  0.029536040  0.027107811  0.026441280  0.027911889
##  [826]  0.028571010  0.029735856  0.029564654  0.029747067  0.030829677
##  [831]  0.029654818  0.029702047  0.031349168  0.030197063  0.029424399
##  [836]  0.027299698  0.028013230  0.025451887  0.025217507  0.025940823
##  [841]  0.023159585  0.022000118  0.019737945  0.019610367  0.019927670
##  [846]  0.020311389  0.019183483  0.020590624  0.020643464  0.021711005
##  [851]  0.022488961  0.021986840  0.022096939  0.023578553  0.025621257
##  [856]  0.024222558  0.023186804  0.023099309  0.021847830  0.021900270
##  [861]  0.020335394  0.019858316  0.018266639  0.018363749  0.017154899
##  [866]  0.017233899  0.018438705  0.020022237  0.019519850  0.018708152
##  [871]  0.018213168  0.016957224  0.018163178  0.018352918  0.019556147
##  [876]  0.019521600  0.020309929  0.020605111  0.020759453  0.021215223
##  [881]  0.019693361  0.019433489  0.021548395  0.020490166  0.020196926
##  [886]  0.022792964  0.022566072  0.021767459  0.021328957  0.021360545
##  [891]  0.021883962  0.021297618  0.021594679  0.021502307  0.021426521
##  [896]  0.020132767  0.021439501  0.020321525  0.021806882  0.022610853
##  [901]  0.022776498  0.022485765  0.022430725  0.021992090  0.023615399
##  [906]  0.024277929  0.023305359  0.025122512  0.025671912  0.027217342
##  [911]  0.026646434  0.026496449  0.026897479  0.025260172  0.024943583
##  [916]  0.025503116  0.025483783  0.024017073  0.025376063  0.025705921
##  [921]  0.025935912  0.025557616  0.025439720  0.027255866  0.025656239
##  [926]  0.026470361  0.027902882  0.028025462  0.029552079  0.028618500
##  [931]  0.028390655  0.029936211  0.030901240  0.030231062  0.030744824
##  [936]  0.030661711  0.030851464  0.032119233  0.033462517  0.033274063
##  [941]  0.032808321  0.031998817  0.031336075  0.032273215  0.033664687
##  [946]  0.032974074  0.032183961  0.033041180  0.032384405  0.032457089
##  [951]  0.032190483  0.033321662  0.034883596  0.034311390  0.034164475
##  [956]  0.033582553  0.032871021  0.032538346  0.032445455  0.032037329
##  [961]  0.031848074  0.032706652  0.032529978  0.032736316  0.031810803
##  [966]  0.032997235  0.034438746  0.032257898  0.032447341  0.032251961
##  [971]  0.032239602  0.033594710  0.033548792  0.032728163  0.030803964
##  [976]  0.031888342  0.031802706  0.030711492  0.029915402  0.030581691
##  [981]  0.029816383  0.029937086  0.030152390  0.031216154  0.031293299
##  [986]  0.030979314  0.031005501  0.031540257  0.031433825  0.031863751
##  [991]  0.031999146  0.033195639  0.031247284  0.029835460  0.031813731
##  [996]  0.031237777  0.029633094  0.029032957  0.027233244  0.027225510
```

```r
cumsum(sample(0:1, n, replace=TRUE))/(1:n)
```

```
##    [1] 0.0000000 0.5000000 0.3333333 0.5000000 0.6000000 0.6666667
##    [7] 0.5714286 0.5000000 0.4444444 0.5000000 0.4545455 0.5000000
##   [13] 0.5384615 0.5714286 0.5333333 0.5000000 0.4705882 0.5000000
##   [19] 0.4736842 0.4500000 0.4761905 0.4545455 0.4782609 0.4583333
##   [25] 0.4800000 0.4615385 0.4444444 0.4642857 0.4827586 0.4666667
##   [31] 0.4838710 0.4687500 0.4848485 0.5000000 0.5142857 0.5277778
##   [37] 0.5405405 0.5263158 0.5384615 0.5250000 0.5121951 0.5238095
##   [43] 0.5116279 0.5227273 0.5333333 0.5217391 0.5319149 0.5208333
##   [49] 0.5306122 0.5200000 0.5098039 0.5000000 0.5094340 0.5000000
##   [55] 0.5090909 0.5000000 0.4912281 0.5000000 0.5084746 0.5166667
##   [61] 0.5081967 0.5000000 0.5079365 0.5156250 0.5230769 0.5151515
##   [67] 0.5223881 0.5294118 0.5217391 0.5285714 0.5352113 0.5416667
##   [73] 0.5479452 0.5540541 0.5600000 0.5657895 0.5714286 0.5641026
##   [79] 0.5569620 0.5500000 0.5432099 0.5487805 0.5542169 0.5595238
##   [85] 0.5647059 0.5697674 0.5747126 0.5681818 0.5617978 0.5555556
##   [91] 0.5604396 0.5543478 0.5483871 0.5531915 0.5473684 0.5520833
##   [97] 0.5567010 0.5510204 0.5454545 0.5500000 0.5445545 0.5490196
##  [103] 0.5436893 0.5384615 0.5428571 0.5471698 0.5420561 0.5462963
##  [109] 0.5412844 0.5363636 0.5315315 0.5357143 0.5398230 0.5438596
##  [115] 0.5391304 0.5431034 0.5470085 0.5423729 0.5378151 0.5416667
##  [121] 0.5454545 0.5491803 0.5447154 0.5403226 0.5440000 0.5396825
##  [127] 0.5354331 0.5390625 0.5348837 0.5307692 0.5343511 0.5303030
##  [133] 0.5338346 0.5298507 0.5259259 0.5294118 0.5255474 0.5289855
##  [139] 0.5251799 0.5285714 0.5248227 0.5211268 0.5174825 0.5208333
##  [145] 0.5172414 0.5136986 0.5170068 0.5135135 0.5167785 0.5133333
##  [151] 0.5165563 0.5131579 0.5163399 0.5129870 0.5096774 0.5064103
##  [157] 0.5031847 0.5063291 0.5031447 0.5000000 0.4968944 0.5000000
##  [163] 0.5030675 0.5060976 0.5030303 0.5000000 0.4970060 0.4940476
##  [169] 0.4911243 0.4941176 0.4912281 0.4883721 0.4855491 0.4885057
##  [175] 0.4857143 0.4829545 0.4802260 0.4831461 0.4804469 0.4777778
##  [181] 0.4806630 0.4835165 0.4863388 0.4836957 0.4810811 0.4784946
##  [187] 0.4812834 0.4840426 0.4867725 0.4894737 0.4921466 0.4895833
##  [193] 0.4870466 0.4896907 0.4871795 0.4846939 0.4873096 0.4848485
##  [199] 0.4824121 0.4800000 0.4776119 0.4752475 0.4778325 0.4803922
##  [205] 0.4829268 0.4854369 0.4830918 0.4807692 0.4784689 0.4761905
##  [211] 0.4739336 0.4764151 0.4741784 0.4719626 0.4697674 0.4675926
##  [217] 0.4654378 0.4633028 0.4611872 0.4636364 0.4615385 0.4639640
##  [223] 0.4663677 0.4687500 0.4666667 0.4646018 0.4669604 0.4692982
##  [229] 0.4716157 0.4739130 0.4761905 0.4784483 0.4763948 0.4743590
##  [235] 0.4765957 0.4745763 0.4767932 0.4789916 0.4769874 0.4791667
##  [241] 0.4771784 0.4793388 0.4773663 0.4754098 0.4775510 0.4756098
##  [247] 0.4736842 0.4717742 0.4698795 0.4680000 0.4701195 0.4682540
##  [253] 0.4664032 0.4685039 0.4666667 0.4687500 0.4708171 0.4728682
##  [259] 0.4749035 0.4769231 0.4789272 0.4809160 0.4790875 0.4772727
##  [265] 0.4754717 0.4774436 0.4794007 0.4813433 0.4832714 0.4814815
##  [271] 0.4797048 0.4816176 0.4798535 0.4817518 0.4800000 0.4818841
##  [277] 0.4837545 0.4856115 0.4874552 0.4857143 0.4875445 0.4858156
##  [283] 0.4876325 0.4894366 0.4912281 0.4930070 0.4947735 0.4930556
##  [289] 0.4948097 0.4965517 0.4982818 0.4965753 0.4948805 0.4965986
##  [295] 0.4949153 0.4932432 0.4949495 0.4932886 0.4916388 0.4900000
##  [301] 0.4883721 0.4900662 0.4884488 0.4901316 0.4885246 0.4901961
##  [307] 0.4885993 0.4902597 0.4886731 0.4870968 0.4855305 0.4839744
##  [313] 0.4856230 0.4872611 0.4888889 0.4873418 0.4858044 0.4874214
##  [319] 0.4890282 0.4875000 0.4859813 0.4875776 0.4891641 0.4907407
##  [325] 0.4923077 0.4907975 0.4892966 0.4878049 0.4863222 0.4878788
##  [331] 0.4894260 0.4879518 0.4864865 0.4880240 0.4865672 0.4851190
##  [337] 0.4836795 0.4822485 0.4808260 0.4794118 0.4809384 0.4795322
##  [343] 0.4810496 0.4796512 0.4782609 0.4768786 0.4783862 0.4770115
##  [349] 0.4785100 0.4771429 0.4757835 0.4744318 0.4759207 0.4745763
##  [355] 0.4732394 0.4719101 0.4733894 0.4748603 0.4763231 0.4750000
##  [361] 0.4764543 0.4751381 0.4738292 0.4752747 0.4767123 0.4754098
##  [367] 0.4741144 0.4755435 0.4769648 0.4783784 0.4770889 0.4758065
##  [373] 0.4745308 0.4759358 0.4746667 0.4760638 0.4748011 0.4761905
##  [379] 0.4749340 0.4763158 0.4776903 0.4790576 0.4778068 0.4791667
##  [385] 0.4805195 0.4792746 0.4780362 0.4768041 0.4755784 0.4769231
##  [391] 0.4757033 0.4744898 0.4758270 0.4746193 0.4759494 0.4747475
##  [397] 0.4735516 0.4723618 0.4736842 0.4725000 0.4738155 0.4726368
##  [403] 0.4714640 0.4727723 0.4740741 0.4753695 0.4766585 0.4754902
##  [409] 0.4767726 0.4780488 0.4768856 0.4781553 0.4794189 0.4782609
##  [415] 0.4795181 0.4807692 0.4820144 0.4832536 0.4844869 0.4857143
##  [421] 0.4869359 0.4881517 0.4869976 0.4882075 0.4870588 0.4882629
##  [427] 0.4894614 0.4906542 0.4895105 0.4906977 0.4918794 0.4930556
##  [433] 0.4942263 0.4930876 0.4919540 0.4908257 0.4897025 0.4885845
##  [439] 0.4874715 0.4886364 0.4875283 0.4864253 0.4875847 0.4887387
##  [445] 0.4876404 0.4865471 0.4854586 0.4843750 0.4832962 0.4844444
##  [451] 0.4833703 0.4845133 0.4834437 0.4845815 0.4835165 0.4846491
##  [457] 0.4857768 0.4847162 0.4836601 0.4826087 0.4837310 0.4848485
##  [463] 0.4859611 0.4870690 0.4860215 0.4871245 0.4882227 0.4871795
##  [469] 0.4882729 0.4872340 0.4883227 0.4894068 0.4883721 0.4873418
##  [475] 0.4863158 0.4873950 0.4863732 0.4853556 0.4843424 0.4854167
##  [481] 0.4844075 0.4854772 0.4844720 0.4834711 0.4824742 0.4814815
##  [487] 0.4804928 0.4815574 0.4826176 0.4836735 0.4826884 0.4817073
##  [493] 0.4807302 0.4817814 0.4828283 0.4818548 0.4808853 0.4819277
##  [499] 0.4809619 0.4820000 0.4810379 0.4800797 0.4811133 0.4801587
##  [505] 0.4792079 0.4802372 0.4792899 0.4783465 0.4774067 0.4764706
##  [511] 0.4774951 0.4765625 0.4775828 0.4785992 0.4796117 0.4786822
##  [517] 0.4796905 0.4806950 0.4816956 0.4807692 0.4817658 0.4808429
##  [523] 0.4818356 0.4809160 0.4800000 0.4809886 0.4800759 0.4791667
##  [529] 0.4782609 0.4792453 0.4783427 0.4774436 0.4784240 0.4794007
##  [535] 0.4785047 0.4776119 0.4767225 0.4758364 0.4768089 0.4777778
##  [541] 0.4768946 0.4778598 0.4769797 0.4761029 0.4770642 0.4780220
##  [547] 0.4789762 0.4781022 0.4772313 0.4781818 0.4773140 0.4764493
##  [553] 0.4773960 0.4783394 0.4792793 0.4784173 0.4793537 0.4802867
##  [559] 0.4812165 0.4803571 0.4795009 0.4786477 0.4777975 0.4769504
##  [565] 0.4761062 0.4752650 0.4761905 0.4753521 0.4762742 0.4771930
##  [571] 0.4781086 0.4790210 0.4799302 0.4790941 0.4800000 0.4809028
##  [577] 0.4818024 0.4826990 0.4835924 0.4844828 0.4853701 0.4862543
##  [583] 0.4871355 0.4863014 0.4871795 0.4863481 0.4872232 0.4863946
##  [589] 0.4855688 0.4847458 0.4839255 0.4831081 0.4822934 0.4814815
##  [595] 0.4806723 0.4815436 0.4824121 0.4832776 0.4824708 0.4816667
##  [601] 0.4825291 0.4817276 0.4809287 0.4801325 0.4809917 0.4801980
##  [607] 0.4810544 0.4802632 0.4794745 0.4803279 0.4811784 0.4820261
##  [613] 0.4828711 0.4837134 0.4829268 0.4821429 0.4829822 0.4838188
##  [619] 0.4846527 0.4838710 0.4847021 0.4855305 0.4847512 0.4839744
##  [625] 0.4832000 0.4824281 0.4816587 0.4808917 0.4817170 0.4809524
##  [631] 0.4801902 0.4794304 0.4786730 0.4794953 0.4803150 0.4795597
##  [637] 0.4788069 0.4796238 0.4788732 0.4781250 0.4773791 0.4781931
##  [643] 0.4774495 0.4782609 0.4790698 0.4783282 0.4775889 0.4783951
##  [649] 0.4776579 0.4784615 0.4777266 0.4785276 0.4793262 0.4785933
##  [655] 0.4793893 0.4786585 0.4794521 0.4802432 0.4810319 0.4818182
##  [661] 0.4826021 0.4818731 0.4811463 0.4819277 0.4812030 0.4804805
##  [667] 0.4812594 0.4820359 0.4813154 0.4805970 0.4798808 0.4806548
##  [673] 0.4799406 0.4807122 0.4814815 0.4807692 0.4815362 0.4823009
##  [679] 0.4815906 0.4823529 0.4831131 0.4824047 0.4816984 0.4809942
##  [685] 0.4817518 0.4810496 0.4818049 0.4811047 0.4818578 0.4826087
##  [691] 0.4819103 0.4812139 0.4805195 0.4798271 0.4791367 0.4798851
##  [697] 0.4791966 0.4799427 0.4806867 0.4814286 0.4821683 0.4829060
##  [703] 0.4836415 0.4829545 0.4836879 0.4830028 0.4823197 0.4830508
##  [709] 0.4837800 0.4830986 0.4838256 0.4831461 0.4838710 0.4831933
##  [715] 0.4825175 0.4818436 0.4825662 0.4818942 0.4812239 0.4805556
##  [721] 0.4812760 0.4806094 0.4799447 0.4806630 0.4813793 0.4807163
##  [727] 0.4800550 0.4793956 0.4787380 0.4780822 0.4787962 0.4781421
##  [733] 0.4774898 0.4782016 0.4789116 0.4782609 0.4789688 0.4783198
##  [739] 0.4776725 0.4770270 0.4777328 0.4770889 0.4764468 0.4758065
##  [745] 0.4751678 0.4745308 0.4738956 0.4745989 0.4753004 0.4760000
##  [751] 0.4766977 0.4773936 0.4767596 0.4761273 0.4768212 0.4761905
##  [757] 0.4768824 0.4775726 0.4769433 0.4776316 0.4770039 0.4763780
##  [763] 0.4757536 0.4751309 0.4758170 0.4765013 0.4771838 0.4778646
##  [769] 0.4785436 0.4779221 0.4785992 0.4792746 0.4786546 0.4793282
##  [775] 0.4787097 0.4780928 0.4787645 0.4781491 0.4788190 0.4782051
##  [781] 0.4775928 0.4782609 0.4789272 0.4783163 0.4777070 0.4770992
##  [787] 0.4777637 0.4771574 0.4765526 0.4759494 0.4753477 0.4747475
##  [793] 0.4754098 0.4760705 0.4754717 0.4748744 0.4742785 0.4749373
##  [799] 0.4755945 0.4750000 0.4744070 0.4750623 0.4757161 0.4751244
##  [805] 0.4745342 0.4739454 0.4733581 0.4740099 0.4734240 0.4740741
##  [811] 0.4734895 0.4741379 0.4735547 0.4729730 0.4736196 0.4730392
##  [817] 0.4724602 0.4731051 0.4737485 0.4731707 0.4738124 0.4732360
##  [823] 0.4738761 0.4745146 0.4739394 0.4745763 0.4740024 0.4746377
##  [829] 0.4752714 0.4759036 0.4753309 0.4747596 0.4753902 0.4748201
##  [835] 0.4742515 0.4736842 0.4743130 0.4749403 0.4755662 0.4761905
##  [841] 0.4768133 0.4762470 0.4756821 0.4763033 0.4757396 0.4763593
##  [847] 0.4757969 0.4764151 0.4758539 0.4752941 0.4759107 0.4765258
##  [853] 0.4759672 0.4765808 0.4760234 0.4766355 0.4760793 0.4766900
##  [859] 0.4761350 0.4755814 0.4761905 0.4756381 0.4750869 0.4745370
##  [865] 0.4739884 0.4734411 0.4740484 0.4746544 0.4741082 0.4735632
##  [871] 0.4741676 0.4736239 0.4730813 0.4725400 0.4731429 0.4737443
##  [877] 0.4732041 0.4726651 0.4732651 0.4727273 0.4733258 0.4727891
##  [883] 0.4733862 0.4728507 0.4723164 0.4729120 0.4735062 0.4740991
##  [889] 0.4746907 0.4741573 0.4747475 0.4753363 0.4748040 0.4753915
##  [895] 0.4748603 0.4754464 0.4749164 0.4743875 0.4749722 0.4755556
##  [901] 0.4750277 0.4756098 0.4750831 0.4745575 0.4740331 0.4746137
##  [907] 0.4740904 0.4746696 0.4752475 0.4758242 0.4763996 0.4769737
##  [913] 0.4764513 0.4770241 0.4775956 0.4781659 0.4776445 0.4771242
##  [919] 0.4766050 0.4771739 0.4766558 0.4772234 0.4767064 0.4772727
##  [925] 0.4778378 0.4773218 0.4768069 0.4773707 0.4768568 0.4763441
##  [931] 0.4769066 0.4774678 0.4780279 0.4785867 0.4780749 0.4775641
##  [937] 0.4781217 0.4786780 0.4781683 0.4787234 0.4782147 0.4787686
##  [943] 0.4782609 0.4777542 0.4772487 0.4767442 0.4772967 0.4767932
##  [949] 0.4773446 0.4768421 0.4773922 0.4768908 0.4763903 0.4758910
##  [955] 0.4753927 0.4748954 0.4754441 0.4749478 0.4754953 0.4750000
##  [961] 0.4745057 0.4750520 0.4755971 0.4761411 0.4756477 0.4761905
##  [967] 0.4756980 0.4752066 0.4757482 0.4752577 0.4747683 0.4753086
##  [973] 0.4758479 0.4763860 0.4758974 0.4754098 0.4759468 0.4754601
##  [979] 0.4759959 0.4765306 0.4770642 0.4765784 0.4771109 0.4776423
##  [985] 0.4781726 0.4787018 0.4792300 0.4797571 0.4792720 0.4787879
##  [991] 0.4783047 0.4788306 0.4783484 0.4778672 0.4783920 0.4779116
##  [997] 0.4774323 0.4769539 0.4764765 0.4760000
```


```r
data("father.son")
x<- father.son$sheight
(mean(x)+c(-1,1)*qnorm(0.975)*sd(x)/sqrt(length(x)))/12
```

```
## [1] 5.709670 5.737674
```

```r
round(1/sqrt(10^(1:6)),3)
```

```
## [1] 0.316 0.100 0.032 0.010 0.003 0.001
```

```r
binom.test(56, 100)$conf.int
```

```
## [1] 0.4571875 0.6591640
## attr(,"conf.level")
## [1] 0.95
```

```r
n<- 20
pvals<- seq(0.1, 0.9, by=0.05)
nosim<- 1000
coverage<- sapply(pvals, function(p){
        phats<- rbinom(nosim, prob=p, size=n)/n
        ll<- phats - qnorm(0.975) * sqrt(phats * (1-phats)/n)
        ul<- phats + qnorm(0.975) * sqrt(phats *(1-phats)/n)
        mean(ll<p&ul>p)
})
ggplot(data=data.frame(cbind(pvals=pvals, coverage=coverage)), mapping=aes(x=pvals, y=coverage)) + geom_line() + theme_bw() + geom_hline(yintercept=0.95, color="red")+ylim(0,1)
```

![](lecture.2_files/figure-html/confidence intervals-1.png) 

```r
n<- 100
pvals<- seq(0.1, 0.9, by=0.05)
nosim<- 1000
coverage<- sapply(pvals, function(p){
        phats<- rbinom(nosim, prob=p, size=n)/n
        ll<- phats - qnorm(0.975) * sqrt(phats * (1-phats)/n)
        ul<- phats + qnorm(0.975) * sqrt(phats *(1-phats)/n)
        mean(ll<p&ul>p)
})
ggplot(data=data.frame(cbind(pvals=pvals, coverage=coverage)), mapping=aes(x=pvals, y=coverage)) + geom_line() + theme_bw() + geom_hline(yintercept=0.95, color="red")+ylim(0,1)
```

![](lecture.2_files/figure-html/confidence intervals-2.png) 

```r
n<- 20
pvals<- seq(0.1, 0.9, by=0.05)
nosim<- 1000
coverage<- sapply(pvals, function(p){
        phats<- (rbinom(nosim, prob=p, size=n)+2)/(n+4)
        ll<- phats - qnorm(0.975) * sqrt(phats * (1-phats)/n)
        ul<- phats + qnorm(0.975) * sqrt(phats *(1-phats)/n)
        mean(ll<p&ul>p)
})
ggplot(data=data.frame(cbind(pvals=pvals, coverage=coverage)), mapping=aes(x=pvals, y=coverage)) + geom_line() + theme_bw() + geom_hline(yintercept=0.95, color="red")+ylim(0,1)
```

![](lecture.2_files/figure-html/confidence intervals-3.png) 


```r
x<- 5
t<- 94.32
lambda<- x/t
round(lambda+c(-1,1) * qnorm(0.975) * sqrt(lambda/t),3)
```

```
## [1] 0.007 0.099
```

```r
poisson.test(x, T = 94.32)$conf
```

```
## [1] 0.01721254 0.12371005
## attr(,"conf.level")
## [1] 0.95
```
#Full notes
<embed src="lecture.2.pdf" width="900" height="500" type='application/pdf'/>