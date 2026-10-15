<h1 align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Chakra+Petch&weight=600&size=55&duration=1&pause=1000&color=FFFFFF&background=000435&center=true&vCenter=true&repeat=false&width=1200&lines=OrbitOps%3A+Evidence-Grounded+AIOps+Copilot" alt="OrbitOps: Evidence-Grounded AIOps Copilot with Non-Bypassable Assurance Gates" />
</h1>

<p align="center">
  <b>Satellite Operations Copilot with Non-Bypassable Assurance Gates</b> <br>
  <i>an intelligent incident investigation system for satellite operations, combining real spacecraft telemetry, anomaly detection, hybrid rag, and an agentic investigation workflow.</i>
</p>


----
#### the actual use case
the key capability is connecting three different kinds of information:

$$
\underbrace{\text{telemetry}}_{\text{what happened}} + \underbrace{\text{historical incidents}}_{\text{what happened before}} + \underbrace{\text{technical documentation}}_{\text{what is known}}
$$

![Authority taxonomy for LLM-based operational agents](public/assets/taxonomy.png)
*figure 1: we focus on read-oriented & tool-grounded diagnosis [1].*

#### the dataset: using real spacecraft telemetry
<b>esa anomaly dataset</b>. developed through a project involving the european space agency, airbus defence and space, and kp labs. the dataset contains real telemetry from three esa missions, with anomalies annotated through a process involving spacecraft operations engineers and machine learning experts [2]. we will start with a small subset from one mission (esa-mission1) [3].
- `train.parquet` - the training set; 14 years of esa-mission1 data from the esa-ad dataset with annotated anomalous time points (is_anomaly column)
- `test.parquet` - the test set; a never before published 6-months long fragment of esa-mission1 data
- `target_channels.csv` - a list of names of 58 channels monitored for anomalies (other 29 channels are just external auxiliary variables)
- `sample_submission.parquet` - a sample submission file in the correct format - note: this is for competition purposes

#### the central research question
can a retrieval-augmented investigation system improve the completeness and factual grounding of satellite anomaly reports while keeping false alarms, unsupported diagnoses, latency, and computational cost within measurable limits?

#### initial-plan: architecture
the agent can query the numerical analysis system through a tool. we connect structured analytics with rag without asking the llm to perform every computation itself.

| information | processing method |
| --- | --- |
| telemetry measurements | time-series database and numerical analysis |
| anomaly detection | statistical or time-series ml model |
| historical incident descriptions | hybrid information retrieval |
| engineering documentation | hybrid document retrieval |
| incident synthesis | llm with tool access and evidence verification |

#### anomaly detection
fortunately, there is already a research paper that has handled training, research, configuration, and hyperparameter tuning [4].
![alt text](public/assets/anom-detection.png)
we can use the same config; using forecasting & thresholding method; with XceptionTimePlus architecture [5]: based on the XceptionTime architecture [6] from the `tsai` time series analysis framework [7]. to know more about this arch, these prerequisites must be completed first:

- [x]  conventional cnns; 2d/3d: learning features instead of engineering them [8]
- [x]  inception: why choose only one temporal scale? [8]
- [x]  resnet: why do deeper networks need shortcuts? [8]
- [ ]  xception: separating temporal and channel interactions
- [ ]  inceptiontime: bringing inception into time-series classification
- [ ]  xceptiontime: combining inceptiontime with separable convolutions


#### sources
[1] [arXiv:2605.12729](https://arxiv.org/pdf/2605.12729).<br>
[2] [zenodo:12528696](https://zenodo.org/records/12528696) <br>
[3] [kaggle: esa-adb-challenge](https://www.kaggle.com/competitions/esa-adb-challenge/data)<br>
[4] [arxiv: 2603.29375](https://arxiv.org/pdf/2603.29375)<br>
[5] [ieee: 10794845](https://ieeexplore.ieee.org/document/10794845)<br>
[6] [arxiv: 1911.03803](https://arxiv.org/pdf/1911.03803)<br>
[7] [tsai](https://timeseriesai.github.io/tsai/) <br>
[8] [convnets](https://yintelligence.space/posts/convnets/)