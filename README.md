# Data Poisoning with Dynamic Backdoor Attacks
this project was done by Hugo Centeno and Lauren Gallego
## Abstract 
In this research project a series of backdoor attacks under numerous conditions were implemented to compare its results. 
We have experimented with the following: 
* Datasets: MNIST & CIFAR-10 
* Models: ResNet18 & custom CNN 
* Attack algorithms: Random Backdoor & BaN 
* Attack type: single/multiple target label
## Introduction
Backdoor attacks are becoming increasingly relevant in the context of machine learning (ML) 
and AI systems.
At the moment, there are no effective defense mechanisms to counter 
these  white-box attacks, as attackers can modify both the data and the model.

By recreating the attacks under different conditions, we have been able to observe their effectiveness 
under different circumstances. We have successfully shown how attackers can shape the model’s 
behaviour to their best interests.  

In our case, we have performed these attacks in two of the most widely used datasets in the 
context of ML: MNIST and CIFAR-10. Our experiments can serve as 
evidence of how subtle modifications can lead to a perfectly confident poisoned model. 
These results can be extrapolated to more sensitive datasets.
## Procedure
We first trained 4 clean benchmark models combining two architectures (ResNet18 and our 
custom CNN) and two datasets (MNIST and CIFAR-10).

This was done with the objective of setting clean accuracy goals, to know if our poisoned models could go undetected when tested against clean data. 
After that we began training and tuning our poisoned models under the same conditions as the 
benchmark models and compared the results obtained. 

When it comes to the defense, we implemented both model-based defense and data-based 
defenses. 

We worked on Neural Cleanse to defend our best performing models both in BaN and Random 
Backdoor. We aimed to compare the robustness of this defense against both of these dynamic 
backdoor attack algorithms.
## Example of how were multiple labels poisoned on CIFAR-10
The image was equally divided into 10 regions, and the trigger was randomly placed in one of those regions.
![CIFAR-10T rigger Regions](imgs/CIFAR-10TriggerRegions.png)

50% of the dataset was attacked, and this new poissoned version was used as training dataset for the possioned model.
![Random Sample Attacked Instances](imgs/RandomSampleAttackedInstances.png)

## Results obtained for ResNet18 model
| DATASET   | ATTACK    | BENCHMARK ACCURACY | CLEAN ACCURACY | ATTACK SUCCESS RATE |
| ------    | -----     | -------| ------ | ------ | 
| MNIST | Random Backdoor | 99.14% | 98.81% | 98.52% |
| CIFAR-10 | Random Backdoor | 84.1% | 82.48% | 97.63% |
| MNIST | BaN | 99.14% | 98.53% | 94.2% |
| CIFAR-10 | BaN | 84.1% | 83.7% | 99.97% |

## Defenses
We tested two types of defenses: Neural Cleanse and STRIP.

Neural Cleanse was tested against a poisoned model trained for CIFAR-10 with a single label attach. The attacked lable was 0, and this was correctly
detected by our defense as we got the following anomaly socres and result. Therefore, we can consider our defense to have been successful.
<table>
  <tr>
    <th>Class</th>
    <td>0</td>
    <td>1</td>
    <td>2</td>
    <td>3</td>
    <td>4</td>
    <td>5</td>
    <td>6</td>
    <td>7</td>
    <td>8</td>
    <td>9</td>
  </tr>
  <tr>
    <th>Score</th>
    <td>3.79</td>
    <td>0.62</td>
    <td>1.95</td>
    <td>0.11</td>
    <td>2.00</td>
    <td>3.29</td>
    <td>0.32</td>
    <td>0.11</td>
    <td>1.29</td>
    <td>0.71</td>
  </tr>
</table>

STRIP is a defense on the data method. We tested it to detect anomalies in an attacked CIFAR-10 dataset. The results obtained show how Random Backdoor Attacks are difficult to defend, as
they are a white-box type attack. If our defense had been successful, attacked images should present lower entropy values than clean images.
![STRIP defense results](imgs/STRIPDefense.png)
