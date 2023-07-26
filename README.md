# Optimization of Automated and Manual Software Tests in Industrial Practice: A Survey and Historical Analysis

### Table1: Table 1: Overview of study subjects
| Company                        | Domain          | Test Process    | Team Size | SLOC   | Language |
|--------------------------------|-----------------|---------|------|--------|----------|
| Time                           | Time Management | A       | 50   | 8M   | Java     |
| BVK                            | Finance         | A       | 20   | 300K | Java     |
| Dolby                          | Audio           | A       | 10   | 28K  | C        |
| ILP                            | ERP             | M       | 5    | 831K | C\#      |
| Zeiss                          | Optics          | M       | 90   | 6M   | C\#      |

### Table 2: Survey questions to answer the research questions

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

### Discussion Study Subjects

\subsection{Discussion}\label{sec:discussion}

Next, we provide more details on our study subjects and their testing processes, which are relevant to interpret our study results.

#### Time
For Time, the whole test suite runs in the same testing environment but consists of 18 sub-test suites which refer to different components of the system and which are managed by different teams.
For Pareto testing and the calculated optimal cost limit L_o = 25%, two sub-test suites (i.e., teams) would have missed build failures.
For \tia{}, the input time range covered a---for automated tests---comparably large time span of a whole week with comparably many code changes.
In turn, this resulted in the ineffective selection of test cases (see also \rqnCostBenefit in Section~\ref{sec:results}).
Figure~\ref{fig:rq2-1-pareto} does not report on fault detection rates for new test failures at \subjectA{} since the collection of meaningful data would have required too many resources in their testing environment.


\textbf{BVK.}
This subject uses a concept called \quotebox{chained testing}{,} where, at first, individual test cases are run and then the same test cases are run within chained test cases.
This way, the output of one test case serves as input for the next test case.
Since chained tests are more expensive to run than individual test cases, both optimization techniques prefer individual test cases for their selection and prioritization.
This is why it can take a long time to detect failures of chained test cases, which explains why in Section~\ref{sec:results}, the fault detection rate of \Pareto{} for BVK in Figure~\ref{fig:rq2-1-pareto} is relatively low and accelerates towards the end.
Notably, failing chained tests are often redundant with a failing individual test case, so, it is less critical to miss these.


\textbf{Dolby.}
Our study setup monitors test executions in the study subject's pipeline, but developers often run tests locally before running tests in the central pipeline, resulting in less pipeline failures.
For \Pareto{}, the fault detection rate jumps quickly to 100\%, because over a recording time span of about 5 months, there were only 14 test failures, and the corresponding test cases are comparably quick, which fits well with the optimization criteria.
The results of \rqnFaultRevelation in Section~\ref{sec:results}, show that \tia{} yields a comparably low fault detection rate of 60\% because an infrastructure-related test case, which is not testing the application and its implementation accounts for several of the failures.


\textbf{ILP.}
After our study, the subject's team reported that \tia{} \quotebox{just works and shows awesome results}{.}
Besides this positive feedback, they note that the \quotebox{test case selection is less effective and meaningful}{,} which is also shown as result for~\rqtCostBenefit{} in Figure~\ref{fig:rq2-3-sub2}.
First, this is because of the large amount of code changed per test phase, in this case around 7800 changed methods, which requires many tests to be executed to cover all changes.
Second, most of their end-to-end tests have a high code coverage per test case which can result in a large set of test cases covering a single change.

\textbf{Zeiss.}
\begin{itemize}
    \item Pareto results look similar to ILP
    \item Develop over a rather long timespan of almost 2.5 months
    \item ~800 commits in that timespan
    \item ~4500 changed methods
    \item diverse set of changes over the whole codebase -> \Pareto needs a long time to find them
\end{itemize}
