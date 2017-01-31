# Observations

`Rich::Rec::GlobalPID::LikelihoodTool::deltaLogLikelihood(LHCb::RichRecTrack*,Rich::ParticleIDType)`
w/ cycle detection
short: LikelihoodTool

## Standard setup

### callgrind (original.out)

| function                                       |     CEst       |  % of `executeRun` |
| ---------------------------------------------- | --------------:| ------------------:|
| `main`                                         | 7723736757226  |       n/a          |
| `virtual ApplicationMgr::executeRun(int)`      | 6034605155174  |      100.000 %     |
|   (seen from main)                             |                |                    |
| `Rich::Rec::initialise::execute()` ????        |  569902547685  |                    |
| `Rich::Rec::GlobalPID::Likelihood::execute()`  |                |                    |
| LikelihoodTool                                 |  131526970650  |        2.180 %     |
| PhotonRecoUsingQuarticSoln                     |  191245047125  |        3.169 %     |
| `MuonIDAlgLite::execute`                       |    5005206732  |                    |
| `CombineParticles::execute()`                  |   78177166723  |        1.295 %     |
| `virtual Run2GhostId::execute(LHCb::Track&)`   |   10048600073  |        0.167 %     |
|   - from `TrackBestTrackCreator::fit(Track&)`  |    5473765064  |        0.091 %     |
|   - from `HltTrackFilterGhostProb::tracks…`    |    4574835009  |        0.076 %     |

| tanh from ANNPID                               |    3394072907

### Rate report

processed: 30000 events
rates assume 1000000.0 Hz from level-0
|---|`Hlt1Global`                                    |142.93+-2.02   |--             |
|---|`Hlt2Global`                                    |12.60+-0.64    |--             |
|---|`Hlt2.*Turbo`                                   |4.87+-0.40     |--             |
|---|`Hlt2.*Full`                                    |8.93+-0.54     |--             |
|---|`Hlt2.*Turcal`                                  |0.37+-0.11     |--             |


### Running

Hlt2 runs RICH over 4288 evts
made PID for 173750 tracks
Hlt2Topo2BodyTosCombiner
attempts 205260 combinations
fits 19116
accepts 8411
in 2139/3896

| it does                         |  so many times   | difference wrt original  |
| ------------------------------- | ----------------:| ------------------------:|
| Hlt2 runs RICH                  |    4288 evts     |       ±  0.000 %         |
| RICH (and others)  made PID for |   173750 tracks  |       ±  0.000 %         |
| Hlt2Topo2BodyTosCombiner        |                  |                          |
|  - attempts                     |  205260 combs    |       ±  0.000 %         |
|  - fits                         |   19116 combs    |       ±  0.000 %         |
|  - accepts                      |   78411 combs    |       ±  0.000 %         |
|  - in                           |   2139/3896 evts |                          |

## GP cut released to > 1.0

### callgrind (hack.out)

| function                                       |     CEst       |  % of `executeRun` |
| ---------------------------------------------- | --------------:| ------------------:|
| `main`                                         | 9008328919384  |       n/a          |
|   - excl. GP                                   |                |                    |
| `executeRun(int)`                              | 7186530848757  |                    |
|   (seen from main)                             |                |                    |
|   - excl. GP                                   | 7176631143805  |      100.000 %     |
| `Rich::Rec::initialise::execute()` ????        |  744462669589  |                    |
| `Rich::Rec::GlobalPID::Likelihood::execute()`  |                |                    |
| LikelihoodTool                                 |  306177678511  |        4.266 %     |
| PhotonRecoUsingQuarticSoln                     |  256604311245  |        3.576 %     |
| `MuonIDAlgLite::execute`                       |    7590668704  |                    |
| `CombineParticles::execute()`                  |  187645739148  |        2.611 %     |
| `virtual Run2GhostId::execute(LHCb::Track&)`   |    9899704952  |                    |
|   - from `TrackBestTrackCreator::fit(Track&)`  |    5372318714  |                    |
|   - from `HltTrackFilterGhostProb::tracks…`    |    4527386238  |                    |

### Rate report

processed: 30000 events
rates assume 1000000.0 Hz from level-0
|---|`Hlt1Global`                                    |148.33+-2.05   |--             |
|---|`Hlt2Global`                                    |17.17+-0.75    |--             |
|---|`Hlt2.*Turbo`                                   |7.77+-0.51     |--             |
|---|`Hlt2.*Full`                                    |11.30+-0.61    |--             |
|---|`Hlt2.*Turcal`                                  |0.33+-0.11     |--             |

### Running

| it does                         |  so many times   | difference wrt original  |
| ------------------------------- | ----------------:| ------------------------:|
| Hlt2 runs RICH                  |    4450 evts     |       +  3.780 %         |
| RICH (and others)  made PID for |   223340 tracks  |       + 28.541 %         |
| Hlt2Topo2BodyTosCombiner        |                  |                          |
|  - attempts                     |  619509 combs    |       +218.167 %         |
|  - fits                         |   41452 combs    |       +116.844 %         |
|  - accepts                      |   18007 combs    |       +114.089 %         |
|  - in                           |   2531/4061 evts |                          |



### Δ
