Analysis of an Italian Emergency Department
===========================================

.. contents::
  :local:

The project focuses on the analysis and simulation of the process carried out at an emergency department of a Italian hospital. The exploited log is available at `ED_Log.xes <./ED_Log.xes>`_.


Description of the Process and of the Event Log
+++++++++++++++++++++++++++++++++++++++++++++++

The process starts with a triage. Triage refers to the evaluation and categorization of the sick or wounded when there are insufficient resources for medical care for everyone at once. 

There are two ways to perform this triage. The first is when a patient autonomously goes the ED (Autonomous Triage). Alternatively, a patient arrives by ambulance (Ambulance Triage). In both cases, a triage nurse carries out the required activities.

In this hospital, the triage activity assigns a triage color to the patient, which depends on the patient's severity, and thus on the urgency of the patient's treatment. The hospital managers determined a five-level triage that was each represented by a color: Red (immediate), yellow (observation), green (wait), blue (expectant), and white (dismiss). 

After the triage activity, the patient may undergo a blood sampling by a nurse if necessary. Then, a physician (i.e., a doctor) visits the patient. The physician can decide to discharge the patient immediately, but frequently (s)he decides that the patient needs further steps:

* observation: The patient is retained at the ED to track his/her health stability. The patient is not sent to some hospital ward, but kept at the ED. There are a limited number of beds at the ED, one of which needs to be available for a patient to be under observation;
* laboratory test: This activity is at times carried out to verify the patient's condition
* emergency service: This activity indicates the performance of other types of support given to the patient. To simplify the process analysis, all these other support types are grouped under a single activity type.
* radiological Examination: Sometimes, it is necessary to carry out some medical imaging of different nature: 
  
  * ANGIO: Angiography 
  * ECHO: Echocardiagram 
  * MRI: Magnetic Resonance Imagining 
  * TC: Computed Tomography 
  * X-Ray: Radiographic testing 

  After completing the required radiological examination, a radiological report is prepared as separate activity. A radiological report is not prepared for the Echocardiagram test. 
* Consultation activities: Patients are directed to medical specialists in the hospital, outside the ED. 

Each patient can undergo any of the steps above, including none or everyone: 
indeed, each of them is optional. Afterwards, the patient is discharged.

In the event log, each trace refers to a different patient and contains the occurrence 
of the activities performed for those patients. The event log also contains the 
information about the resources that perform the activities. The ED works 7/24 with 
three shifts. Shifts hours are 00:00-08:00, 08:00-16:00, 16:00-00:00. The resources are equally divided in those periods of the day. 

The event log also contains the information about the triage colors, which are the following, ordered by descending severity: red, yellow, green, blue, and white. Note that the ED defines a Key Performance Indicator (abbreviation KPI) that is used to determine whether process executions (i.e., the patient treatment) are adequate. In particular, the KPI is related to the first response time, namely the time elapsed between the triage and the beginning of the patient's treatment (e.g., the blood sampling or the visit). The satisfactory KPI values depend on the triage color. Table 1 summarizes the threshold values for the five triage colors. 

.. _KPI-table:  

.. list-table:: Key Performance Indicator

  * - Triage color
    - Meaning
    - First time response
  * - Red
    - Immediate
    - <= 10 minutes
  * - Yellow
    - Observation
    - <= 20 minutes
  * - Green
    - Wait
    - <= 60 minutes
  * - Blue
    - Expectant
    - <= 90 minutes
  * - White
    - Dismiss
    - <= 120 minutes

Questions
+++++++++

The assignment is to answer the following questions, using process mining techniques.

Question 1
----------
The hospital wants to gain further insight into how the process is executed. Suppose you are a process analyst. You want to provide a Petri net that represents the actual process executions. Draw a Petri net and validate it by checking its conformance using alignments against the event log. If the alignment shows that the model is not satisfactory, iteratively improve the model until the quality of satisfactory. The model is deemed satisfactory if the fitness value is at least 0.85 and the precision value is at least 
0.68. Note that in general, precision values of 0.68 are considered low. However, the health-care domains are typically characterized by a large variability which corresponds to an amount of different behavior that is difficult to put into a precise model.

Question 2
----------
The hospital stakeholders wonder whether the typical process behavior depends on the triage color, and whether patients are treated with the key performance indicator defined in KPI-table_: 

#. Discover process models for different triage colors, and compare whether or not significant differences are observed in the models of different triage colors. 
#. Verify whether the hospital treats patients in accordance with the indicators of KPI-table_. If some patients are not treated according to KPI-table_, find what their percentage is. 


Question 3
----------
The hospital is unsatisfied with the costs: there are certainly too many resources at the ED. Use Process Simulation to reduce the number of resources while keeping similar case duration. First, build a simulation model in BIMP that defines case arrival rate, resource roles, task durations, branching probabilities. Then, work with different resources allocated per role and reduce them in number while keeping similar case duration.

Answers
++++++++++++++++++++
The answers and adopted solutions are available at the report `Analysis of an italian ED <./analysis-of-an-Italian-Emergency-Department.pdf>`_. Moreover, you can find the code written for analysis at the following colab: `https://colab.research.google.com/drive/1RsszOawY-SAbywpFEiGkebFcGx_NAZ2y?usp=sharing <https://colab.research.google.com/drive/1RsszOawY-SAbywpFEiGkebFcGx_NAZ2y?usp=sharing>`_

Tools
+++++

* WoPeD: software for modelling, simulating and analyzing processes described by workflow nets [1]_.
* ProM Lite: extensible framework that supports a wide variety of process mining techniques in the form of plugins [2]_.
* PM4PY: python library implementing a variety of process mining algorithms [3]_.
* BIMP: business process simulator for BPMN [4]_.

References
++++++++++
.. [1] `WoPeD https://woped.dhbw-karlsruhe.de <https://woped.dhbw-karlsruhe.de>`_
.. [2] `ProM Lite https://promtools.org <https://promtools.org/>`_
.. [3] `PM4PY https://pm4py.fit.fraunhofer.de <https://pm4py.fit.fraunhofer.de/>`_
.. [4] `BIMP https://bimp.cs.ut.ee/ <https://bimp.cs.ut.ee/>`_
