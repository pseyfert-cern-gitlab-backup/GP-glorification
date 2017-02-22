# GP-glorification

A project with profiling tests which are meant to do shamelessly glorify the
importance and achievements of the ghost probability. No dignity, modesty,
realism, or attempt to give an unbiassed picture of reality shall be assumed.

![LICENSE LOGO](http://www.wtfpl.net/wp-content/uploads/2012/12/wtfpl-badge-2.png)

# LOGO

The logo is merged from a
[crown](https://pixabay.com/en/crown-golden-yellow-emperor-576226/) (CC0) and a
[ghost](http://www.freestockphotos.biz/stockphoto/12084) (public domain).


# setup

```shell
/afs/cern.ch/lhcb/software/releases/LBSCRIPTS/LBSCRIPTS_v8r6p9/InstallArea/scripts/lb-dev Moore v25r3
cd ./MooreDev_v25r3
git lb-use Rec
git lb-checkout Rec/v19r3p1 Tr/TrackUtils
git lb-use Hlt
git lb-checkout Hlt/v25r1 Hlt/HltTracking
getpack PRConfig v1r25
cp $GPGLORIFICATION/0001-hacks.patch ./
git apply 0001-hacks.patch
cd PRConfig/python
patch -p0 -i $GPGLORIFICATION/svn-patch
```

then either ignore the build and do
```
lb-run Moore/v25r3 $SHELL $RANDOMOPTION
cd MooreDev_v25r3/PRConfig/python/MooreTests
gaudirun.py --profilerName=valgrindcallgrind --profilerExtraOptions="__smc-check=all-non-file  __dump-instr=yes __trace-jump=yes __callgrind-out-file=original.out" Moore_RateTest_options3.py
```

or build everything and

```
cd MooreDev_v25r3
./run  $SHELL $RANDOMOPTION
cd PRConfig/python/MooreTests
gaudirun.py --profilerName=valgrindcallgrind --profilerExtraOptions="__smc-check=all-non-file  __dump-instr=yes __trace-jump=yes __callgrind-out-file=original.out" Moore_RateTest_options3.py
```
