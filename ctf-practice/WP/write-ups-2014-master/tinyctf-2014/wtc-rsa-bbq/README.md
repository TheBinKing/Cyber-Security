# tinyCTF 2014: WTC RSA BBQ

**Category:** Crypto
**Points:** 200
**Description:**

> [Download file](cry200.zip)

## Write-up

Let’s extract [the provided `cry200.zip` file](cry200.zip):

```bash
$ unzip cry200.zip
Archive:  cry200.zip
  inflating: cry200
```

The extracted `cry200` file is another ZIP file:

```bash
$ file cry200
cry200: Zip archive data, at least v2.0 to extract
```

So let’s extract it as well:

```bash
$ unzip cry200
Archive:  cry200
  inflating: cipher.bin
  inflating: key.pem
```

This is an RSA task, so let’s try to break the public key first. The task title contains a big hint: WTC refers to the Twin Towers, which is a hint at [twin primes](https://en.wikipedia.org/wiki/Twin_prime).

Let’s extract the modulus and exponent from the public key first.

```bash
$ openssl rsa -in key.pem -pubin -text -noout
Public-Key: (8587 bit)
Modulus:
    06:2d:3d:61:c9:24:52:63:01:47:e8:96:70:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff
Exponent: 65537 (0x10001)
```

This already looks very fishy. Those `\xff` bytes show that the modulus is very close to a power of 2, multiplied by some number. Factoring this number would be impossible if we started from the beginning, but we can find the square root of the number and start from there. The following script does just that:

```python
def isqrt(n):
  x = n
  y = (x + n // x) // 2
  while y < x:
    x = y
    y = (x + n // x) // 2
  return x

n = 67957992944541709079637331495835288051017736172946219268979124310219676901814634141994056910249665182493729973853745613557654443204907939100289830019879722192443748372464385547701814777428863933615522890059773474417386931884425569247554583568455670977507333610910984675277207738543785144821532814109666026143830882670492412501367418900259525020329476259602896533289977520877332000639367622359213599508853567838502735818733930199768810238363613613753812700686852922490193705926713608040249887743216661319134457665231243871456616938275370046526015614319970725259025037328092187037543179610573655207460380491069632574369131778109901652462838149658009709174356861767870204803806924289315954871595222073859185353284268587331267173728221658781990119401252167899826047588583247362298572788397512447184590473718761927222549389515152849248566281272354480116085470203137413924993107429630882329043259530840382880179158766903387472716587067982240678129096467201138461960380680792953534366991098348930562736587887507018304132204828793333486018470656056870548645765390879310100168147762901154890481163444481122296433539288905754638768700952492512406731460604412447424967642115057341729310735982961515248311488333222612609961196477124084039771246638999119951171033639602489932159455170406551791127198312487436473494597495007637073871513066738388720194946877125132719068351961085662002556667562192631487439603084021927891681500086528284664252971146275389474911554158614058033716200975019522317823518017673425098559715637356338155079086810436188632405309750833509905138561418180066417475648209078560221064551872389391920606516486209161430247427717376721027499023891011742164463421915449354247944433039198608877315066424065203739793333831943021283319660097829517280179002430376294322395829290502762707146363340431306946572116838111246133390539315819023086956548363452657425340012155573512351731935196011505710069798425307656340650313899667019621505845424588367900827398564048322933092059258373872118350187669748998950161402077367239291462315563970921983573721268515566367155707585109243757143789901450148994239501684623655163637997105769222959494325064113278738038394139099703042640054592379346782002980751786063951491138135071807202634411442713870047730189971333170418112077390015852729766594918955255488280027359348811304774349052504612270369695008061623968574970758347117606577939555446238067430685787886502742201372798852010893885999941946548336103402517187248492765699490151394806591149028320530966365733320484047650429644420042692902092613911608152310152409036167526533619822851411589502970363903
e = 65537

i = isqrt(n)

p, q = 0, 0

while True:
  if n - (i * (n / i)) == 0:
    p = i
    q = n/i
    break
  i += 1

print p
print q
```

This gives us `p` and `q`, which are indeed twin primes. All we have to do now is to decrypt `cipher.bin`.
We can achieve this with the following script:

```python
n = 67957992944541709079637331495835288051017736172946219268979124310219676901814634141994056910249665182493729973853745613557654443204907939100289830019879722192443748372464385547701814777428863933615522890059773474417386931884425569247554583568455670977507333610910984675277207738543785144821532814109666026143830882670492412501367418900259525020329476259602896533289977520877332000639367622359213599508853567838502735818733930199768810238363613613753812700686852922490193705926713608040249887743216661319134457665231243871456616938275370046526015614319970725259025037328092187037543179610573655207460380491069632574369131778109901652462838149658009709174356861767870204803806924289315954871595222073859185353284268587331267173728221658781990119401252167899826047588583247362298572788397512447184590473718761927222549389515152849248566281272354480116085470203137413924993107429630882329043259530840382880179158766903387472716587067982240678129096467201138461960380680792953534366991098348930562736587887507018304132204828793333486018470656056870548645765390879310100168147762901154890481163444481122296433539288905754638768700952492512406731460604412447424967642115057341729310735982961515248311488333222612609961196477124084039771246638999119951171033639602489932159455170406551791127198312487436473494597495007637073871513066738388720194946877125132719068351961085662002556667562192631487439603084021927891681500086528284664252971146275389474911554158614058033716200975019522317823518017673425098559715637356338155079086810436188632405309750833509905138561418180066417475648209078560221064551872389391920606516486209161430247427717376721027499023891011742164463421915449354247944433039198608877315066424065203739793333831943021283319660097829517280179002430376294322395829290502762707146363340431306946572116838111246133390539315819023086956548363452657425340012155573512351731935196011505710069798425307656340650313899667019621505845424588367900827398564048322933092059258373872118350187669748998950161402077367239291462315563970921983573721268515566367155707585109243757143789901450148994239501684623655163637997105769222959494325064113278738038394139099703042640054592379346782002980751786063951491138135071807202634411442713870047730189971333170418112077390015852729766594918955255488280027359348811304774349052504612270369695008061623968574970758347117606577939555446238067430685787886502742201372798852010893885999941946548336103402517187248492765699490151394806591149028320530966365733320484047650429644420042692902092613911608152310152409036167526533619822851411589502970363903
p = 260687538913047604611581784183499992008451760653785074016920718323190075912750802620741024634382067897986936407072164858654195035172056629230527593989978466296098220579031027154724041642557344915423242566240332284307941704981938020407661739104882149483433969072174052675580644164713319546908058746795753762649896919296312912702039493797237183118384499796757914157936629672274357161577311007769338358918777509136488505959298049498018461823273893799669038335872602861372239911549680531979970541528181711754520442958622706059603000655429088872469604344301647170492716926975027102329909258120989355802343558462047316328752521306824960655230501606894696454547299868668551619819367530969111390441903346427083466873717778205853984905381790237396069409514016317067322105019049986366714245693681256834514176535381210683575566036929609986694319036120560201862975426434985372574748540556000702736560930190396248279747095930579691977036607335841985416541503515963817848780705827093841092321324825882821075072622553561916744473353548759606182352622008019859330726239330083782855413787656845382479896229326659871568516059343215385393836820040891163826148343904385963328442668250413125432533185139042633099387310968853063208000057718438859818276275817262048678368751842523947169311954597690408896814857060351
q = 260687538913047604611581784183499992008451760653785074016920718323190075912750802620741024634382067897986936407072164858654195035172056629230527593989978466296098220579031027154724041642557344915423242566240332284307941704981938020407661739104882149483433969072174052675580644164713319546908058746795753762649896919296312912702039493797237183118384499796757914157936629672274357161577311007769338358918777509136488505959298049498018461823273893799669038335872602861372239911549680531979970541528181711754520442958622706059603000655429088872469604344301647170492716926975027102329909258120989355802343558462047316328752521306824960655230501606894696454547299868668551619819367530969111390441903346427083466873717778205853984905381790237396069409514016317067322105019049986366714245693681256834514176535381210683575566036929609986694319036120560201862975426434985372574748540556000702736560930190396248279747095930579691977036607335841985416541503515963817848780705827093841092321324825882821075072622553561916744473353548759606182352622008019859330726239330083782855413787656845382479896229326659871568516059343215385393836820040891163826148343904385963328442668250413125432533185139042633099387310968853063208000057718438859818276275817262048678368751842523947169311954597690408896814857060353
e = 65537

def egcd(a, b):
  if a == 0:
    return (b, 0, 1)
  else:
    g, y, x = egcd(b % a, a)
    return (g, x - (b // a) * y, y)

def modinv(a, m):
  g, x, y = egcd(a, m)
  if g != 1:
    raise Exception('modular inverse does not exist')
  else:
    return x % m

cipher = open('cipher.bin', 'rb').read().encode('hex')
cipher = int(cipher, 16)

fi = (p-1)*(q-1)
d = modinv(e, fi)

flag = pow(cipher, d, n)
print ('%x' % flag).decode('hex')
```

After executing this, we get the flag in the output:

```
Congratulations! Here is a treat for you: flag{how_d0_you_7urn_this_0n?}
```

## Other write-ups and resources

* <https://github.com/jesstess/tinyctf/blob/master/rsa/rsa.md>