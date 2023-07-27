# Optimization of Automated and Manual Software Tests in Industrial Practice: A Survey and Historical Analysis

This supplementary website enriches the paper _Optimization of Automated and Manual Software Tests in
Industrial Practice: A Survey and Historical Analysis_, currently submitted at the Research Track of ICSE 2024. We provide more details on our study subjects (Section 3 of the paper), list the questions of our questionnaire (Section 3 of the paper), discuss study-subject specific results (Section 4 of the paper), and provide access to the plotting scripts used for the paper charts, for reproducibility reasons.

## Additional Insights About Study Subjects

The following table provides an overview of our five study subjects from industry. It specifies their domain, which test process we used to investigate optimization techniques, their (development and test) team size, the size of the system under test in source lines of code (SLOC) and in which language the system under test is implemented.

| Company                        | Domain          | Test Process    | Team Size | SLOC   | Language |
|--------------------------------|-----------------|---------|------:|--------:|----------|
| Time<sup>[1]</sup>                           | Time Management | A       | 50   | 8 M   | Java     |
| BVK                            | Finance         | A       | 20   | 300 K | Java     |
| Dolby                          | Audio           | A       | 10   | 28 K  | C        |
| ILP                            | ERP             | M       | 5    | 831 K | C\#      |
| Zeiss                          | Optics          | M       | 90   | 6 M   | C\#      |

<sup>[1]</sup> Subject anonymized due to NDA

## Survey Questions

As outlined in Section 3.4 of our paper, we answer several research questions of RA<sub>1</sub> ( Test Strategies) using an open-text survey. The following table lists all survey questions and maps these to the research questions (RQ) in the paper. 


|RQ | Survey Question|
|--:|------------------------------------------------------------------------------------|
|1.2|How many test engineers (e.g., testers, test developers) are there in your project? |
|1.2|How many test engineers spend their whole working time on testing? |
|1.2|How many test engineers work with the automated test suite? |
|1.2|How many test engineers work with the manual test suite? |
|||
|1.1|Which test activities are performed via automated tests? |
|1.2|How much time do you estimate is invested into maintaining the automated test suite? |
|1.3|What are bottlenecks in your automated test process? |
|1.5|How much automated testing effort would you desire? |
|1.3|Are there flaky automated test cases? |
|||
|1.1|Which test activities are performed manually? |
|1.1|How big is the manual test suite overall? |
|1.2|How many manual test cycles take place per year? |
|1.2|Is the entire manual test suite executed in every test cycle? |
|1.2|How many test cases are executed per manual test cycle? |
|1.1|Which events trigger the execution of a manual test case? |
|1.2, 1.4|How long does it take to execute the entire manual test suite? |
|1.2|How much time do you estimate is invested into maintaining the manual test suite? |
|1.2|What are bottlenecks in your manual test process? |
|1.2|How much manual testing effort would you desire? |
|1.3|Are there flaky manual test cases? |

## Study-Subject Specific Discussion 

We provide more details on our study subjects and their testing processes, which provide additional insights into our study results (Section 4.2).

### Time
For Time, the whole test suite runs in the same testing environment but consists of 18 sub-test suites which refer to different components of the system and which are managed by different teams.
For Pareto testing and the calculated optimal cost limit $L_o$ = 25%, two sub-test suites (i.e., teams) would have missed build failures.
For test impact analysis, the input time range covered a - for automated tests - comparably large time span of a whole week with comparably many code changes.
In turn, this resulted in the ineffective selection of test cases (see also RQ<sub>2.3</sub> in Section 4).
Figure 4 does not report on fault detection rates for new test failures at Time since the collection of meaningful data would have required too many resources in their testing environment.


### BVK
This subject uses a concept called _chained testing_, where, at first, individual test cases are run and then the same test cases are run within chained test cases.
This way, the output of one test case serves as input for the next test case.
Since chained tests are more expensive to run than individual test cases, both optimization techniques prefer individual test cases for their selection and prioritization.
This is why it can take a long time to detect failures of chained test cases, which explains why in Section 4, the fault detection rate of Pareto testing for BVK in Figure 4 is relatively low and accelerates towards the end.
Notably, failing chained tests are often redundant with a failing individual test case, so, it is less critical to miss these.


### Dolby
Our study setup monitors test executions in the study subject's pipeline, but developers often run tests locally before running tests in the central pipeline, resulting in less pipeline failures.
For Pareto testing, the fault detection rate jumps quickly to 100%, because over a recording time span of about 5 months, there were only 14 test failures, and the corresponding test cases are comparably quick, which fits well with the optimization criteria.
The results of RQ<sub>2.1</sub> in Section 4, show that test impact analysis yields a comparably low fault detection rate of 60% because an infrastructure-related test case, which is not testing the application and its implementation accounts for several of the failures.


### ILP
After our study, the subject's team reported that test impact analysis _just works and shows awesome results_.
Besides this positive feedback, they note that the _test case selection is less effective and meaningful_, which is also shown as result for RQ<sub>2.3</sub> in Figure 5b.
First, this is because of the large amount of code changed per test phase, in this case around 7800 changed methods, which requires many tests to be executed to cover all changes.
Second, most of their end-to-end tests have a high code coverage per test case which can result in a large set of test cases covering a single change.
Pareto Testing yields the optimal cost limit L<sub>o</sub>=15%, for which approximately 61% of failures are detected. 

### Zeiss
The second manual test suite in our study produces similar results like the manual test suite of ILP:
First, for test impact analysis, almost all test cases are selected, yielding a perfect fault detection rate but also producing only 1% of time savings.
Still, the prioritization of tests is effective and the time-to-first-failure is 6-times faster than the baseline.
Similar to ILP, the development timespan is rather long: 2.5 months with approx. 800 commits and 4,500 changed methods.
Second, Pareto testing achieves optimal cost-benefits for the cost limit L<sub>o</sub>=30%, which detects approximately 61% of failures.
The changes performed in the 2.5-months development phase were widely spread over the whole code base.
This explains the need of more tests to obtain a similar fault detection rate of the lower optimal cost limit for ILP.

## Plotting Scripts

Due to confidentiality agreements, we cannot provide access to the raw data of our paper. For reproducibility reasons we publish scripts that generate the plots of our paper, which also contain the presented data in an aggregated manner:  

* [Plots for RA1: Test Strategies](https://anonymous.4open.science/r/Test-Optimization-in-Industry-D14E/01_Testing-Strategies-plots-public.ipynb)
* [Plots for RA2: Test Optimization](https://anonymous.4open.science/r/Test-Optimization-in-Industry-D14E/02_Optimization-plots-public.ipynb)