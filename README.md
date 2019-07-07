# Metamorphic Testing for Validation of ML/DL Models 
## The problem
Find the suitable ways to solve the test Oracle problem [1] in AI/ML/DL
software (in a simple way find an approach to an end to end functional testing
for AI which considered as a non-testable system).
## Introduction
### The Test Oracle
In software testing, Test oracle is a mechanism that can tell you whether a
program is working correctly or not. For the simplest case, an oracle could be a
direct comparison of the output of the program with the correct answer.

Test oracle can provides a mean to (1) Generate expected results for test inputs
(2) Compare the expected and actual results of execution of the implementation
under test (IUT) [2].

Test oracle has different types Perfect Oracle, Gold standard Oracle, Parametric
Oracle, Statistical Oracle, etc… the most common is the statistical Oracle (a
type of parametric oracle).

![alt text](media/2f6ba4e32ba35027660e28d6d4096b47.jpg)

### The ML System Under Test

Testing machine learning and AI algorithms is hard [3] as scientific software
differs significantly from the development of more traditional business
information systems, these differences appear throughout the following stages of
the software lifecycle: requirement, design, coding, validation and
verification, and deployment.

Moreover, the problem is that often there is no oracle without human
intervention, e.g., image recognition solved by supervised ML. This usually
begins by curating a dataset of correctly labelled image for training and
validating, which is itself a way of introducing an oracle for the software
model in development by human intervention. This implies that the range of test
conducted to the model will be limited by human efforts, and expanding the test
cases, for example increasing the sampling size and varieties significantly with
online testing, would be a problem.

The key component of an autonomous vehicle is the perception module controlled by the underlying Deep Neural Network (DNN), the network takes input from different sensors like camera, light detection and ranging sensor (LiDAR), and IR (infrared) sensor that measure the environment and outputs the steering angle, braking, etc. necessary to maneuver the car safely under different
conditions.

![](media/42528cabfe25de76fa6d8613385fca35.jpg)

![](media/c8f4230e9912aa57a1cc052536b8b622.jpg)

The main idea is to develop an automated testing methodology for driven autonomous cars
-   How do we systematically explore the input-output spaces of an autonomous
    car DNN?
-   How can we synthesize realistic inputs to automate such exploration?
-   How can we optimize the exploration process?
-   How do we automatically create a test oracle that can detect erroneous
    behaviors without detailed manual specifications?



### Metamorphic Testing
A software testing technique that can effectively address two fundamental problems in software testing: the **oracle problem** and **automated test case generation problem**. The main difference between MT and regular testing techniques is that MT does not focus on the verification of each componant of  the software under test (and therefore can be performed in the absence of an oracle). MT checks the relations among the inputs and outputs of multiple executions of the software. Such relations are called metamorphic relations (MRs) [6].

## MT In Action 

### Systematic Testing with Neuron Coverage (The Testing Technique)

The combination of all possible inputs and outputs for autonomous car
exploratory analysis is very large so there must be a way for partitioning the
space into different equivalence classes and choosing the right equivalent
representatives is done by *neuron coverage (for measuring how many rules in a
DNN are exercised by a set of inputs), this way is dependent on the s*

*Neuron Coverage = Number of activated Neurons/Total number of Neurons*

### Image Augmentations (Automated Test Case Generation)

Arbitrary inputs that maximize neuron coverage is inefficient way in deep
learning models, in stead generating realistic synthetic images by applying
image transformations on seed images and mimicking different real-world
phenomena like camera lens distortions, object movements, different weather
conditions (rain, fog, etc…) is a more efficient way for increasing test
coverage. The image generation is done by a greedy search algorithm in [8].

### Creating a Test Oracle with Metamorphic Relations

Here is where metamorphic relations [4] between the car behaviors across
different synthetic images come to play a role. The key insight is that even
though it is hard to specify the correct behavior of a self-driving car for
every transformed image, one can define relationships between the car’s
behaviors across certain types of transformations. For example, the autonomous
car’s steering angle should not change significantly for the same image under
any lighting/weather conditions, blurring, or any affine transformations with
small parameter values.

### Violations (bugs) --- chauffeur model  

| original|contrast(2.0)| original|contrast(2.0)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572510052897_arrow.jpg" width="300"> | <img src="./media/1479425572510052897_contrast_2.0_arrow.jpg" width="300">  | <img src="./media/1479425572360010147_arrow.jpg" width="300"> | <img src="./media/1479425572360010147_contrast_2.0_arrow.jpg" width="300"> |


| original|contrast(2.0)| original|contrast(2.0)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572411157865_arrow.jpg" width="300"> | <img src="./media/1479425572411157865_contrast_2.0_arrow.jpg" width="300">  | <img src="./media/1479425572560301984_arrow.jpg" width="300"> | <img src="./media/1479425572560301984_contrast_2.0_arrow.jpg" width="300"> |


| original|contrast(2.0)| original|contrast(2.0)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572460127373_arrow.jpg" width="300"> | <img src="./media/1479425572460127373_contrast_2.0_arrow.jpg" width="300">  | <img src="./media/1479425572610024407_arrow.jpg" width="300"> | <img src="./media/1479425572610024407_contrast_2.0_arrow.jpg" width="300"> |


| original|contrast(2.0)| original|contrast(2.0)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572310124728_arrow.jpg" width="300"> | <img src="./media/1479425572310124728_contrast_2.0_arrow.jpg" width="300">  | <img src="./media/1479425572660350537_arrow.jpg" width="300"> | <img src="./media/1479425572660350537_contrast_2.0_arrow.jpg" width="300"> |


| original|contrast(2.0)| original|contrast(2.0)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572260066549_arrow.jpg" width="300"> | <img src="./media/1479425572260066549_contrast_2.0_arrow.jpg" width="300">  | <img src="./media/1479425572710226941_arrow.jpg" width="300"> | <img src="./media/1479425572710226941_contrast_2.0_arrow.jpg" width="300"> |


| original|contrast(2.0)| original|contrast(2.0)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572210131608_arrow.jpg" width="300"> | <img src="./media/1479425572210131608_contrast_2.0_arrow.jpg" width="300">  | <img src="./media/1479425572159996266_arrow.jpg" width="300"> | <img src="./media/1479425572159996266_contrast_2.0_arrow.jpg" width="300"> |


| original|contrast(2.0)| original|brightness(100)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572109841130_arrow.jpg" width="300"> | <img src="./media/1479425572109841130_contrast_2.0_arrow.jpg" width="300">  | <img src="./media/1479425578460213280_arrow.jpg" width="300"> | <img src="./media/1479425578460213280_brightness_100_arrow.jpg" width="300"> |


| original|brightness(90)| original|brightness(100)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578460213280_arrow.jpg" width="300"> | <img src="./media/1479425578460213280_brightness_90_arrow.jpg" width="300">  | <img src="./media/1479425578510049930_arrow.jpg" width="300"> | <img src="./media/1479425578510049930_brightness_100_arrow.jpg" width="300"> |


| original|contrast(2.0)| original|brightness(100)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572060558494_arrow.jpg" width="300"> | <img src="./media/1479425572060558494_contrast_2.0_arrow.jpg" width="300">  | <img src="./media/1479425578409926566_arrow.jpg" width="300"> | <img src="./media/1479425578409926566_brightness_100_arrow.jpg" width="300"> |


| original|brightness(90)| original|brightness(100)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578510049930_arrow.jpg" width="300"> | <img src="./media/1479425578510049930_brightness_90_arrow.jpg" width="300">  | <img src="./media/1479425578359907740_arrow.jpg" width="300"> | <img src="./media/1479425578359907740_brightness_100_arrow.jpg" width="300"> |


| original|brightness(90)| original|contrast(2.0)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578409926566_arrow.jpg" width="300"> | <img src="./media/1479425578409926566_brightness_90_arrow.jpg" width="300">  | <img src="./media/1479425572010068938_arrow.jpg" width="300"> | <img src="./media/1479425572010068938_contrast_2.0_arrow.jpg" width="300"> |


| original|brightness(80)| original|brightness(80)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578460213280_arrow.jpg" width="300"> | <img src="./media/1479425578460213280_brightness_80_arrow.jpg" width="300">  | <img src="./media/1479425578510049930_arrow.jpg" width="300"> | <img src="./media/1479425578510049930_brightness_80_arrow.jpg" width="300"> |


| original|brightness(100)| original|contrast(2.0)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578559950992_arrow.jpg" width="300"> | <img src="./media/1479425578559950992_brightness_100_arrow.jpg" width="300">  | <img src="./media/1479425571960500180_arrow.jpg" width="300"> | <img src="./media/1479425571960500180_contrast_2.0_arrow.jpg" width="300"> |


| original|brightness(90)| original|brightness(90)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578359907740_arrow.jpg" width="300"> | <img src="./media/1479425578359907740_brightness_90_arrow.jpg" width="300">  | <img src="./media/1479425578559950992_arrow.jpg" width="300"> | <img src="./media/1479425578559950992_brightness_90_arrow.jpg" width="300"> |


| original|brightness(70)| original|brightness(80)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578460213280_arrow.jpg" width="300"> | <img src="./media/1479425578460213280_brightness_70_arrow.jpg" width="300">  | <img src="./media/1479425578409926566_arrow.jpg" width="300"> | <img src="./media/1479425578409926566_brightness_80_arrow.jpg" width="300"> |


| original|brightness(70)| original|brightness(100)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578510049930_arrow.jpg" width="300"> | <img src="./media/1479425578510049930_brightness_70_arrow.jpg" width="300">  | <img src="./media/1479425578310238583_arrow.jpg" width="300"> | <img src="./media/1479425578310238583_brightness_100_arrow.jpg" width="300"> |


| original|brightness(80)| original|contrast(2.0)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578559950992_arrow.jpg" width="300"> | <img src="./media/1479425578559950992_brightness_80_arrow.jpg" width="300">  | <img src="./media/1479425571910047539_arrow.jpg" width="300"> | <img src="./media/1479425571910047539_contrast_2.0_arrow.jpg" width="300"> |


| original|brightness(60)| original|brightness(70)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578460213280_arrow.jpg" width="300"> | <img src="./media/1479425578460213280_brightness_60_arrow.jpg" width="300">  | <img src="./media/1479425578409926566_arrow.jpg" width="300"> | <img src="./media/1479425578409926566_brightness_70_arrow.jpg" width="300"> |


| original|brightness(70)| original|brightness(80)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578559950992_arrow.jpg" width="300"> | <img src="./media/1479425578559950992_brightness_70_arrow.jpg" width="300">  | <img src="./media/1479425578359907740_arrow.jpg" width="300"> | <img src="./media/1479425578359907740_brightness_80_arrow.jpg" width="300"> |


| original|brightness(90)| original|brightness(60)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578310238583_arrow.jpg" width="300"> | <img src="./media/1479425578310238583_brightness_90_arrow.jpg" width="300">  | <img src="./media/1479425578510049930_arrow.jpg" width="300"> | <img src="./media/1479425578510049930_brightness_60_arrow.jpg" width="300"> |


| original|brightness(100)| original|brightness(100)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578610230854_arrow.jpg" width="300"> | <img src="./media/1479425578610230854_brightness_100_arrow.jpg" width="300">  | <img src="./media/1479425555406668683_arrow.jpg" width="300"> | <img src="./media/1479425555406668683_brightness_100_arrow.jpg" width="300"> |


| original|brightness(100)| original|translation(10)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425555456885076_arrow.jpg" width="300"> | <img src="./media/1479425555456885076_brightness_100_arrow.jpg" width="300">  | <img src="./media/1479425573460229446_arrow.jpg" width="300"> | <img src="./media/1479425573460229446_translation_10_arrow.jpg" width="300"> |


| original|translation(10)| original|brightness(90)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425573410225191_arrow.jpg" width="300"> | <img src="./media/1479425573410225191_translation_10_arrow.jpg" width="300">  | <img src="./media/1479425578610230854_arrow.jpg" width="300"> | <img src="./media/1479425578610230854_brightness_90_arrow.jpg" width="300"> |


| original|brightness(90)| original|brightness(60)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425555406668683_arrow.jpg" width="300"> | <img src="./media/1479425555406668683_brightness_90_arrow.jpg" width="300">  | <img src="./media/1479425578409926566_arrow.jpg" width="300"> | <img src="./media/1479425578409926566_brightness_60_arrow.jpg" width="300"> |


| original|brightness(100)| original|brightness(60)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578260210617_arrow.jpg" width="300"> | <img src="./media/1479425578260210617_brightness_100_arrow.jpg" width="300">  | <img src="./media/1479425578559950992_arrow.jpg" width="300"> | <img src="./media/1479425578559950992_brightness_60_arrow.jpg" width="300"> |


| original|brightness(90)| original|translation(10)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425555456885076_arrow.jpg" width="300"> | <img src="./media/1479425555456885076_brightness_90_arrow.jpg" width="300">  | <img src="./media/1479425573510293691_arrow.jpg" width="300"> | <img src="./media/1479425573510293691_translation_10_arrow.jpg" width="300"> |


| original|brightness(80)| original|contrast(2.0)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578610230854_arrow.jpg" width="300"> | <img src="./media/1479425578610230854_brightness_80_arrow.jpg" width="300">  | <img src="./media/1479425571860004228_arrow.jpg" width="300"> | <img src="./media/1479425571860004228_contrast_2.0_arrow.jpg" width="300"> |


| original|contrast(1.8)| original|brightness(100)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425574160328983_arrow.jpg" width="300"> | <img src="./media/1479425574160328983_contrast_1.8_arrow.jpg" width="300">  | <img src="./media/1479425555506801465_arrow.jpg" width="300"> | <img src="./media/1479425555506801465_brightness_100_arrow.jpg" width="300"> |


| original|translation(10)| original|contrast(1.8)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425573360290341_arrow.jpg" width="300"> | <img src="./media/1479425573360290341_translation_10_arrow.jpg" width="300">  | <img src="./media/1479425574210325091_arrow.jpg" width="300"> | <img src="./media/1479425574210325091_contrast_1.8_arrow.jpg" width="300"> |


| original|brightness(70)| original|brightness(80)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578359907740_arrow.jpg" width="300"> | <img src="./media/1479425578359907740_brightness_70_arrow.jpg" width="300">  | <img src="./media/1479425578310238583_arrow.jpg" width="300"> | <img src="./media/1479425578310238583_brightness_80_arrow.jpg" width="300"> |


| original|brightness(90)| original|brightness(70)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578260210617_arrow.jpg" width="300"> | <img src="./media/1479425578260210617_brightness_90_arrow.jpg" width="300">  | <img src="./media/1479425578610230854_arrow.jpg" width="300"> | <img src="./media/1479425578610230854_brightness_70_arrow.jpg" width="300"> |


| original|brightness(50)| original|brightness(80)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578460213280_arrow.jpg" width="300"> | <img src="./media/1479425578460213280_brightness_50_arrow.jpg" width="300">  | <img src="./media/1479425572360010147_arrow.jpg" width="300"> | <img src="./media/1479425572360010147_brightness_80_arrow.jpg" width="300"> |


| original|brightness(80)| original|brightness(70)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572310124728_arrow.jpg" width="300"> | <img src="./media/1479425572310124728_brightness_80_arrow.jpg" width="300">  | <img src="./media/1479425572360010147_arrow.jpg" width="300"> | <img src="./media/1479425572360010147_brightness_70_arrow.jpg" width="300"> |


| original|brightness(90)| original|brightness(90)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572310124728_arrow.jpg" width="300"> | <img src="./media/1479425572310124728_brightness_90_arrow.jpg" width="300">  | <img src="./media/1479425572360010147_arrow.jpg" width="300"> | <img src="./media/1479425572360010147_brightness_90_arrow.jpg" width="300"> |


| original|brightness(80)| original|brightness(70)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425555406668683_arrow.jpg" width="300"> | <img src="./media/1479425555406668683_brightness_80_arrow.jpg" width="300">  | <img src="./media/1479425572310124728_arrow.jpg" width="300"> | <img src="./media/1479425572310124728_brightness_70_arrow.jpg" width="300"> |


| original|brightness(100)| original|contrast(1.8)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572310124728_arrow.jpg" width="300"> | <img src="./media/1479425572310124728_brightness_100_arrow.jpg" width="300">  | <img src="./media/1479425574110326325_arrow.jpg" width="300"> | <img src="./media/1479425574110326325_contrast_1.8_arrow.jpg" width="300"> |


| original|contrast(1.8)| original|brightness(90)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425574260461130_arrow.jpg" width="300"> | <img src="./media/1479425574260461130_contrast_1.8_arrow.jpg" width="300">  | <img src="./media/1479425555506801465_arrow.jpg" width="300"> | <img src="./media/1479425555506801465_brightness_90_arrow.jpg" width="300"> |


| original|brightness(50)| original|brightness(100)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578510049930_arrow.jpg" width="300"> | <img src="./media/1479425578510049930_brightness_50_arrow.jpg" width="300">  | <img src="./media/1479425578660949750_arrow.jpg" width="300"> | <img src="./media/1479425578660949750_brightness_100_arrow.jpg" width="300"> |


| original|brightness(100)| original|brightness(100)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572360010147_arrow.jpg" width="300"> | <img src="./media/1479425572360010147_brightness_100_arrow.jpg" width="300">  | <img src="./media/1479425572260066549_arrow.jpg" width="300"> | <img src="./media/1479425572260066549_brightness_100_arrow.jpg" width="300"> |


| original|brightness(100)| original|translation(10)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425555556824695_arrow.jpg" width="300"> | <img src="./media/1479425555556824695_brightness_100_arrow.jpg" width="300">  | <img src="./media/1479425573310229531_arrow.jpg" width="300"> | <img src="./media/1479425573310229531_translation_10_arrow.jpg" width="300"> |


| original|brightness(70)| original|brightness(90)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572411157865_arrow.jpg" width="300"> | <img src="./media/1479425572411157865_brightness_70_arrow.jpg" width="300">  | <img src="./media/1479425578660949750_arrow.jpg" width="300"> | <img src="./media/1479425578660949750_brightness_90_arrow.jpg" width="300"> |


| original|brightness(90)| original|brightness(80)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572260066549_arrow.jpg" width="300"> | <img src="./media/1479425572260066549_brightness_90_arrow.jpg" width="300">  | <img src="./media/1479425555456885076_arrow.jpg" width="300"> | <img src="./media/1479425555456885076_brightness_80_arrow.jpg" width="300"> |


| original|brightness(80)| original|translation(10)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572260066549_arrow.jpg" width="300"> | <img src="./media/1479425572260066549_brightness_80_arrow.jpg" width="300">  | <img src="./media/1479425573560335423_arrow.jpg" width="300"> | <img src="./media/1479425573560335423_translation_10_arrow.jpg" width="300"> |


| original|brightness(60)| original|brightness(80)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578610230854_arrow.jpg" width="300"> | <img src="./media/1479425578610230854_brightness_60_arrow.jpg" width="300">  | <img src="./media/1479425572411157865_arrow.jpg" width="300"> | <img src="./media/1479425572411157865_brightness_80_arrow.jpg" width="300"> |


| original|brightness(60)| original|brightness(100)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572360010147_arrow.jpg" width="300"> | <img src="./media/1479425572360010147_brightness_60_arrow.jpg" width="300">  | <img src="./media/1479425572210131608_arrow.jpg" width="300"> | <img src="./media/1479425572210131608_brightness_100_arrow.jpg" width="300"> |


| original|brightness(70)| original|brightness(60)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572260066549_arrow.jpg" width="300"> | <img src="./media/1479425572260066549_brightness_70_arrow.jpg" width="300">  | <img src="./media/1479425578359907740_arrow.jpg" width="300"> | <img src="./media/1479425578359907740_brightness_60_arrow.jpg" width="300"> |


| original|brightness(50)| original|brightness(60)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578409926566_arrow.jpg" width="300"> | <img src="./media/1479425578409926566_brightness_50_arrow.jpg" width="300">  | <img src="./media/1479425572411157865_arrow.jpg" width="300"> | <img src="./media/1479425572411157865_brightness_60_arrow.jpg" width="300"> |


| original|brightness(90)| original|brightness(70)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572411157865_arrow.jpg" width="300"> | <img src="./media/1479425572411157865_brightness_90_arrow.jpg" width="300">  | <img src="./media/1479425572460127373_arrow.jpg" width="300"> | <img src="./media/1479425572460127373_brightness_70_arrow.jpg" width="300"> |


| original|brightness(60)| original|brightness(80)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572310124728_arrow.jpg" width="300"> | <img src="./media/1479425572310124728_brightness_60_arrow.jpg" width="300">  | <img src="./media/1479425578260210617_arrow.jpg" width="300"> | <img src="./media/1479425578260210617_brightness_80_arrow.jpg" width="300"> |


| original|brightness(80)| original|brightness(60)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578660949750_arrow.jpg" width="300"> | <img src="./media/1479425578660949750_brightness_80_arrow.jpg" width="300">  | <img src="./media/1479425572460127373_arrow.jpg" width="300"> | <img src="./media/1479425572460127373_brightness_60_arrow.jpg" width="300"> |


| original|brightness(90)| original|brightness(50)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572210131608_arrow.jpg" width="300"> | <img src="./media/1479425572210131608_brightness_90_arrow.jpg" width="300">  | <img src="./media/1479425578559950992_arrow.jpg" width="300"> | <img src="./media/1479425578559950992_brightness_50_arrow.jpg" width="300"> |


| original|contrast(1.8)| original|brightness(70)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425574310305401_arrow.jpg" width="300"> | <img src="./media/1479425574310305401_contrast_1.8_arrow.jpg" width="300">  | <img src="./media/1479425578310238583_arrow.jpg" width="300"> | <img src="./media/1479425578310238583_brightness_70_arrow.jpg" width="300"> |


| original|brightness(90)| original|brightness(80)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425555556824695_arrow.jpg" width="300"> | <img src="./media/1479425555556824695_brightness_90_arrow.jpg" width="300">  | <img src="./media/1479425572210131608_arrow.jpg" width="300"> | <img src="./media/1479425572210131608_brightness_80_arrow.jpg" width="300"> |


| original|brightness(50)| original|brightness(80)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572411157865_arrow.jpg" width="300"> | <img src="./media/1479425572411157865_brightness_50_arrow.jpg" width="300">  | <img src="./media/1479425555506801465_arrow.jpg" width="300"> | <img src="./media/1479425555506801465_brightness_80_arrow.jpg" width="300"> |


| original|brightness(50)| original|brightness(70)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572460127373_arrow.jpg" width="300"> | <img src="./media/1479425572460127373_brightness_50_arrow.jpg" width="300">  | <img src="./media/1479425578660949750_arrow.jpg" width="300"> | <img src="./media/1479425578660949750_brightness_70_arrow.jpg" width="300"> |


| original|brightness(100)| original|brightness(50)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425555606707769_arrow.jpg" width="300"> | <img src="./media/1479425555606707769_brightness_100_arrow.jpg" width="300">  | <img src="./media/1479425572360010147_arrow.jpg" width="300"> | <img src="./media/1479425572360010147_brightness_50_arrow.jpg" width="300"> |


| original|contrast(1.8)| original|brightness(60)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425574060380700_arrow.jpg" width="300"> | <img src="./media/1479425574060380700_contrast_1.8_arrow.jpg" width="300">  | <img src="./media/1479425572260066549_arrow.jpg" width="300"> | <img src="./media/1479425572260066549_brightness_60_arrow.jpg" width="300"> |


| original|translation(10)| original|brightness(100)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425573610358944_arrow.jpg" width="300"> | <img src="./media/1479425573610358944_translation_10_arrow.jpg" width="300">  | <img src="./media/1479425578710309188_arrow.jpg" width="300"> | <img src="./media/1479425578710309188_brightness_100_arrow.jpg" width="300"> |


| original|brightness(70)| original|brightness(90)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572210131608_arrow.jpg" width="300"> | <img src="./media/1479425572210131608_brightness_70_arrow.jpg" width="300">  | <img src="./media/1479425578710309188_arrow.jpg" width="300"> | <img src="./media/1479425578710309188_brightness_90_arrow.jpg" width="300"> |


| original|translation(10)| original|translation(10)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425573260248557_arrow.jpg" width="300"> | <img src="./media/1479425573260248557_translation_10_arrow.jpg" width="300">  | <img src="./media/1479425572760140967_arrow.jpg" width="300"> | <img src="./media/1479425572760140967_translation_10_arrow.jpg" width="300"> |


| original|translation(10)| original|translation(10)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572710226941_arrow.jpg" width="300"> | <img src="./media/1479425572710226941_translation_10_arrow.jpg" width="300">  | <img src="./media/1479425572810176786_arrow.jpg" width="300"> | <img src="./media/1479425572810176786_translation_10_arrow.jpg" width="300"> |


| original|brightness(50)| original|brightness(50)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572310124728_arrow.jpg" width="300"> | <img src="./media/1479425572310124728_brightness_50_arrow.jpg" width="300">  | <img src="./media/1479425578610230854_arrow.jpg" width="300"> | <img src="./media/1479425578610230854_brightness_50_arrow.jpg" width="300"> |


| original|brightness(60)| original|brightness(100)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578660949750_arrow.jpg" width="300"> | <img src="./media/1479425578660949750_brightness_60_arrow.jpg" width="300">  | <img src="./media/1479425572159996266_arrow.jpg" width="300"> | <img src="./media/1479425572159996266_brightness_100_arrow.jpg" width="300"> |


| original|brightness(80)| original|translation(10)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578710309188_arrow.jpg" width="300"> | <img src="./media/1479425578710309188_brightness_80_arrow.jpg" width="300">  | <img src="./media/1479425572860178463_arrow.jpg" width="300"> | <img src="./media/1479425572860178463_translation_10_arrow.jpg" width="300"> |


| original|brightness(90)| original|brightness(60)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425555606707769_arrow.jpg" width="300"> | <img src="./media/1479425555606707769_brightness_90_arrow.jpg" width="300">  | <img src="./media/1479425578310238583_arrow.jpg" width="300"> | <img src="./media/1479425578310238583_brightness_60_arrow.jpg" width="300"> |


| original|brightness(80)| original|brightness(40)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425555556824695_arrow.jpg" width="300"> | <img src="./media/1479425555556824695_brightness_80_arrow.jpg" width="300">  | <img src="./media/1479425578460213280_arrow.jpg" width="300"> | <img src="./media/1479425578460213280_brightness_40_arrow.jpg" width="300"> |


| original|contrast(1.8)| original|contrast(1.8)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425574360826373_arrow.jpg" width="300"> | <img src="./media/1479425574360826373_contrast_1.8_arrow.jpg" width="300">  | <img src="./media/1479425573710305811_arrow.jpg" width="300"> | <img src="./media/1479425573710305811_contrast_1.8_arrow.jpg" width="300"> |


| original|brightness(50)| original|brightness(90)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578359907740_arrow.jpg" width="300"> | <img src="./media/1479425578359907740_brightness_50_arrow.jpg" width="300">  | <img src="./media/1479425572159996266_arrow.jpg" width="300"> | <img src="./media/1479425572159996266_brightness_90_arrow.jpg" width="300"> |


| original|contrast(1.8)| original|contrast(1.8)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425573660189561_arrow.jpg" width="300"> | <img src="./media/1479425573660189561_contrast_1.8_arrow.jpg" width="300">  | <img src="./media/1479425573610358944_arrow.jpg" width="300"> | <img src="./media/1479425573610358944_contrast_1.8_arrow.jpg" width="300"> |


| original|brightness(70)| original|brightness(100)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578710309188_arrow.jpg" width="300"> | <img src="./media/1479425578710309188_brightness_70_arrow.jpg" width="300">  | <img src="./media/1479425578760030245_arrow.jpg" width="300"> | <img src="./media/1479425578760030245_brightness_100_arrow.jpg" width="300"> |


| original|translation(10)| original|brightness(40)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425573660189561_arrow.jpg" width="300"> | <img src="./media/1479425573660189561_translation_10_arrow.jpg" width="300">  | <img src="./media/1479425578510049930_arrow.jpg" width="300"> | <img src="./media/1479425578510049930_brightness_40_arrow.jpg" width="300"> |


| original|brightness(90)| original|translation(10)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578760030245_arrow.jpg" width="300"> | <img src="./media/1479425578760030245_brightness_90_arrow.jpg" width="300">  | <img src="./media/1479425572910104234_arrow.jpg" width="300"> | <img src="./media/1479425572910104234_translation_10_arrow.jpg" width="300"> |


| original|translation(10)| original|translation(10)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425573210225556_arrow.jpg" width="300"> | <img src="./media/1479425573210225556_translation_10_arrow.jpg" width="300">  | <img src="./media/1479425572660350537_arrow.jpg" width="300"> | <img src="./media/1479425572660350537_translation_10_arrow.jpg" width="300"> |


| original|brightness(40)| original|brightness(60)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572411157865_arrow.jpg" width="300"> | <img src="./media/1479425572411157865_brightness_40_arrow.jpg" width="300">  | <img src="./media/1479425572210131608_arrow.jpg" width="300"> | <img src="./media/1479425572210131608_brightness_60_arrow.jpg" width="300"> |


| original|contrast(1.8)| original|brightness(80)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425574010306443_arrow.jpg" width="300"> | <img src="./media/1479425574010306443_contrast_1.8_arrow.jpg" width="300">  | <img src="./media/1479425572159996266_arrow.jpg" width="300"> | <img src="./media/1479425572159996266_brightness_80_arrow.jpg" width="300"> |


| original|brightness(50)| original|translation(10)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572260066549_arrow.jpg" width="300"> | <img src="./media/1479425572260066549_brightness_50_arrow.jpg" width="300">  | <img src="./media/1479425572960255643_arrow.jpg" width="300"> | <img src="./media/1479425572960255643_translation_10_arrow.jpg" width="300"> |


| original|brightness(40)| original|brightness(40)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572360010147_arrow.jpg" width="300"> | <img src="./media/1479425572360010147_brightness_40_arrow.jpg" width="300">  | <img src="./media/1479425578409926566_arrow.jpg" width="300"> | <img src="./media/1479425578409926566_brightness_40_arrow.jpg" width="300"> |


| original|brightness(80)| original|contrast(1.8)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578760030245_arrow.jpg" width="300"> | <img src="./media/1479425578760030245_brightness_80_arrow.jpg" width="300">  | <img src="./media/1479425573760218620_arrow.jpg" width="300"> | <img src="./media/1479425573760218620_contrast_1.8_arrow.jpg" width="300"> |


| original|translation(10)| original|brightness(60)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425573710305811_arrow.jpg" width="300"> | <img src="./media/1479425573710305811_translation_10_arrow.jpg" width="300">  | <img src="./media/1479425578710309188_arrow.jpg" width="300"> | <img src="./media/1479425578710309188_brightness_60_arrow.jpg" width="300"> |


| original|contrast(1.8)| original|translation(10)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425574410522828_arrow.jpg" width="300"> | <img src="./media/1479425574410522828_contrast_1.8_arrow.jpg" width="300">  | <img src="./media/1479425573010289372_arrow.jpg" width="300"> | <img src="./media/1479425573010289372_translation_10_arrow.jpg" width="300"> |


| original|brightness(70)| original|brightness(50)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572159996266_arrow.jpg" width="300"> | <img src="./media/1479425572159996266_brightness_70_arrow.jpg" width="300">  | <img src="./media/1479425578660949750_arrow.jpg" width="300"> | <img src="./media/1479425578660949750_brightness_50_arrow.jpg" width="300"> |


| original|brightness(40)| original|translation(10)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578559950992_arrow.jpg" width="300"> | <img src="./media/1479425578559950992_brightness_40_arrow.jpg" width="300">  | <img src="./media/1479425573060269318_arrow.jpg" width="300"> | <img src="./media/1479425573060269318_translation_10_arrow.jpg" width="300"> |


| original|brightness(100)| original|brightness(100)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425582711810630_arrow.jpg" width="300"> | <img src="./media/1479425582711810630_brightness_100_arrow.jpg" width="300">  | <img src="./media/1479425582661896163_arrow.jpg" width="300"> | <img src="./media/1479425582661896163_brightness_100_arrow.jpg" width="300"> |


| original|brightness(70)| original|translation(10)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578760030245_arrow.jpg" width="300"> | <img src="./media/1479425578760030245_brightness_70_arrow.jpg" width="300">  | <img src="./media/1479425573160140587_arrow.jpg" width="300"> | <img src="./media/1479425573160140587_translation_10_arrow.jpg" width="300"> |


| original|translation(10)| original|contrast(1.8)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425573110137849_arrow.jpg" width="300"> | <img src="./media/1479425573110137849_translation_10_arrow.jpg" width="300">  | <img src="./media/1479425573810366349_arrow.jpg" width="300"> | <img src="./media/1479425573810366349_contrast_1.8_arrow.jpg" width="300"> |


| original|translation(10)| original|brightness(40)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425573760218620_arrow.jpg" width="300"> | <img src="./media/1479425573760218620_translation_10_arrow.jpg" width="300">  | <img src="./media/1479425572310124728_arrow.jpg" width="300"> | <img src="./media/1479425572310124728_brightness_40_arrow.jpg" width="300"> |


| original|translation(10)| original|contrast(1.8)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572610024407_arrow.jpg" width="300"> | <img src="./media/1479425572610024407_translation_10_arrow.jpg" width="300">  | <img src="./media/1479425573560335423_arrow.jpg" width="300"> | <img src="./media/1479425573560335423_contrast_1.8_arrow.jpg" width="300"> |


| original|brightness(100)| original|brightness(90)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425582611936634_arrow.jpg" width="300"> | <img src="./media/1479425582611936634_brightness_100_arrow.jpg" width="300">  | <img src="./media/1479425578810428555_arrow.jpg" width="300"> | <img src="./media/1479425578810428555_brightness_90_arrow.jpg" width="300"> |


| original|brightness(100)| original|translation(10)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578810428555_arrow.jpg" width="300"> | <img src="./media/1479425578810428555_brightness_100_arrow.jpg" width="300">  | <img src="./media/1479425573810366349_arrow.jpg" width="300"> | <img src="./media/1479425573810366349_translation_10_arrow.jpg" width="300"> |


| original|brightness(60)| original|brightness(40)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578760030245_arrow.jpg" width="300"> | <img src="./media/1479425578760030245_brightness_60_arrow.jpg" width="300">  | <img src="./media/1479425578610230854_arrow.jpg" width="300"> | <img src="./media/1479425578610230854_brightness_40_arrow.jpg" width="300"> |


| original|contrast(1.8)| original|contrast(1.8)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425574460394479_arrow.jpg" width="300"> | <img src="./media/1479425574460394479_contrast_1.8_arrow.jpg" width="300">  | <img src="./media/1479425573910233411_arrow.jpg" width="300"> | <img src="./media/1479425573910233411_contrast_1.8_arrow.jpg" width="300"> |


| original|contrast(1.8)| original|contrast(1.8)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425573960279718_arrow.jpg" width="300"> | <img src="./media/1479425573960279718_contrast_1.8_arrow.jpg" width="300">  | <img src="./media/1479425573860170819_arrow.jpg" width="300"> | <img src="./media/1479425573860170819_contrast_1.8_arrow.jpg" width="300"> |


| original|brightness(50)| original|brightness(80)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578710309188_arrow.jpg" width="300"> | <img src="./media/1479425578710309188_brightness_50_arrow.jpg" width="300">  | <img src="./media/1479425578810428555_arrow.jpg" width="300"> | <img src="./media/1479425578810428555_brightness_80_arrow.jpg" width="300"> |


| original|brightness(50)| original|brightness(60)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425572210131608_arrow.jpg" width="300"> | <img src="./media/1479425572210131608_brightness_50_arrow.jpg" width="300">  | <img src="./media/1479425572159996266_arrow.jpg" width="300"> | <img src="./media/1479425572159996266_brightness_60_arrow.jpg" width="300"> |


| original|brightness(70)| original|brightness(40)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578810428555_arrow.jpg" width="300"> | <img src="./media/1479425578810428555_brightness_70_arrow.jpg" width="300">  | <img src="./media/1479425572260066549_arrow.jpg" width="300"> | <img src="./media/1479425572260066549_brightness_40_arrow.jpg" width="300"> |


| original|brightness(40)| original|brightness(90)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578359907740_arrow.jpg" width="300"> | <img src="./media/1479425578359907740_brightness_40_arrow.jpg" width="300">  | <img src="./media/1479425578860396761_arrow.jpg" width="300"> | <img src="./media/1479425578860396761_brightness_90_arrow.jpg" width="300"> |


| original|contrast(1.8)| original|brightness(50)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425573510293691_arrow.jpg" width="300"> | <img src="./media/1479425573510293691_contrast_1.8_arrow.jpg" width="300">  | <img src="./media/1479425578760030245_arrow.jpg" width="300"> | <img src="./media/1479425578760030245_brightness_50_arrow.jpg" width="300"> |


| original|brightness(80)| original|brightness(40)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578860396761_arrow.jpg" width="300"> | <img src="./media/1479425578860396761_brightness_80_arrow.jpg" width="300">  | <img src="./media/1479425578660949750_arrow.jpg" width="300"> | <img src="./media/1479425578660949750_brightness_40_arrow.jpg" width="300"> |


| original|brightness(60)| original|brightness(70)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578810428555_arrow.jpg" width="300"> | <img src="./media/1479425578810428555_brightness_60_arrow.jpg" width="300">  | <img src="./media/1479425578860396761_arrow.jpg" width="300"> | <img src="./media/1479425578860396761_brightness_70_arrow.jpg" width="300"> |


| original|brightness(40)| original|brightness(50)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578710309188_arrow.jpg" width="300"> | <img src="./media/1479425578710309188_brightness_40_arrow.jpg" width="300">  | <img src="./media/1479425572159996266_arrow.jpg" width="300"> | <img src="./media/1479425572159996266_brightness_50_arrow.jpg" width="300"> |


| original|brightness(60)| original|contrast(1.8)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578860396761_arrow.jpg" width="300"> | <img src="./media/1479425578860396761_brightness_60_arrow.jpg" width="300">  | <img src="./media/1479425573460229446_arrow.jpg" width="300"> | <img src="./media/1479425573460229446_contrast_1.8_arrow.jpg" width="300"> |


| original|brightness(50)| original|brightness(40)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425578810428555_arrow.jpg" width="300"> | <img src="./media/1479425578810428555_brightness_50_arrow.jpg" width="300">  | <img src="./media/1479425572210131608_arrow.jpg" width="300"> | <img src="./media/1479425572210131608_brightness_40_arrow.jpg" width="300"> |


| original|contrast(1.8)| original|brightness(40)|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425573410225191_arrow.jpg" width="300"> | <img src="./media/1479425573410225191_contrast_1.8_arrow.jpg" width="300">  | <img src="./media/1479425578760030245_arrow.jpg" width="300"> | <img src="./media/1479425578760030245_brightness_40_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425487544586069_arrow.jpg" width="300"> | <img src="./media/1479425487544586069_fog_arrow.jpg" width="300">  | <img src="./media/1479425487594171655_arrow.jpg" width="300"> | <img src="./media/1479425487594171655_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425487644294769_arrow.jpg" width="300"> | <img src="./media/1479425487644294769_fog_arrow.jpg" width="300">  | <img src="./media/1479425487694272050_arrow.jpg" width="300"> | <img src="./media/1479425487694272050_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425487744232612_arrow.jpg" width="300"> | <img src="./media/1479425487744232612_fog_arrow.jpg" width="300">  | <img src="./media/1479425487794351214_arrow.jpg" width="300"> | <img src="./media/1479425487794351214_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425487844203409_arrow.jpg" width="300"> | <img src="./media/1479425487844203409_fog_arrow.jpg" width="300">  | <img src="./media/1479425487894242789_arrow.jpg" width="300"> | <img src="./media/1479425487894242789_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425487944331268_arrow.jpg" width="300"> | <img src="./media/1479425487944331268_fog_arrow.jpg" width="300">  | <img src="./media/1479425487994249169_arrow.jpg" width="300"> | <img src="./media/1479425487994249169_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425488044375871_arrow.jpg" width="300"> | <img src="./media/1479425488044375871_fog_arrow.jpg" width="300">  | <img src="./media/1479425488094513517_arrow.jpg" width="300"> | <img src="./media/1479425488094513517_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425488144363495_arrow.jpg" width="300"> | <img src="./media/1479425488144363495_fog_arrow.jpg" width="300">  | <img src="./media/1479425488194522932_arrow.jpg" width="300"> | <img src="./media/1479425488194522932_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425488244177248_arrow.jpg" width="300"> | <img src="./media/1479425488244177248_fog_arrow.jpg" width="300">  | <img src="./media/1479425488294190492_arrow.jpg" width="300"> | <img src="./media/1479425488294190492_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425488344463413_arrow.jpg" width="300"> | <img src="./media/1479425488344463413_fog_arrow.jpg" width="300">  | <img src="./media/1479425488394166804_arrow.jpg" width="300"> | <img src="./media/1479425488394166804_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425488444301767_arrow.jpg" width="300"> | <img src="./media/1479425488444301767_fog_arrow.jpg" width="300">  | <img src="./media/1479425488494235228_arrow.jpg" width="300"> | <img src="./media/1479425488494235228_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425488544582948_arrow.jpg" width="300"> | <img src="./media/1479425488544582948_fog_arrow.jpg" width="300">  | <img src="./media/1479425488594640273_arrow.jpg" width="300"> | <img src="./media/1479425488594640273_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425488644373500_arrow.jpg" width="300"> | <img src="./media/1479425488644373500_fog_arrow.jpg" width="300">  | <img src="./media/1479425488694449473_arrow.jpg" width="300"> | <img src="./media/1479425488694449473_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425488744496100_arrow.jpg" width="300"> | <img src="./media/1479425488744496100_fog_arrow.jpg" width="300">  | <img src="./media/1479425488794919110_arrow.jpg" width="300"> | <img src="./media/1479425488794919110_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425488844445874_arrow.jpg" width="300"> | <img src="./media/1479425488844445874_fog_arrow.jpg" width="300">  | <img src="./media/1479425488894592942_arrow.jpg" width="300"> | <img src="./media/1479425488894592942_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425488944488527_arrow.jpg" width="300"> | <img src="./media/1479425488944488527_fog_arrow.jpg" width="300">  | <img src="./media/1479425488994540598_arrow.jpg" width="300"> | <img src="./media/1479425488994540598_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425489044630045_arrow.jpg" width="300"> | <img src="./media/1479425489044630045_fog_arrow.jpg" width="300">  | <img src="./media/1479425489094638546_arrow.jpg" width="300"> | <img src="./media/1479425489094638546_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425489144756926_arrow.jpg" width="300"> | <img src="./media/1479425489144756926_fog_arrow.jpg" width="300">  | <img src="./media/1479425489194941386_arrow.jpg" width="300"> | <img src="./media/1479425489194941386_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425489244752068_arrow.jpg" width="300"> | <img src="./media/1479425489244752068_fog_arrow.jpg" width="300">  | <img src="./media/1479425489294597543_arrow.jpg" width="300"> | <img src="./media/1479425489294597543_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425489344631737_arrow.jpg" width="300"> | <img src="./media/1479425489344631737_fog_arrow.jpg" width="300">  | <img src="./media/1479425489394648780_arrow.jpg" width="300"> | <img src="./media/1479425489394648780_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425489444718542_arrow.jpg" width="300"> | <img src="./media/1479425489444718542_fog_arrow.jpg" width="300">  | <img src="./media/1479425489495361171_arrow.jpg" width="300"> | <img src="./media/1479425489495361171_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425489744721210_arrow.jpg" width="300"> | <img src="./media/1479425489744721210_fog_arrow.jpg" width="300">  | <img src="./media/1479425489795375605_arrow.jpg" width="300"> | <img src="./media/1479425489795375605_fog_arrow.jpg" width="300"> |


| original          | fog          | original | fog|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425489844681471_arrow.jpg" width="300"> | <img src="./media/1479425489844681471_fog_arrow.jpg" width="300">  | <img src="./media/1479425489894813556_arrow.jpg" width="300"> | <img src="./media/1479425489894813556_fog_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425450387736225_arrow.jpg" width="300"> | <img src="./media/1479425450387736225_rain_arrow.jpg" width="300">  | <img src="./media/1479425450437633063_arrow.jpg" width="300"> | <img src="./media/1479425450437633063_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425450487629515_arrow.jpg" width="300"> | <img src="./media/1479425450487629515_rain_arrow.jpg" width="300">  | <img src="./media/1479425450537693455_arrow.jpg" width="300"> | <img src="./media/1479425450537693455_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425450587926787_arrow.jpg" width="300"> | <img src="./media/1479425450587926787_rain_arrow.jpg" width="300">  | <img src="./media/1479425450637667263_arrow.jpg" width="300"> | <img src="./media/1479425450637667263_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425450687712799_arrow.jpg" width="300"> | <img src="./media/1479425450687712799_rain_arrow.jpg" width="300">  | <img src="./media/1479425450737697908_arrow.jpg" width="300"> | <img src="./media/1479425450737697908_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425450787679324_arrow.jpg" width="300"> | <img src="./media/1479425450787679324_rain_arrow.jpg" width="300">  | <img src="./media/1479425450837705965_arrow.jpg" width="300"> | <img src="./media/1479425450837705965_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425450887747982_arrow.jpg" width="300"> | <img src="./media/1479425450887747982_rain_arrow.jpg" width="300">  | <img src="./media/1479425450937763410_arrow.jpg" width="300"> | <img src="./media/1479425450937763410_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425450987742643_arrow.jpg" width="300"> | <img src="./media/1479425450987742643_rain_arrow.jpg" width="300">  | <img src="./media/1479425451037800301_arrow.jpg" width="300"> | <img src="./media/1479425451037800301_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425451087748243_arrow.jpg" width="300"> | <img src="./media/1479425451087748243_rain_arrow.jpg" width="300">  | <img src="./media/1479425451137712996_arrow.jpg" width="300"> | <img src="./media/1479425451137712996_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425451188093502_arrow.jpg" width="300"> | <img src="./media/1479425451188093502_rain_arrow.jpg" width="300">  | <img src="./media/1479425451237936062_arrow.jpg" width="300"> | <img src="./media/1479425451237936062_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425451287831550_arrow.jpg" width="300"> | <img src="./media/1479425451287831550_rain_arrow.jpg" width="300">  | <img src="./media/1479425451338117861_arrow.jpg" width="300"> | <img src="./media/1479425451338117861_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425451388204158_arrow.jpg" width="300"> | <img src="./media/1479425451388204158_rain_arrow.jpg" width="300">  | <img src="./media/1479425451438015086_arrow.jpg" width="300"> | <img src="./media/1479425451438015086_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425451487954445_arrow.jpg" width="300"> | <img src="./media/1479425451487954445_rain_arrow.jpg" width="300">  | <img src="./media/1479425451537890765_arrow.jpg" width="300"> | <img src="./media/1479425451537890765_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425451588254261_arrow.jpg" width="300"> | <img src="./media/1479425451588254261_rain_arrow.jpg" width="300">  | <img src="./media/1479425451637830513_arrow.jpg" width="300"> | <img src="./media/1479425451637830513_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425451687836583_arrow.jpg" width="300"> | <img src="./media/1479425451687836583_rain_arrow.jpg" width="300">  | <img src="./media/1479425454088914759_arrow.jpg" width="300"> | <img src="./media/1479425454088914759_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425454138995578_arrow.jpg" width="300"> | <img src="./media/1479425454138995578_rain_arrow.jpg" width="300">  | <img src="./media/1479425454189032032_arrow.jpg" width="300"> | <img src="./media/1479425454189032032_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425454239072802_arrow.jpg" width="300"> | <img src="./media/1479425454239072802_rain_arrow.jpg" width="300">  | <img src="./media/1479425454288997748_arrow.jpg" width="300"> | <img src="./media/1479425454288997748_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425454339153057_arrow.jpg" width="300"> | <img src="./media/1479425454339153057_rain_arrow.jpg" width="300">  | <img src="./media/1479425484143787396_arrow.jpg" width="300"> | <img src="./media/1479425484143787396_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425484193891524_arrow.jpg" width="300"> | <img src="./media/1479425484193891524_rain_arrow.jpg" width="300">  | <img src="./media/1479425484243761144_arrow.jpg" width="300"> | <img src="./media/1479425484243761144_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425484293644999_arrow.jpg" width="300"> | <img src="./media/1479425484293644999_rain_arrow.jpg" width="300">  | <img src="./media/1479425484343750085_arrow.jpg" width="300"> | <img src="./media/1479425484343750085_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425484393766777_arrow.jpg" width="300"> | <img src="./media/1479425484393766777_rain_arrow.jpg" width="300">  | <img src="./media/1479425484444200094_arrow.jpg" width="300"> | <img src="./media/1479425484444200094_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425484493700831_arrow.jpg" width="300"> | <img src="./media/1479425484493700831_rain_arrow.jpg" width="300">  | <img src="./media/1479425484543846628_arrow.jpg" width="300"> | <img src="./media/1479425484543846628_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425484593811806_arrow.jpg" width="300"> | <img src="./media/1479425484593811806_rain_arrow.jpg" width="300">  | <img src="./media/1479425484643680871_arrow.jpg" width="300"> | <img src="./media/1479425484643680871_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425484693712982_arrow.jpg" width="300"> | <img src="./media/1479425484693712982_rain_arrow.jpg" width="300">  | <img src="./media/1479425484743748958_arrow.jpg" width="300"> | <img src="./media/1479425484743748958_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425484793863790_arrow.jpg" width="300"> | <img src="./media/1479425484793863790_rain_arrow.jpg" width="300">  | <img src="./media/1479425484843782512_arrow.jpg" width="300"> | <img src="./media/1479425484843782512_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425484893828668_arrow.jpg" width="300"> | <img src="./media/1479425484893828668_rain_arrow.jpg" width="300">  | <img src="./media/1479425484944071871_arrow.jpg" width="300"> | <img src="./media/1479425484944071871_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425487094283294_arrow.jpg" width="300"> | <img src="./media/1479425487094283294_rain_arrow.jpg" width="300">  | <img src="./media/1479425487144225750_arrow.jpg" width="300"> | <img src="./media/1479425487144225750_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425487194348504_arrow.jpg" width="300"> | <img src="./media/1479425487194348504_rain_arrow.jpg" width="300">  | <img src="./media/1479425487244330562_arrow.jpg" width="300"> | <img src="./media/1479425487244330562_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425487294150834_arrow.jpg" width="300"> | <img src="./media/1479425487294150834_rain_arrow.jpg" width="300">  | <img src="./media/1479425487344263425_arrow.jpg" width="300"> | <img src="./media/1479425487344263425_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425487394168676_arrow.jpg" width="300"> | <img src="./media/1479425487394168676_rain_arrow.jpg" width="300">  | <img src="./media/1479425487444223901_arrow.jpg" width="300"> | <img src="./media/1479425487444223901_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425487494192261_arrow.jpg" width="300"> | <img src="./media/1479425487494192261_rain_arrow.jpg" width="300">  | <img src="./media/1479425487544586069_arrow.jpg" width="300"> | <img src="./media/1479425487544586069_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425487594171655_arrow.jpg" width="300"> | <img src="./media/1479425487594171655_rain_arrow.jpg" width="300">  | <img src="./media/1479425487644294769_arrow.jpg" width="300"> | <img src="./media/1479425487644294769_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425487694272050_arrow.jpg" width="300"> | <img src="./media/1479425487694272050_rain_arrow.jpg" width="300">  | <img src="./media/1479425487744232612_arrow.jpg" width="300"> | <img src="./media/1479425487744232612_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425487794351214_arrow.jpg" width="300"> | <img src="./media/1479425487794351214_rain_arrow.jpg" width="300">  | <img src="./media/1479425487844203409_arrow.jpg" width="300"> | <img src="./media/1479425487844203409_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425487894242789_arrow.jpg" width="300"> | <img src="./media/1479425487894242789_rain_arrow.jpg" width="300">  | <img src="./media/1479425487944331268_arrow.jpg" width="300"> | <img src="./media/1479425487944331268_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425487994249169_arrow.jpg" width="300"> | <img src="./media/1479425487994249169_rain_arrow.jpg" width="300">  | <img src="./media/1479425488044375871_arrow.jpg" width="300"> | <img src="./media/1479425488044375871_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425488094513517_arrow.jpg" width="300"> | <img src="./media/1479425488094513517_rain_arrow.jpg" width="300">  | <img src="./media/1479425488144363495_arrow.jpg" width="300"> | <img src="./media/1479425488144363495_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425488194522932_arrow.jpg" width="300"> | <img src="./media/1479425488194522932_rain_arrow.jpg" width="300">  | <img src="./media/1479425488244177248_arrow.jpg" width="300"> | <img src="./media/1479425488244177248_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425488294190492_arrow.jpg" width="300"> | <img src="./media/1479425488294190492_rain_arrow.jpg" width="300">  | <img src="./media/1479425488344463413_arrow.jpg" width="300"> | <img src="./media/1479425488344463413_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425488394166804_arrow.jpg" width="300"> | <img src="./media/1479425488394166804_rain_arrow.jpg" width="300">  | <img src="./media/1479425488444301767_arrow.jpg" width="300"> | <img src="./media/1479425488444301767_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425488494235228_arrow.jpg" width="300"> | <img src="./media/1479425488494235228_rain_arrow.jpg" width="300">  | <img src="./media/1479425488544582948_arrow.jpg" width="300"> | <img src="./media/1479425488544582948_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425488594640273_arrow.jpg" width="300"> | <img src="./media/1479425488594640273_rain_arrow.jpg" width="300">  | <img src="./media/1479425488644373500_arrow.jpg" width="300"> | <img src="./media/1479425488644373500_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425488694449473_arrow.jpg" width="300"> | <img src="./media/1479425488694449473_rain_arrow.jpg" width="300">  | <img src="./media/1479425488744496100_arrow.jpg" width="300"> | <img src="./media/1479425488744496100_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425488794919110_arrow.jpg" width="300"> | <img src="./media/1479425488794919110_rain_arrow.jpg" width="300">  | <img src="./media/1479425488844445874_arrow.jpg" width="300"> | <img src="./media/1479425488844445874_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425488894592942_arrow.jpg" width="300"> | <img src="./media/1479425488894592942_rain_arrow.jpg" width="300">  | <img src="./media/1479425488944488527_arrow.jpg" width="300"> | <img src="./media/1479425488944488527_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425488994540598_arrow.jpg" width="300"> | <img src="./media/1479425488994540598_rain_arrow.jpg" width="300">  | <img src="./media/1479425489044630045_arrow.jpg" width="300"> | <img src="./media/1479425489044630045_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425489094638546_arrow.jpg" width="300"> | <img src="./media/1479425489094638546_rain_arrow.jpg" width="300">  | <img src="./media/1479425489144756926_arrow.jpg" width="300"> | <img src="./media/1479425489144756926_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425489194941386_arrow.jpg" width="300"> | <img src="./media/1479425489194941386_rain_arrow.jpg" width="300">  | <img src="./media/1479425489244752068_arrow.jpg" width="300"> | <img src="./media/1479425489244752068_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425489294597543_arrow.jpg" width="300"> | <img src="./media/1479425489294597543_rain_arrow.jpg" width="300">  | <img src="./media/1479425489344631737_arrow.jpg" width="300"> | <img src="./media/1479425489344631737_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425489394648780_arrow.jpg" width="300"> | <img src="./media/1479425489394648780_rain_arrow.jpg" width="300">  | <img src="./media/1479425489444718542_arrow.jpg" width="300"> | <img src="./media/1479425489444718542_rain_arrow.jpg" width="300"> |


| original          | rain          | original | rain|
| -------------     | -------------  | -------- | ---------- |
| <img src="./media/1479425489495361171_arrow.jpg" width="300"> | <img src="./media/1479425489495361171_rain_arrow.jpg" width="300">  | <img src="./media/1479425489544698642_arrow.jpg" width="300"> | <img src="./media/1479425489544698642_rain_arrow.jpg" width="300"> |










## Conclusion

Using pseudo-oracles or metamorphic testing reduces testing effort and enables
bug to be found that might otherwise be overlooked.

[1]: Elaine J. Weyuker, On Testing Non-Testable Programs, The Computer Journal, Volume 25, Issue 4, November 1982, Pages 465–470, https://doi.org/10.1093/comjnl/25.4.465.

[2]: Kshirasagar Naik and Priyadarshi Tripathy. 2018. Software Testing and Quality Assurance: Theory and Practice (2nd ed.). Wiley Publishing.

[3]: J. Carver, N. P. C. Hong, and G. K. Thiruvathukal, Eds., Software engineering for science. Boca Raton: Taylor & Francis, CRC Press, 2017.

[4]: T. Y. Chen, S. C. Cheung, and S. M. Yiu, “Metamorphic testing: a new approach for generating next test cases,” Technical Report HKUST-CS98–01, Department of Computer Science, Hong Kong University of Science and Technology, Hong Kong, 1998.

[5]: Giannoulatou, E., Park, S. H., Humphreys, D. T., & Ho, J. W. (). Verification and validation of bioinformatics software without a gold standard: a case study of BWA and Bowtie. BMC bioinformatics, 15 Suppl 16(Suppl 16), S15. doi:10.1186/1471-2105-15-S16-S15

[6] Tsong Yueh Chen, Fei-Ching Kuo, Huai Liu, Pak-Lok Poon, Dave Towey, T. H. Tse, and Zhi Quan Zhou. 2018. Metamorphic testing: A review of challenges and opportunities. ACM Computing Surveys 51, 1 (2018), 4:1–4:27.

[7] Joshua Brown, Zhi Quan Zhou, and Yang-Wai Chow. 2018. Metamorphic testing of navigation software: A pilot study with Google Maps. In Proceedings of the 51st Annual Hawaii International Conference on System Sciences (HICSS-51). 5687–5696. Available: http://hdl.handle.net/10125/50602.

[8] https://arxiv.org/abs/1708.08559
